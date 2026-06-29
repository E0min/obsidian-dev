### xAB (A/B 테스트 기반 SNS)

서비스 개요: 두 가지 선택지에 대한 실시간 투표 및 댓글 토론이 가능한 소셜 네트워크 서비스. Next.js App Router 위에서 프로필·팔로우 도메인과 @modal 인터셉팅 라우트 모달·무한스크롤 피드를 담당했습니다.

팀원: 4명 (FE 4명)

기술 스택: TypeScript, Next.js, React Query, Zustand, Supabase, Tailwind CSS

- 글쓰기 화면 진입 시 피드 위치와 맥락이 끊기는 문제를 App Router의 `@modal` 병렬 슬롯과 `(.)write` 인터셉팅 라우트를 결합한 모달 라우팅으로 해결하고, 직접 접근 시 `app/write` 전체 페이지로 폴백하도록 구성했습니다.

- 프로필·팔로우 도메인을 단독으로 맡아 프로필 페이지(`profile/[id]`)와 팔로워·팔로잉 API·페이지를 구현하고, 팔로우 토글을 서버 액션(`useActionState`)으로 처리한 뒤 `router.refresh()`로 최신 상태를 반영했습니다.

- 팔로워·팔로잉 목록을 페이지 이동 없이 띄우기 위해 App Router의 `@modal` 병렬 슬롯과 `(.)followers`·`(.)followings` 인터셉팅 라우트를 결합해 모달로 가로채고, 직접 접근 시에는 전체 페이지로 폴백하도록 구성했습니다.

- 메인 피드 초기 로딩 지연을 줄이기 위해 TanStack Query의 `useInfiniteQuery`와 Intersection Observer 트리거를 결합해 페이지 단위 분할 호출 기반 무한 스크롤 피드를 구현했습니다.

- 팔로우한 유저와 본인 게시글을 묶어 보여주는 피드 API(`api/posts/feed`)를 page·limit·offset 기반 페이지네이션으로 구현하고, A/B 투표·좋아요 API(`api/vote`·`api/like`)를 함께 맡아 피드의 쓰기 경로를 처리했습니다.
