---
title: xAB (A/B 테스트 SNS) 기술 면접 준비
aliases:
  - xab interview prep
  - xAB 면접
  - A/B test SNS
type: interview-prep
project: xab
status: budding
created: 2026-05-23
updated: 2026-05-23
tags:
  - career
  - interview-prep
  - project/xab
  - status/budding
  - career/product-engineer
  - career/fe
related:
  - "[[취업/_INDEX]]"
  - "[[../../../xab/_INDEX]]"
  - "[[이력서가이드]]"
source:
  - ~/깃허브/취업/이력서_포폴/이력서_포폴_v2/xab_interview_prep.md
migrated-from: 깃허브/취업/이력서_포폴/이력서_포폴_v2/xab_interview_prep.md
---

# xAB (A/B 테스트 SNS) 기술 면접 및 포트폴리오 상세 설명서

이 문서는 `xab_portfolio.md`의 각 케이스에 대한 기술 근거(Rationale), 예상 면접 질문, 그리고 실제 코드 구현 위치를 정리한 자료입니다.

---

## Case 1. LCP 최적화 (Lazy Loading & Infinite Scroll)

### 📌 핵심 기술 근거
- **Critical Rendering Path**: 초기 로딩 시 불필요한 네트워크 요청과 DOM 생성을 막아야 LCP(Largest Contentful Paint)가 개선됩니다.
- **Resource Efficiency**: 사용자가 보지 않을 수도 있는 데이터를 미리 가져오는 것은 모바일 데이터와 서버 리소스 낭비입니다.

### ❓ 예상 면접 질문
1. **Q: 일반적인 페이지네이션 대신 무한 스크롤을 구현할 때 주의할 점은?**
   - **A:** 스크롤 이벤트 디바운싱(Deboucing) 혹은 `Intersection Observer` 사용 여부입니다. 저는 `react-intersection-observer`를 사용하여 구현 복잡도를 낮추고 성능을 확보했습니다. 또한, 뒤로가기 시 스크롤 위치 유지(Scroll Restoration) 문제도 고려해야 합니다.

2. **Q: useInfiniteQuery의 `getNextPageParam`은 어떻게 동작하나요?**
   - **A:** 서버 응답에 다음 페이지 번호나 커서(Cursor) 정보가 포함되어야 합니다. 이 값을 반환하면 `fetchNextPage` 호출 시 자동으로 인자로 전달되어 다음 데이터를 가져옵니다.

### 📍 코드 구현 (Code References)
- **`infinite-survey-list.tsx` (@/xab/src/components/home/infinite-survey-list.tsx)**
    - `line 67-74`: `useInfiniteQuery` 구현. `getNextPageParam` 설정.
    - `line 90`: `useInView({ threshold: 0.1 })`로 하단 트리거 감지.
    - `line 109-113`: `inView`가 `true`이고 `hasNextPage`가 있으면 `fetchNextPage()` 실행.

---

## Case 2. Soft Navigation (Intercepting & Parallel Routes)

### 📌 핵심 기술 근거
- **Context Preservation**: 사용자가 피드를 탐색하던 스크롤 위치와 맥락을 잃지 않으려면 페이지 전체를 갈아끼우는 Hard Navigation 대신, URL만 바꾸고 화면 일부만 덮어쓰는 Soft Navigation이 필요합니다.

### ❓ 예상 면접 질문
1. **Q: Next.js의 Intercepting Route는 어떤 원리인가요?**
   - **A:** 클라이언트 사이드 라우팅(`Link` 클릭)으로 진입할 때만 라우트를 가로채서 다른 컴포넌트(모달)를 렌더링하고, 새로고침이나 직접 URL 입력 시에는 원래의 페이지 컴포넌트를 렌더링하는 조건부 라우팅 메커니즘입니다.

### 📍 코드 구현 (Code References)
- **(추정) File Structure**
    - `src/app/@modal/(.)write/page.tsx`: 가로채기(Intercept) 라우트 정의.
    - `src/app/write/page.tsx`: 원본 페이지 정의.
    - `src/app/layout.tsx`: `props.modal`을 받아 렌더링하는 슬롯(Slot) 설정.

---

## Case 3. Realtime Updates (Supabase CDC)

### 📌 핵심 기술 근거
- **Event-Driven**: 클라이언트가 서버에게 "새 데이터 있나요?"라고 계속 묻는(Polling) 대신, 서버(DB)가 데이터 변경 시 이벤트를 "발행(Publish)"하고 클라이언트가 이를 "구독(Subscribe)"하는 모델이 효율적입니다.
- **Cache Invalidation**: 실시간 데이터가 들어오면 기존에 가지고 있던 React Query의 캐시를 "오래된 데이터(Stale)"로 취급하고 다시 가져오게(Refetch) 만들어야 데이터 정합성이 유지됩니다.

### ❓ 예상 면접 질문
1. **Q: Supabase Realtime의 장점은 무엇인가요?**
   - **A:** 별도의 WebSocket 서버를 구축할 필요 없이, PostgreSQL의 WAL(Write Ahead Log)을 감지하여 CRUD 이벤트가 발생하면 자동으로 클라이언트에게 알려준다는 점입니다. 백엔드 코드 작성 없이 DB 레벨에서 실시간성을 확보할 수 있습니다.

2. **Q: 소켓 이벤트 수신 후 UI 업데이트는 어떻게 처리했나요?**
   - **A:** 소켓으로 들어온 데이터를 직접 State에 push 할 수도 있지만, 데이터 정합성을 위해 `queryClient.invalidateQueries`를 호출하여 React Query가 원본 데이터를 다시 안전하게 가져오도록 처리했습니다. (Optimistic Update와 병행 가능)

### 📍 코드 구현 (Code References)
- **`use-realtime-comments.ts` (@/xab/src/hooks/use-realtime-comments.ts)**
    - `line 12`: `supabase.channel` 생성.
    - `line 14`: `postgres_changes` 이벤트 리스너 등록. `table: comments`, `filter: post_id=eq...`로 특정 게시글 댓글만 감지.
    - `line 22`: 이벤트 수신 시 `queryClient.invalidateQueries` 실행.
