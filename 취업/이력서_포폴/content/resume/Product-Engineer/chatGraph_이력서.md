### chatGraph (AI 대화 시각화 플랫폼)

서비스 개요: LLM과의 대화를 꼬리물기 형태의 마인드맵 그래프로 시각화해 비선형 사고 흐름을 보존하는 웹 서비스. 4인 팀의 FE 한 명으로 응답 대기 동안의 사용자 흐름과 시각화 라이프사이클을 담당했습니다.

팀원: 4명 (FE 2명, BE 2명)

기술 스택: TypeScript, React, Next.js, D3.js, Zustand, Tailwind CSS, TanStack Query, Vitest

- 새 토픽 생성 시 LLM 응답 대기로 화면이 멈추는 문제를 해결하기 위해 sessionStorage에 프롬프트를 저장하고 temp ID로 즉시 라우팅한 뒤 mutation 성공 시 실제 ID로 교체하는 Optimistic 라우팅을 설계했습니다.

- 사이드바 토픽 클릭 시 초기 로딩 지연을 줄이기 위해 Zustand 스토어에 응답을 프리패치하고 useSuspenseQuery의 initialData로 주입해 라우트 전환 시 빈 화면 없이 데이터가 즉시 그려지게 했습니다.

- 843줄까지 비대해진 use-question-tree 훅을 책임 단위로 분리해 355줄로 축소하고 Feature-First 구조로 도메인·조립·공통 계층을 나눴습니다.

- 거대해진 페이지 컴포넌트를 TopicContentLayout·StandardChatView·OptimisticChatView 뷰 계층으로 나누고 findPathToNode 경로 탐색·토픽 토글 훅에 Vitest 회귀 테스트를 작성했습니다.

- 팀원이 도입한 D3 Force Simulation과 React 리렌더 충돌을, 매 갱신마다 전체 SVG를 재생성하던 방식에서 노드 id 키 기반 enter/update/exit 데이터 조인으로 바꿔 변경 노드만 갱신하고 시뮬레이션을 재사용하도록 개선했습니다.
