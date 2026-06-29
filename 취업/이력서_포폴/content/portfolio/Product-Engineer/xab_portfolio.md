## [xAB] - 실시간 투표 및 소통 중심의 A/B 테스트 SNS

두 선택지의 실시간 투표·댓글 토론이 곧장 반영되는 SNS로, 본인은 4인 FE 팀에 참여해 Next.js App Router 위에서 프로필·팔로우 도메인과 @modal 인터셉팅 라우트 모달·무한스크롤 피드를 담당했습니다.

### 전체적인 아키텍처
```mermaid
graph TD
    User[User Client] -->|Interaction| FE[Next.js App Router]
    FE -->|조회 fetch| RH[Route Handlers]
    RH -->|Query| SB[Supabase]
    FE -.->|변형 작업| SA[Server Actions]
    SA -.->|Insert / Update / Delete| SB
    SB -->|SQL| DB[(PostgreSQL)]

    subgraph "상태 관리"
        FE -->|서버 상태| RQ[TanStack Query]
        FE -->|클라이언트 상태| ZD[Zustand]
    end

    subgraph "프로필·팔로우"
        FE -->|팔로워/팔로잉 조회| PF[Profile / Follow API]
        PF -->|Query| SB
    end

    subgraph "모달 라우팅"
        FE -->|클라이언트 네비게이션| MD["@modal 인터셉팅 라우트"]
        MD -->|독립 페이지 폴백| FE
    end
```
- Next.js App Router 기반 프론트엔드와 Supabase 백엔드를 결합하여 구축했습니다.
- 조회성 요청은 클라이언트 컴포넌트가 Route Handler를 호출해 Supabase에 접근하는 경로로 처리하고, 게시글 작성·수정·삭제 같은 변형 작업은 Server Actions가 Supabase를 직접 호출하도록 두 경로를 명확히 분리했습니다.
- 서버 상태는 TanStack Query, 클라이언트 전역 상태는 Zustand로 책임을 분리하여 실시간성이 중요한 SNS 환경에서도 캐시 일관성과 사용자 인터랙션 상태를 한 흐름에서 관리했습니다.

### Case 1. 피드 초기 로딩 부담을 줄인 페이지 단위 로딩 전략
#### 1. 문제 원인
- 메인 피드 접속 시 게시글, 투표 옵션, 댓글 수, 좋아요 정보를 한 번에 불러오는 구조에서는 첫 화면 진입 시 응답 페이로드와 렌더링 비용이 크게 누적되었습니다.
- 뷰포트 밖에 있는 게시글까지 동일한 비중으로 페칭과 렌더링을 수행하면서 초기 화면이 그려지기까지의 체감 지연이 발생했습니다.

#### 2. 해결 과정
```mermaid
flowchart LR
    A[User Scroll] -->|Trigger Visibility| B{Intersection Observer}
    B -->|Threshold 도달| C[Fetch Next Page]
    C -->|GET /api/posts/feed?page=N| D[Route Handler]
    D -->|range offset| SB[Supabase]
    SB -->|페이지 단위 응답| E[Append to List]
    E -->|UI Update| F[User View]
```
- 사용자가 당장 보지 않는 데이터까지 한 번에 호출하는 대신 피드를 페이지 단위로 분할하여 호출하는 전략을 수립했습니다.
- `useInfiniteQuery`로 페이지네이션 상태를 관리하고, `react-intersection-observer`로 뷰포트 하단 트리거 요소의 노출 시점을 감지해 다음 페이지를 가져오도록 구현했습니다.
- Route Handler는 `page` 쿼리 파라미터를 받아 Supabase의 `.range(offset, offset + limit - 1)` 메서드로 페이지 단위 응답만 반환하도록 구성하여 서버와 클라이언트가 동일한 분할 단위를 공유하게 했습니다.

#### 3. 결과
- 초기 진입 시 필요한 데이터만 우선 응답하도록 변경하여 첫 화면이 그려지기까지의 체감 지연을 완화했습니다.
- 스크롤 위치에 따라 점진적으로 데이터를 채워 사용자의 탐색 흐름이 끊기지 않는 무한 스크롤 경험을 제공했습니다.
- useInfiniteQuery와 IntersectionObserver로 페이지 단위 분할 호출을 적용해 첫 화면 응답 페이로드와 렌더링 비용을 줄였습니다.

### Case 2. 피드 맥락을 유지하는 모달 라우팅 패턴 적용
#### 1. 문제 원인
- 피드에서 게시글 작성이나 상세 화면으로 이동할 때 전체 페이지가 다시 렌더되면서 스크롤 위치와 진행 중이던 인터랙션이 모두 초기화되는 문제가 있었습니다.
- 기존 라우팅 방식은 페이지 컨텍스트를 완전히 교체하기 때문에 이전 화면의 상태를 유지한 채 상호작용할 수 없는 구조적 한계가 원인이었습니다.

#### 2. 해결 과정
```mermaid
graph TD
    A[User at /feed] -->|클라이언트 네비게이션| B["@modal/(.)write 인터셉트"]
    B --> C[모달 오버레이 렌더]
    C --> D[피드 트리는 백그라운드 유지]
    A -->|새로고침 / 직접 URL 진입| E["/write 독립 페이지 렌더"]
```
- 탐색 흐름을 유지하기 위해 피드 트리는 그대로 두고 그 위에 모달을 띄우는 방식을 채택했습니다.
- Next.js App Router의 병렬 라우트 슬롯(`@modal`)과 인터셉팅 라우트(`(.)write`)를 함께 배치하여, 클라이언트 네비게이션 시에는 모달 오버레이가 렌더되고 직접 URL 진입이나 새로고침 시에는 독립 페이지가 렌더되는 구조를 만들었습니다.
- `@modal/default.tsx`에 빈 슬롯 폴백을 두어 슬롯이 활성화되지 않은 라우트에서도 트리가 흐트러지지 않도록 처리했습니다.

#### 3. 결과
- 게시글 작성과 상세 진입 시 피드 위치와 스크롤 컨텍스트가 보존되어 탐색이 끊기지 않는 경험을 제공했습니다.
- 모달 진입과 독립 페이지 진입을 같은 URL로 처리할 수 있어 공유 링크나 새로고침 시에도 일관된 화면을 유지했습니다.
- @modal 병렬 라우트와 (.)write 인터셉팅 라우트를 결합해 클라이언트 네비게이션은 모달, 직접 URL 진입은 독립 페이지로 갈라지는 흐름을 구성했습니다.

### Case 3. 팔로워·팔로잉 목록을 맥락 유지한 채 여는 모달 라우팅
#### 1. 문제 원인
- 프로필 화면에서 팔로워나 팔로잉 목록으로 이동할 때 별도 페이지로 전환되면 직전 프로필의 스크롤 위치와 탐색 흐름이 끊겼습니다.
- 같은 목록을 공유 링크나 새로고침으로 직접 열었을 때도 동일하게 보여야 했지만, 단일 라우팅 방식으로는 모달과 독립 페이지를 한 URL로 갈라 처리할 수 없었습니다.

#### 2. 해결 과정
```mermaid
graph TD
    A[User at /profile/:id] -->|클라이언트 네비게이션| B["@modal/(.)followers 인터셉트"]
    B --> C[UserListModal 오버레이 렌더]
    C --> D["/api/profile/:id/followers 조회"]
    A -->|새로고침 / 직접 URL 진입| E["/followers 독립 페이지 렌더"]
```
- 프로필 트리를 유지한 채 목록을 띄우기 위해 병렬 라우트 슬롯(`@modal`)과 인터셉팅 라우트(`(.)followers`·`(.)followings`)를 함께 배치했습니다.
- 클라이언트 네비게이션 시에는 `UserListModal`이 `/api/profile/[id]/followers` 응답을 받아 Dialog 오버레이로 렌더되고, 직접 URL 진입이나 새로고침 시에는 `/followers` 독립 페이지가 렌더되도록 구성했습니다.
- `@modal/default.tsx`에 `null` 폴백 슬롯을 두어 슬롯이 활성화되지 않은 라우트에서도 트리가 흐트러지지 않게 했고, 목록 안의 팔로우 버튼은 `/api/follow/[id]`로 POST·DELETE를 보내 followStates를 즉시 갱신하도록 했습니다.

#### 3. 결과
- 팔로워·팔로잉 목록 진입 시 직전 프로필의 스크롤 위치와 탐색 컨텍스트가 보존되어 흐름이 끊기지 않았습니다.
- 같은 URL로 모달 진입과 독립 페이지 진입을 함께 처리해 공유 링크나 새로고침 시에도 일관된 화면을 유지했습니다.
- 목록 안 팔로우 버튼은 모달과 독립 페이지 어느 쪽에서 눌러도 `/api/follow/[id]`로 followStates를 즉시 갱신해, 목록을 닫지 않고 팔로우 상태를 바꿀 수 있게 했습니다.
