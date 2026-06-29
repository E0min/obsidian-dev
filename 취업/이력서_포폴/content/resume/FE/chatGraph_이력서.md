### chatGraph (AI 대화 시각화 플랫폼)

서비스 개요: AI와의 대화를 꼬리물기 형식의 마인드맵 그래프로 시각화하여 비선형 사고 흐름을 보존하는 웹 서비스

팀원: 4명 (FE 2명, BE 2명)

기술 스택: TypeScript, React, Next.js, D3.js, Zustand, Tailwind CSS, TanStack Query, Vitest

- 순환 참조를 해소하기 위해 Feature-First 구조로 features·views·shared를 분리하고, 843줄까지 커진 use-question-tree 훅을 책임 단위로 분해해 355줄로 축소했습니다.

- 새 토픽 생성 시 LLM 응답 대기로 화면이 멈추던 문제를 해결하기 위해 sessionStorage에 프롬프트를 저장하고 temp ID로 즉시 라우팅한 뒤 mutation 성공 시 실제 ID로 교체하는 Optimistic 라우팅을 설계했습니다.

- 사이드바 토픽 클릭 시 로딩 지연을 줄이기 위해 Zustand 스토어에 응답을 프리패치해 useSuspenseQuery의 initialData로 주입하여 라우트 전환 시 빈 화면 없이 데이터가 그려지도록 했습니다.

- D3 Force Simulation의 자체 DOM 제어 주기와 React 리렌더 주기가 충돌해, 데이터가 바뀔 때마다 전체 SVG를 지우고 처음부터 다시 그리는 방식으로 동작하고 있었습니다. 이를 노드 id를 키로 한 enter/update/exit 데이터 조인으로 재설계해 추가·삭제된 노드만 부분 갱신하고, svg 프레임·필터·forceSimulation을 마운트 시 1회 생성해 재사용하며 기존 노드 좌표를 보존하도록 바꿨습니다. 이를 통해 토픽 전환 시 전체 DOM 파괴·재건축을 제거하고 변경분만 반영하도록 개선했습니다.

- 비대해진 페이지 컴포넌트를 TopicContentLayout·StandardChatView·OptimisticChatView로 분리하고 useSuspenseQuery 분기에 맞춰 Suspense 경계를 재설계했습니다.

- 경로 탐색·토픽 토글·새 토픽 시작 훅에 Vitest 회귀 테스트를 작성해 리팩토링 전후 결과 일치를 자동 검증했습니다.
