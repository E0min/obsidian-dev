---
type: upgrade-guide
job: FE
target_project: mindgraph
based_on: zighang depthTwos=프론트엔드 + keyword=frontend 합본 93건 + matrix.md
created: 2026-05-26
last_updated: 2026-05-31
---

# Frontend Engineer 관점 mindgraph 업그레이드 로드맵

## 1. 직무 핵심 빈출 자격·우대 (zighang FE 93건 합본 Top 6)

- HTML5 · CSS3 · JavaScript(ES6+) 깊은 이해 및 내부 동작 원리 — `requirements/FE.md`
- Git 활용 협업 및 코드 리뷰 프로세스
- TypeScript 정적 타입 기반 견고한 코드 작성
- 빌드 도구 (ESBuild · Vite · Webpack · SWC · Babel) 이해
- 반응형 웹 · 크로스 브라우저 · 웹 접근성 · 웹 표준
- 테스트 · 배포 자동화 · 프로젝트 리딩 경험

추가 우대 빈출: 디자인 시스템 토큰화, axe·Lighthouse 접근성 검증, Storybook 컴포넌트 카탈로그, Storybook visual regression, RSC(React Server Components) 활용.

> 표본 교체 이력: 2026-05-30 frontend 키워드 30건 → depthTwos=프론트엔드 + keyword=frontend 93건 합본. "빌드 도구 이해 · HTML/CSS/JS 내부 동작" 가시화.

## 2. mindgraph 현재 자산 매칭 (matrix.md §4 인용)

매칭됨:
- React 19 + TypeScript + Next.js 16 App Router → `department/dev/web/`
- D3 + SSR 격리 (`'use client'` + transpilePackages) → `department/dev/web/next.config.ts`
- Vite 3종 빌드 설정 분리 → `vite.config.extension.ts`(Service Worker) · `vite.config.content.ts`(Content Script) · `vite.config.bridge.ts`(인증 bridge) 번들 분리, Next.js webpack 빌드와 공존
- Vitest 단위 테스트 + Playwright e2e → `department/dev/web/vitest.config.ts`, `e2e/`
- next-intl 다국어 활성화 → `department/dev/web/i18n/`, `messages/`
- Sentry + OpenTelemetry + PostHog 관측성 → `instrumentation*.ts`, `posthog.server.config.ts`
- Tiptap 에디터 다중 확장 → `@tiptap/*` 의존 (코드 리뷰·테이블·이미지·하이라이트 등 다중 extension)

Gap:
- WCAG 접근성 자동 검증 → 흔적 미확인
- Storybook 컴포넌트 카탈로그 → 흔적 미확인
- React Server Components 비중 → `'use client'` 우세 추정
- 디자인 시스템 토큰화 → Tailwind config 직접 사용 추정, 토큰 추상 미확인
- 성능 정량 측정 자동화 → Core Web Vitals 측정 흔적 미확인 (PE 가이드와 공통)

## 3. 업그레이드 후보

### 1. 웹 접근성 자동 검증 (axe-core + Lighthouse CI)
- **무엇**: Vitest 또는 Playwright 위에 `@axe-core/playwright`를 끼워 주요 화면(캡처 페이지·canvas·sidebar) 접근성 위반 0 보장. Lighthouse CI를 GitHub Actions에서 PR마다 실행해 a11y 점수 임계치(예: 90+) 미달 시 차단.
- **왜**: zighang FE 우대 "디자인 시스템·웹 접근성"(3건) 매칭. axe·Lighthouse 도입은 FE 시니어의 운영 시그널.
- **주요 파일**: `department/dev/web/playwright.config.ts`, `.github/workflows/a11y.yml` 신규
- **도입 난이도**: S (Playwright·CI 이미 도입)
- **우대 키워드 매핑**: "디자인 시스템·웹 접근성"

### 2. Storybook 컴포넌트 카탈로그 + 시각 회귀
- **무엇**: 캡처 버튼·노드 뷰·sidebar·trigger 같은 핵심 컴포넌트를 Storybook 스토리로 분리. Chromatic 또는 Playwright 스크린샷 비교로 시각 회귀를 자동 검증.
- **왜**: zighang FE 우대 "디자인 시스템·웹 접근성"·"테스트 자동화"·"코드 리뷰" 매칭. 협업 표면 가시화.
- **주요 파일**: `department/dev/web/.storybook/`, `department/dev/web/components/*.stories.tsx`
- **도입 난이도**: M
- **우대 키워드 매핑**: "디자인 시스템", "테스트 자동화"

### 3. Core Web Vitals 자동 측정 + 지표 회귀 차단
- **무엇**: `web-vitals` 라이브러리로 LCP·INP·CLS 측정해 Sentry·PostHog 전송. CI에서 Lighthouse CI assertions로 LCP < 2.5s, INP < 200ms 임계 위반 시 PR 차단.
- **왜**: zighang FE 자격 "성능 최적화"(13건) 매칭. 정량 임계가 곧 시니어 시그널.
- **주요 파일**: `department/dev/web/instrumentation-client.ts`, `.github/workflows/lighthouse.yml`
- **도입 난이도**: S
- **우대 키워드 매핑**: "성능 최적화", "프로덕션 환경에서의 모니터링·장애 대응"

### 4. 디자인 시스템 토큰 추상화 (color·spacing·typography)
- **무엇**: 현재 Tailwind config 직접 사용을 1단계 추상으로 분리. `design-tokens/{color,space,type}.ts`에 의미 기반 토큰(예: `surface.primary`, `text.muted`) 정의하고 Tailwind config에서 import. shadcn/ui 같은 컴포넌트 라이브러리도 토큰 위에 작성.
- **왜**: zighang FE 우대 "디자인 시스템" 매칭. 컴포넌트 일관성·테마 교체 가능성을 시각적으로 보여줌.
- **주요 파일**: `department/dev/web/design-tokens/`, `tailwind.config.ts`
- **도입 난이도**: M

### 5. React Server Components 비중 확대 + 분리
- **무엇**: `app/` 라우트의 데이터 로딩을 RSC로 옮기고 `'use client'`는 인터랙티브 컴포넌트(D3 canvas·input form)에만 한정. 페이지 셸·메타데이터·SEO·정적 영역을 서버 렌더로 받기.
- **왜**: zighang FE 자격 "SSR 처리 경험"(4건) + 우대 "큰 규모의 Frontend 시스템 개발/운영" 매칭.
- **주요 파일**: `department/dev/web/app/**`
- **도입 난이도**: M (점진적 리팩터링)
- **우대 키워드 매핑**: "SSR 처리 경험", "Suspense / 서버 컴포넌트"

### 6. PostHog 이벤트 분류 정제 + FE 인터랙션 funnel
- **무엇**: 현재 PostHog 이벤트가 분류 없이 누적되면 분석 불가. `(domain)/(action)/(target)` 같은 명명 규칙 + 이벤트 카탈로그 문서. FE 인터랙션(클릭·hover·scroll depth) 표준 이벤트로 정리.
- **왜**: zighang FE 자격 "사용자 지표 우선순위·UX 감각"(1건) + 우대 "운영 전문성" 매칭. PE 가이드와 공통.
- **주요 파일**: `department/dev/web/lib/analytics/events.ts` 신규, `docs/analytics/event-catalog.md`
- **도입 난이도**: S

### 7. Tiptap 에디터 a11y 강화
- **무엇**: web/package.json에 `@tiptap/*` 다수 의존 확인. Tiptap 에디터의 키보드 단축·ARIA·focus management를 axe로 검증하고 안 보이는 단축키 안내 추가.
- **왜**: zighang FE 우대 "디자인 시스템·웹 접근성" + 시니어 FE의 깊은 도메인 흔적. Tiptap 같은 명령형 에디터의 a11y는 까다로움.
- **주요 파일**: `department/dev/web/components/editor/`
- **도입 난이도**: M

## 4. 우선순위

1. **1번 (a11y axe + Lighthouse CI)** — Playwright·CI 이미 도입, FE 시니어 시그널 빠르게 가시화
2. **3번 (Core Web Vitals)** — PE 가이드 2번과 동일, 한 번에 묶어 PR
3. **6번 (PostHog 이벤트 카탈로그)** — PostHog 이미 도입, 1일 작업
4. **2번 (Storybook + 시각 회귀)** — 시니어 협업 시그널, M 분량
5. **4번 (디자인 토큰)** — Storybook 2번과 묶어 효과 ↑
6. **5번 (RSC 비중 확대)** — 점진적, 시간 필요
7. **7번 (Tiptap a11y)** — 깊은 도메인 시그널이나 우선순위는 후순위

## 5. 안 하는 것 (의도적 제외)

- **마이크로프론트엔드 분리** — 현재 단일 Next.js app 규모에서 과잉 설계
- **CSS-in-JS 마이그레이션 (styled-components·emotion)** — Tailwind 이미 정착, 마이그레이션 효익 없음
- **상태관리 전면 교체 (Redux 등)** — Zustand·TanStack Query 조합 정착, 변경 무리
- **PWA·Service Worker** — Chrome Extension MV3 도메인과 다른 영역, 변경 범위 큼
