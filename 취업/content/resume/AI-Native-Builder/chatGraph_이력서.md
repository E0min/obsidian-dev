### chatGraph (AI 대화 시각화 플랫폼)

서비스 개요: 선형 채팅 UI에서 사고의 분기와 맥락이 사라지는 한계를 해결하기 위해, LLM과의 대화를 꼬리물기 형식의 마인드맵 그래프로 시각화하여 비선형 사고 흐름을 보존하고 대화의 깊이와 관계를 한눈에 보여주는 웹 서비스

팀원: 4명 (FE 2명, BE 2명)

기술 스택: TypeScript, React, Next.js, D3.js, Zustand, Tailwind CSS, TanStack Query, Vitest

- LLM 응답 지연으로 입력 직후 화면이 멈추는 문제를 해결하고자 sessionStorage에 프롬프트를 저장하고 temp ID로 즉시 라우팅한 뒤 mutation 성공 시 실제 ID로 교체하는 Optimistic 라우팅을 구현했습니다.

- 4인 협업에서 토픽 전환·노드 경로 탐색이 회귀로 무너지는 문제를 막고자 findPathToNode와 Zustand 토픽 토글에 Vitest 회귀 테스트를 작성해 트리 경로 탐색과 토픽 스토어 상태 회귀를 자동 검증했습니다.

- 843줄로 비대해진 단일 훅을 책임 단위로 쪼개 355줄로 축소하고, Feature-First 구조로 features·views·shared를 분리해 LLM 보조 리팩토링이 진입할 모듈 경계를 마련했습니다.

- 거대해진 페이지 컴포넌트를 TopicContentLayout·StandardChatView·OptimisticChatView로 분리하고 useSuspenseQuery 분기에 맞춰 Suspense 경계를 재설계해 응답 상태별 뷰를 정리했습니다.

- 사이드바 토픽 클릭 시 발생하던 초기 로딩 지연을 줄이고자 Zustand 스토어에 응답을 프리패치해 useSuspenseQuery의 initialData로 주입하는 패턴으로 라우트 전환 시 빈 화면 없이 데이터를 즉시 렌더했습니다.

- 팀원이 도입한 D3.js Force Simulation이 React 리렌더 시 SVG 트리와 충돌하는 문제를 해결하고자 useEffect cleanup과 `d3.selectAll("*").remove()`를 결합해 SVG를 다시 그리는 코드를 담당했습니다.
