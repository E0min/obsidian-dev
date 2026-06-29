---
title: chatGraph 기술 면접 준비
aliases:
  - chatgraph interview prep
  - chatGraph 면접
type: interview-prep
project: chatGraph-FE-local
status: budding
created: 2026-05-23
updated: 2026-05-23
tags:
  - career
  - interview-prep
  - project/chatGraph-FE-local
  - status/budding
  - career/fe
  - career/product-engineer
related:
  - "[[취업/_INDEX]]"
  - "[[../../../chatGraph-FE-local/_INDEX]]"
  - "[[이력서가이드]]"
source:
  - ~/깃허브/취업/이력서_포폴/이력서_포폴_v2/chatgraph_interview_prep.md
migrated-from: 깃허브/취업/이력서_포폴/이력서_포폴_v2/chatgraph_interview_prep.md
---

# chatGraph 기술 면접 및 포트폴리오 상세 설명서

이 문서는 `chatGraph_portfolio.md`의 각 케이스에 대한 기술 근거(Rationale), 예상 면접 질문, 그리고 실제 코드 구현 위치를 정리한 자료입니다.

---

## Case 1. 물리 엔진 기반 시각화 (D3.js & React Integration)

### 📌 핵심 기술 근거
- **Hybrid Rendering**: React가 DOM 제어권을 독점하려 하기 때문에, D3에게 제어권을 넘겨주는 전략이 중요했습니다.
- **Declarative vs Imperative**: React는 선언적이고 D3는 명령적이므로, React의 `useRef`와 `useEffect`를 브릿지로 사용해야 합니다.

### ❓ 예상 면접 질문
1. **Q: React와 D3를 함께 사용할 때 가장 큰 어려움은 무엇이었나요?**
   - **A:** 두 라이브러리 모두 DOM을 조작하려 한다는 점(Control Conflict)입니다. 이를 해결하기 위해 React는 SVG 컨테이너(`ref`)만 렌더링하고, 내부 노드와 링크의 좌표 계산 및 속성 변경은 D3가 직접 DOM을 선택(`d3.select`)하여 업데이트하는 방식을 택했습니다.

2. **Q: 왜 Canvas가 아닌 SVG를 사용했나요?**
   - **A:** 노드 개수가 수천 개 단위가 아니라 수백 개 수준이었고, 각 노드에 대한 클릭 이벤트 및 CSS 스타일링, 접근성 처리가 SVG가 훨씬 용이했기 때문입니다.

### 📍 코드 구현 (Code References)
- **`TopicGraphView.tsx` (@/features/topic/components/conversation/content/topic-graph-view.tsx)**
    - `line 3-8`: React 컴포넌트 내에서 D3 그래프를 `InteractiveD3Graph` 컴포넌트로 래핑하여 사용.
    - `line 28-31`: 데이터(`viewData`)를 prop으로 전달하고, 이벤트 핸들러(`onNodeClick`)를 바인딩.
- **`InteractiveD3Graph.tsx` (추정)**
    - 실제 `forceSimulation` 초기화 및 `d3.select` 로직이 들어있는 곳.

---

## Case 2. Feature-First Architecture & View Composition

### 📌 핵심 기술 근거
- **Scalability**: 기능(Feature) 단위로 코드를 묶어야 프로젝트가 커져도 유지보수가 가능합니다.
- **Circular Dependency**: 상위 뷰가 하위 기능을 import 해야지, 하위 기능이 상위 뷰를 import 하면 순환 참조가 발생합니다.

### ❓ 예상 면접 질문
1. **Q: Feature-First 구조의 장점은 무엇인가요?**
   - **A:** 관련된 코드(API, Hook, Component)가 한 폴더에 모여 있어 코드 탐색 비용이 줄어들고(Cohesion), 특정 기능을 들어내거나 수정할 때 다른 부분에 영향을 덜 줍니다(Decoupling).

2. **Q: 'God Component'를 어떻게 분리했나요?**
   - **A:** 기존 `TopicConversation` 컴포넌트가 가지고 있던 Layout, Chat 렌더링, Graph 렌더링, Modal 관리 책임을 각각 `TopicContentLayout`, `ChatView`, `GraphView`, `GlobalDialogs`로 분리하고, 상위 컴포넌트(`Layout`)가 이를 조합(Composition)하는 방식으로 해결했습니다.

### 📍 코드 구현 (Code References)
- **`TopicContentLayout.tsx` (@/features/topic/components/conversation/content/topic-content-layout.tsx)**
    - 뷰의 뼈대를 잡고 `ChatView`와 `GraphView`를 조건부 렌더링하는 역할.
- **`OptimisticChatView.tsx` (@/features/topic/components/conversation/content/optimistic-chat-view.tsx)**
    - `line 29`: `QuestionTreeContext.Provider`를 제공하고 `TopicContentLayout`을 자식으로 사용.

---

## Case 3. Recursive Tree Optimization (Path Finder & Partial Update)

### 📌 핵심 기술 근거
- **Immutability Performance**: Redux나 Zustand 같은 불변성 스토어에서 깊은 객체를 수정하면, 루트부터 변경된 노드까지의 모든 경로를 새로 생성해야 합니다. 전체를 복사하면 O(N)이지만, 경로만 복사하면 O(depth)로 최적화됩니다.

### ❓ 예상 면접 질문
1. **Q: 깊은 트리 구조에서 렌더링 최적화는 어떻게 했나요?**
   - **A:** 전체 트리를 새로 만드는 대신, 수정하려는 노드와 그 조상 노드들만 새로 객체를 할당(Structural Sharing)하고 나머지 형제 노드들은 참조를 유지했습니다. 그리고 `React.memo`를 사용하여 참조가 바뀌지 않은 컴포넌트는 리렌더링되지 않도록 했습니다.

2. **Q: Path Finder DFS는 왜 필요했나요?**
   - **A:** 불변성 업데이트를 하려면 "어떤 경로를 타고 내려가야 하는지" 알아야 하는데, 매번 전체를 탐색할 수 없으므로 타겟 ID를 주면 경로 배열을 즉시 반환하는 유틸리티가 필요했습니다.

### 📍 코드 구현 (Code References)
- **`useQuestionTree.ts` (@/features/topic/hooks/conversation/breadcrumb/use-question-tree.ts)**
    - `line 117`: `findPathToNode(viewData, nodeToMove.id)`를 사용하여 경로를 찾음.
- **`utils.ts` (findPathToNode)**
    - DFS 알고리즘 구현부.

---

## Case 4. Optimistic Updates & UX (Async Handling)

### 📌 핵심 기술 근거
- **Perceived Performance**: 실제 속도보다 중요한 것은 사용자에게 느껴지는 속도입니다.
- **Consistency**: 낙관적 업데이트 실패 시 롤백(Revert) 로직이 필수입니다.

### ❓ 예상 면접 질문
1. **Q: 낙관적 업데이트 구현 시 가장 까다로운 점은?**
   - **A:** 임시 ID(Temp ID) 관리입니다. 프론트에서 생성한 ID로 트리에 렌더링했다가, 서버에서 실제 ID가 오면 사용자는 눈치채지 못하게 "Swap" 해주는 로직이 복잡했습니다.

2. **Q: Suspense와 Loading Spinner 처리는?**
   - **A:** `OptimisticChatView`에서 데이터가 없거나 로딩 중일 때 `LoadingSpinner`를 보여주고(line 17-23), 데이터가 준비되면 `TopicContentLayout`을 보여줍니다. 이를 통해 초기 진입 시 빈 화면 대신 명확한 로딩 상태를 제공합니다.

### 📍 코드 구현 (Code References)
- **`useQuestionTree.ts` (handleAddQuestion)**
    - `line 232-252`:
        1. `setPrompt("")`: 입력창 즉시 비움. (line 238)
        2. `setIsLoading(true)`: 로딩 상태 표시.
        3. `createQuestion.mutateAsync`: 서버 요청.
        4. `catch`: 에러 시 `setPrompt(optimisticPrompt)`로 롤백. (line 248)
- **`OptimisticChatView.tsx`**
    - `line 13`: `useOptimisticTopicData` 훅을 사용하여 데이터 페칭.
    - `line 17`: 데이터 로딩 중 `LoadingSpinner` 표시.

---
