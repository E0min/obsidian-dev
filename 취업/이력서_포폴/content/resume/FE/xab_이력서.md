### xAB (A/B 테스트 기반 SNS)

서비스 개요: 두 가지 선택지에 대한 실시간 투표 및 댓글 토론이 가능한 소셜 네트워크 서비스

팀원: 4명 (FE 4명)

기술 스택: TypeScript, Next.js, React Query, Zustand, Supabase, Tailwind CSS

- 메인 피드 초기 로딩 지연을 해결하기 위해 TanStack Query의 `useInfiniteQuery`와 Intersection Observer 트리거를 결합해 페이지 단위 분할 호출과 지연 로딩이 적용된 무한 스크롤을 구현했습니다.

- 팔로워·팔로잉 목록을 모달로 띄울 때 페이지 맥락이 끊기던 문제를 해결하기 위해 App Router의 병렬 라우트(`@modal`)와 인터셉팅 라우트(`(.)followers`·`(.)followings`)를 결합해 현재 화면 위에 목록 모달이 겹쳐 뜨도록 구현했습니다.

- 팔로우 도메인을 풀스택으로 맡아 팔로우 토글·팔로워·팔로잉 목록 페이지와 `api/follow/[id]`·`api/profile/[id]/followers`·`api/profile/[id]/followings` 라우트를 설계해 팔로우 관계 조회와 변경 흐름을 구현했습니다.

- 프로필 도메인의 헤더·목록 컴포넌트와 `profile/[id]` 페이지를 구현하고 투표·좋아요 API(`api/vote`·`api/like`)를 작성해 사용자 활동 데이터의 조회·갱신 경로를 담당했습니다.
