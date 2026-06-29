### xAB (A/B 테스트 기반 SNS)

서비스 개요: 두 가지 선택지에 대한 실시간 투표 및 댓글 토론이 가능한 소셜 네트워크 서비스

팀원: 4명 (FE 4명)

기술 스택: TypeScript, Next.js, React Query, Zustand, Supabase, Tailwind CSS

- 메인 피드 초기 로딩 지연을 줄이기 위해 TanStack Query의 `useInfiniteQuery`와 Intersection Observer 트리거를 결합한 페이지 단위 분할 호출·지연 로딩 기반 무한 스크롤 피드를 구현했습니다.

- 글쓰기 화면 진입 시 피드 맥락이 끊기는 문제를 해결하기 위해 App Router의 `@modal` 병렬 슬롯과 `(.)write` 인터셉팅 라우트로 글쓰기 화면을 모달로 띄우고, 직접 진입 시에는 전체 페이지로 폴백하도록 구성했습니다.

- 메인 피드 응답 크기를 줄이기 위해 `api/posts/feed` 라우트에 page·limit·offset 기반 페이지네이션을 구현하고, 팔로잉·본인 게시글을 5건 단위로 잘라 `hasNextPage`·`nextPage`를 함께 내려 무한 스크롤과 연결했습니다.

- 팔로워·팔로잉 목록을 보면서 프로필 맥락이 끊기지 않도록 App Router의 `@modal` 인터셉팅 라우트로 followers·followings 화면을 모달로 띄우고, 직접 진입 시에는 전체 페이지로 폴백하도록 구성했습니다.

- 프로필 도메인의 팔로우 기능을 구현하기 위해 팔로워·팔로잉 조회와 팔로우 토글 API 라우트를 작성하고, 프로필 헤더와 팔로우 목록 페이지에서 같은 카운트가 일관되게 반영되도록 연결했습니다.
