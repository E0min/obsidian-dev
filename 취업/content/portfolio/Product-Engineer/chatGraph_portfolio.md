## [chatGraph] - AI 대화 시각화 플랫폼

기존 선형 채팅 UI에서는 한 갈래 흐름만 살아남고 도중에 떠올린 분기 질문과 맥락이 휘발되어, 깊이 있게 사고를 확장하려는 사용자가 이전 맥락을 다시 짜맞춰야 하는 비용이 컸습니다.
chatGraph는 비선형 사고 흐름을 보존하려는 학습자와 리서처를 위해 AI와의 대화를 꼬리물기 그래프로 시각화합니다. 분기와 깊이를 잃지 않고 사고를 확장하도록 돕습니다. 본인은 4인 팀의 FE 한 명으로 참여해 응답 대기 시 사용자 흐름 단축과 시각화 라이프사이클 안정화를 담당했습니다.

### 전체적인 아키텍처
```mermaid
graph TD
    App["App Router (/app)"] -->|렌더링 위임| Views["페이지 뷰 (/views)"]
    Views -->|기능 조립| Features["기능 모듈 (/features)"]
    Views -->|UI 재사용| Shared["공통 요소 (/shared)"]
    Features -->|공통 로직| Shared

    subgraph "Feature-First Design"
        Features --> Topic[Topic Domain]
        Features --> Auth[Auth Domain]
        Features --> Sidebar[Sidebar Domain]
    end

    Topic -->|상태 관리| Zustand[Zustand Store]
    Topic -->|서버 상태| Query[TanStack Query]
    Topic -->|시각화| D3[D3.js Force]
```
- Next.js App Router 위에 Feature-First 디렉토리 구조를 적용해 도메인 기능과 페이지 조립, 공통 자원을 분리했습니다.
- 본인은 FE 2명 중 1명으로 참여했으며, 아키텍처 재정비, 새 토픽 Optimistic 흐름, useSuspenseQuery 기반 데이터 패칭, 뷰 컴포지션 분리, 테스트 코드 작성을 담당했습니다.
- D3 기반 그래프 시각화의 색상 알고리즘과 호버 인터랙션은 팀원이 주도했고, 본인은 React 라이프사이클 통합과 cleanup 로직을 담당했습니다.

### Case 1. Feature-First 디렉토리 도입과 거대 훅 분해
#### 1. 문제 원인
- 초기 구조에서는 페이지, 기능, 공통 코드의 경계가 모호하여 컴포넌트끼리 서로를 직접 import하는 순환 참조가 반복 발생했습니다.
- 트리 상태와 인터랙션을 모두 끌어안은 use-question-tree 훅이 843줄까지 비대해져 변경 시 영향 범위 파악이 어려웠습니다.

#### 2. 해결 과정
```mermaid
graph TD
    Old["use-question-tree 843줄"]
    Old -->|데이터 책임| Data["use-tree-data"]
    Old -->|인터랙션 책임| Inter["use-tree-interaction"]
    Old -->|서버 변경 책임| Mut["use-graph-mutations"]
    Old -->|조립 책임| Root["use-question-tree 355줄"]
```
- app은 라우팅, features는 도메인, views는 조립, shared는 공통이라는 네 가지 책임으로 디렉토리를 재정의하고 import 방향을 단방향으로 정비했습니다.
- 단일 훅이 들고 있던 책임을 트리 데이터(use-tree-data), 인터랙션 상태(use-tree-interaction), 서버 변경(use-graph-mutations)으로 분리하고 최상위에서 합성하는 형태로 정리했습니다.
- 해당 작업은 본인 단독 커밋 3건에 걸친 점진적 리팩토링으로 진행했으며, 단일 거대 PR이 아닌 분해 방식으로 운영 중 위험을 분산했습니다.

#### 3. 결과
- 핵심 훅을 843줄에서 355줄로 축소하고 인접한 페이지 컴포넌트도 186줄에서 59줄로 정리하여 도메인별 책임을 명확히 했습니다.
- 기능 추가 시 어떤 디렉토리에 어떤 파일이 들어가야 하는지에 대한 팀 내 합의가 잡혀 신규 기능 머지 충돌 빈도가 줄었고, 다음 가설 검증을 받아낼 모듈 구조가 마련되었습니다.
- app·features·views·shared 네 책임으로 import 방향을 단방향으로 고정한 뒤 신규 기능 머지 충돌이 줄었습니다.

### Case 2. 새 토픽 생성 시 LLM 응답 대기 가리기
#### 1. 문제 원인
- 메인 화면에서 첫 질문을 입력하면 LLM 응답이 도착할 때까지 화면이 정지된 듯한 경험이 사용자 몰입을 끊었습니다.
- 토스트나 스피너만 띄우는 방식은 새 토픽이 생성될 URL을 미리 보여주지 못해 뒤로가기와 새로고침 동작이 어색했습니다.

#### 2. 해결 과정
```mermaid
sequenceDiagram
    participant User
    participant Form as StartNewTopicForm
    participant Storage as sessionStorage
    participant Router
    participant Optimistic as OptimisticChatView
    participant API as askQuestion

    User->>Form: 프롬프트 입력
    Form->>Storage: temp-{timestamp} 키로 저장
    Form->>Router: /temp-xxx?optimistic=true 곧장 이동
    Router->>Optimistic: 마운트
    Optimistic->>Storage: 프롬프트 복원해 가짜 트리 렌더
    Optimistic->>API: 실제 mutation 호출
    API-->>Optimistic: 실제 topic ID 응답
    Optimistic->>Router: router.replace로 optimistic 쿼리 제거
```
- StartNewTopicForm에서 temp-{Date.now()} 형태의 임시 ID를 만들어 sessionStorage에 프롬프트를 보관한 뒤 곧장 해당 경로로 push하도록 흐름을 설계했습니다(use-start-new-topic.ts).
- 이동한 경로에서는 useOptimisticTopicData 훅이 sessionStorage 데이터를 복원해 한 단계짜리 트리를 곧장 렌더링하고 동시에 실제 mutation을 실행합니다.
- mutation 성공 시 Zustand 스토어에 응답을 채워 두고 router.replace로 optimistic 쿼리 파라미터를 제거하여 실제 topic ID 경로로 자연스럽게 정착시켰습니다.

#### 3. 결과
- LLM 응답까지의 대기 시간 동안에도 사용자가 자신이 입력한 질문이 그려진 화면을 곧장 볼 수 있어 체감 대기 시간이 줄었고, 첫 입력에서 첫 화면 사이의 사용자 흐름 단절을 없애 가장 큰 이탈 지점을 막았습니다.
- 임시 URL과 실제 URL의 전환을 사용자에게 노출하지 않도록 처리해 새로고침이나 공유 링크 동작도 정상적으로 유지했습니다.
- sessionStorage 임시 키·temp ID 라우팅·mutation 성공 시 router.replace를 한 흐름으로 묶어 첫 입력에서 첫 화면까지의 단절을 없앴습니다.

### Case 3. 라우트 전환 시 빈 화면을 없애는 프리패치 패턴
#### 1. 문제 원인
- 사이드바에서 다른 토픽을 클릭하면 useQuery가 새로 호출되며 페이지가 잠시 빈 상태로 보였습니다.
- App Router의 Suspense fallback이 노출되며 깜빡임이 발생했고, 데이터 양이 많은 토픽일수록 체감 지연이 커졌습니다.

#### 2. 해결 과정
```mermaid
flowchart LR
    Sidebar[사이드바 hover 또는 클릭] -->|선택 토픽 응답 prefetch| Store[Zustand prefetchedResponse]
    Store -->|initialData 주입| Suspense[useSuspenseQuery]
    Suspense -->|곧장 렌더| View[StandardChatView]
    Suspense -->|background fetch| Server[(API)]
    Server -->|최신 데이터| Suspense
```
- 사이드바에서 토픽 응답을 미리 받아 Zustand 스토어의 prefetchedResponse 슬롯에 저장하도록 했습니다.
- 페이지 진입 시 useSuspenseQuery의 initialData에 동일 topicId의 프리패치 응답이 있으면 그대로 사용하고(use-topic-data.ts), 없을 때만 Suspense fallback을 거치도록 분기했으며, 다음 단계에서 백엔드 응답을 transformApiDataToViewData 어댑터로 트리 형태로 변환해 주입했습니다(use-tree-data.ts).
- 사용한 프리패치 데이터는 effect에서 정리해 다음 토픽 전환 시 잔여 데이터가 섞이지 않도록 했습니다.

#### 3. 결과
- 사이드바 기반 라우트 전환에서 빈 화면 노출 없이 트리가 지연 없이 그려지는 흐름을 확보해, 사용자가 토픽 사이를 빠르게 오가는 탐색 경험을 받아낼 수 있게 했습니다.
- useSuspenseQuery initialData와 Zustand prefetchedResponse 슬롯을 같은 topicId로 맞춰, 사이드바 토픽 전환에서 Suspense fallback이 노출되는 경우를 프리패치 미적재 경로로만 한정했습니다.

### Case 4. D3 그래프와 React 라이프사이클의 안전한 통합
#### 1. 문제 원인
- 팀원이 도입한 D3 Force Simulation은 SVG DOM을 직접 변형하기 때문에, React가 동일한 SVG를 다시 그리려고 할 때 잔여 노드나 이벤트 리스너가 남아 시각적 아티팩트가 발생했습니다.
- 토픽이 바뀌거나 트리가 갱신될 때마다 이전 시뮬레이션 상태가 새 데이터에 남는 문제가 있었습니다.

#### 2. 해결 과정
```mermaid
flowchart LR
    Data[ViewData 변경] -->|useEffect deps| Effect[Effect 실행]
    Effect -->|selectAll remove| Clear[SVG 초기화]
    Clear -->|hierarchy 재구성| Build[새 그래프 빌드]
    Build -->|simulation tick| Render[렌더링]
    Effect -->|cleanup| Unmount[안전 정리]
```
- visualizer 컴포넌트의 useEffect에서 `d3.select(svgRef).selectAll("*").remove()`로 매 갱신마다 SVG 하위 트리를 초기화한 뒤 hierarchy와 simulation을 다시 구성하는 패턴을 정리했습니다.
- onNodeClick과 같이 자주 변하는 콜백은 ref로 감싸 effect 의존성에서 분리하고, currentPath 등 시각적 강조에 영향을 주는 값만 deps에 포함해 불필요한 재구성을 막았습니다.
- 색상 알고리즘과 호버 desaturate 같은 시각적 인터랙션은 팀원이 작성한 코드를 유지하고, 본인은 통합 지점인 라이프사이클과 cleanup 흐름에 집중했습니다.

#### 3. 결과
- 토픽이 바뀌거나 트리가 갱신될 때 SVG가 정상적으로 재구성되어 잔여 노드나 중복 이벤트로 인한 시각적 결함이 사라졌고, 사용자가 토픽을 오가도 시각 표현이 일관되게 유지되도록 안정화했습니다.
- 팀원이 작성한 D3 시각화 코드는 그대로 두고 통합 지점인 useEffect cleanup과 selectAll remove만 본인이 맡아, 토픽 전환 시 잔여 노드·중복 이벤트로 인한 시각적 결함을 없앴습니다.
