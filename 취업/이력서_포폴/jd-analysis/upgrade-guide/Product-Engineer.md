---
type: upgrade-guide
job: Product-Engineer
target_project: mindgraph
based_on: zighang Product Engineer + Product Builder + 프로덕트 엔지니어 합본 78건 + matrix.md
created: 2026-05-26
last_updated: 2026-05-31
---

# Product Engineer 관점 mindgraph 업그레이드 로드맵

## 1. 직무 핵심 빈출 자격·우대 (zighang PE 78건 합본 Top 6)

- 코드부터가 아니라 정의부터 시작하는 문제 정의 우선 사고 — `requirements/Product-Engineer.md`
- 직접 만들고 검증하는 빌더 정신
- 주도적 오너십 (복잡한 문제 해결을 주도, 제품 개발 사이클을 이끌어)
- 좋은 설계와 나쁜 설계를 자기 기준으로 판단
- "무엇을 할지 / 무엇을 버릴지" 판단 (제한된 시간)
- 작은 팀에서 끝까지 책임지고 마무리한 경험 + 풀스택 엔지니어 지향

추가 우대 빈출: 하네스·Cursor Skill·Sub-agent·MCP 같은 AI 워크플로우 자산 직접 생성, Zero to One·MVP·빠른 검증, AI 기반 프로덕트 직접 개발·배포·운영, 대규모 트래픽 성능 최적화.

> 표본 교체 이력: 2026-05-30 Product Engineer 30건 → Product Engineer + Product Builder + 프로덕트 엔지니어 78건 합본. "문제 정의 우선·작은 팀 끝까지 책임" 키워드 가시화.

## 2. mindgraph 현재 자산 매칭 (matrix.md §4 인용, 2026-05-28~29 시스템 재편 반영)

매칭됨:
- 풀스택 (Chrome Extension MV3 + Next.js 16 App Router + Supabase) → `department/dev/src/`, `department/dev/web/`
- 1인 PO 출시 전 프로토타입 → 도메인 getmindgraph.com 등록 후 1인 프로토타입 빌드 단계 (실서비스 운영 X)
- AI 워크플로우 자산 (PE 시그니처) → `.claude/hooks/` 9개 훅(차단 게이트 4: spec-gate · linear-done-gate · build-pr-block · inp-cycle-guard + 보조 5: stale-warn · inp-reuse-suggest · integrity-sync · context-pack-stale · worktree-env-symlink) + `.claude/skills/{sprint,feature-contract,adr-record,review-swarm,context-pack-regen,cycle-brief}/` 6개 skill + `/sprint` 3 phase(plan · qa · ship) 메타 스킬
- 4중 SSOT → SPRINT.md · Linear Cycle · Git · CHANGELOG, 이월 옵션 mechanism 차단으로 검증 안 된 변경의 main 머지 사전 차단
- 부서·에이전트 분리 + context-map 자동 라우팅 (신규 매칭) → 7개 부서(design · dev · docs · marketing · ops · product · qa) + 9개 에이전트(ceo · frontend/backend/qa-engineer · product-manager · ui-ux-designer · marketing-strategist · ops-engineer · knowledge-logger)별 CLAUDE.md + docs lifecycle 분리. `RULES/context-map.md` + `SYSTEM/schemas/code-doc-mapping.yaml`로 task_type 6종과 코드 path glob을 must-read doc에 자동 매핑, CEO → 워커 위임 시 합집합 5개 내외 doc만 prompt에 첨부 → PO가 가설을 코드로 옮길 때 LLM 응답 정확도·토큰 비용 동시 확보
- 권위 계층 L1~L4 → L1 Canonical Principles · L2 Domain SSOT + Operational Playbook · L3 Cycle Records · L4 Generated Cache (2026-05-28 재편)
- 사용자 흐름 의사결정 → Write-Behind 캐시(`sync-engine.ts` MAX_RETRIES = 5) · Optimistic UI · IndexedDB 우선 저장 · Realtime 멀티 디바이스 통합
- 출시 후 가설 검증 인프라 사전 구축 → PostHog 행동 이벤트 + Sentry 에러 + OpenTelemetry 로그 + `app/api/feedback` + `app/api/error-log` 4개 채널을 한 PR 단위로 묶음 → 출시 후 sprint retro 입력으로 곧장 이어 붙일 수 있는 관측성 인프라
- 임베딩 추천 + 정량 측정 인프라 (신규 매칭) → `lib/auto-link/related-nodes.ts` 코사인 top-K + `lib/telemetry.ts`의 AccuracyEvent(H1 top-3 ≥ 60%) + InteractionEvent(H3 클릭률 ≥ 60%)

Gap:
- PostHog feature flag 기반 A/B 분기 → PostHog SDK 도입은 되어 있으나 실험 그룹 분기·전환 funnel 측정 흔적 미확인
- Core Web Vitals 자동 측정 (LCP · INP · CLS) → `web-vitals` 라이브러리 도입·CI 임계 차단 흔적 미확인
- E2E 자동 회귀 차단 → `e2e/` · `playwright.config.ts` 존재하나 GitHub Actions CI 연동 흔적 미확인
- 자체 AI 워크플로우 자산 외부 사용 가능 형태 → 9개 훅 · 3 phase sprint · 6 skill · context-map이 사용자 코드 자산이나 npm 패키지·외부 저장소 배포 미확인 (PE 시그니처 키워드 "Sub-agent · MCP 같은 AI 워크플로우 자산을 직접 만들고 운영"의 외부 검증 가능 자산화 Gap)
- LLM 비용 라우팅 (Haiku · Flash · mini 선택) → 후속 LLM API 호출 어댑터 자체가 미확인이라 라우팅도 미확인

## 3. 업그레이드 후보

### 1. PostHog 기반 A/B 테스트 + 실험 그룹 분기
- **무엇**: 캡처 버튼 위치·온보딩 카피·노드 색상 알고리즘 같은 가설을 실제 사용자에게 A/B로 노출하고 PostHog feature flag로 분기. 전환 지표(첫 캡처 완료율·재방문율)를 PostHog Insights로 측정.
- **왜**: zighang PE 우대 "사용자 지표 우선순위·UX 감각" + "AI 기반 프로덕트를 직접 개발·배포·운영"에 직접 매칭. PO가 가설을 사용자로 검증한 흔적.
- **주요 파일**: `department/dev/web/instrumentation-client.ts`, `department/dev/web/lib/posthog/` 신규
- **도입 난이도**: S (PostHog 이미 도입)
- **우대 키워드 매핑**: "사용자 지표 우선순위·UX 감각", "MVP를 빠르게 만들고 검증"

### 2. Core Web Vitals 모니터링 자동화
- **무엇**: `web-vitals` 라이브러리로 LCP·INP·CLS를 측정해 Sentry·PostHog에 자동 전송. 임계치 초과 시 Sentry 알림.
- **왜**: zighang PE 우대 "대규모 트래픽 환경에서 시스템 안정성을 확보하고 성능을 최적화" 매칭. 운영 데이터 기반 의사결정 증거.
- **주요 파일**: `department/dev/web/instrumentation-client.ts`, `department/dev/web/app/layout.tsx`
- **도입 난이도**: S
- **우대 키워드 매핑**: "성능 최적화", "프로덕션 환경에서의 모니터링·장애 대응"

### 3. 9개 훅·3 phase sprint·6 skill·context-map을 외부 사용 가능한 sub-agent 패키지로 추출
- **무엇**: `.claude/hooks/` 10개, `.claude/skills/{sprint,feature-contract,adr-record,review-swarm,context-pack-regen,cycle-brief}/`, `RULES/context-map.md` + `SYSTEM/schemas/code-doc-mapping.yaml`을 npm 또는 별도 저장소로 추출해 다른 1인 개발자가 설치·사용 가능하게 만들기. README·설치 가이드·예제 포함.
- **왜**: zighang PE 우대 빈출 "하네스(Harness) · Cursor Skill/Rule · Sub-agent · MCP 같은 AI 워크플로우 자산을 직접 만들고 운영" 직접 매칭. 자산이 외부 검증 가능해짐.
- **주요 파일**: `mindgraph/.claude/` + `RULES/` 일부 추출 → 신규 저장소 또는 `packages/harness-kit/`
- **도입 난이도**: M~L (코드 추출 + 일반화 + 문서화)
- **우대 키워드 매핑**: "Sub-agent · MCP 같은 AI 워크플로우 자산을 직접 만들고 운영", "조직 차원에서 AI 기반 개발 워크플로우를 정립하거나 고도화"

### 4. 사용자 행동 funnel + 활성 사용자 코호트 정의
- **무엇**: PostHog 이벤트를 (방문 → 캡처 → 트리 생성 → 재방문) 4단계 funnel로 정의하고, 활성 사용자(주간 1+ 캡처) 코호트 정의. 가설 검증마다 funnel 영향도 측정.
- **왜**: zighang PE 자격 "사용자에게 가치를 주는 기능 개발에 기쁨" + 우대 "혼자서 5개 이상 프로덕트 또는 1개라도 YoY 3배 이상의 성장" 매칭. PO가 사용자 데이터로 사고하는 증거.
- **주요 파일**: `department/dev/web/lib/analytics/funnels.ts` 신규
- **도입 난이도**: S
- **우대 키워드 매핑**: "사용자 지표 우선순위", "YoY 성장"

### 5. Playwright E2E를 GitHub Actions CI에 연결
- **무엇**: 현재 `e2e/`와 `playwright.config.ts` 존재. PR마다 자동 실행해 사용자 흐름(캡처 → 트리 생성 → 노드 클릭) 회귀 차단.
- **왜**: zighang PE 우대 "테스트 자동화를 통한 품질/효율성 향상" 매칭. 빠른 릴리즈 사이클의 안전망.
- **주요 파일**: `.github/workflows/e2e.yml` 신규, `department/dev/web/playwright.config.ts`
- **도입 난이도**: S
- **우대 키워드 매핑**: "테스트 자동화를 통한 품질/효율성 향상"

### 6. /sprint plan 단계 PRD 템플릿 강제화
- **무엇**: 현재 3 phase sprint의 plan 단계가 Linear Cycle 생성·SPRINT.md 작성·RESEARCH.md 자동 기록을 처리하나, PRD 템플릿이 별도 active doc(`department/product/docs/active/PRD.md`)에 있어 cycle마다 갱신 강제성 약함. plan 단계 산출물에 "사용자 가설 → 문제 정의 → 기술 결정 → 측정 지표 → 결과" 5섹션 PRD 템플릿을 추가하고 spec-gate.sh가 PRD STALE 시 코드 작성 차단(이미 PRD/FEATURES/KPI_METRICS STALE 체크가 plan에 들어가 있으니 강도 상향).
- **왜**: zighang PE 시그니처 "코드부터가 아니라 정의부터 시작하는 문제 정의 우선 사고" 직접 매칭. PO 사고가 코드 변경 옆에 함께 기록되는 흔적.
- **주요 파일**: `.claude/skills/sprint/SKILL.md`, 신규 `RULES/templates/prd-cycle.md`
- **도입 난이도**: S

### 7. LLM 비용 라우팅
- **무엇**: 후속 질문 기능 도입 시 (FDE 가이드 3번과 동일 기능), 비용·품질에 따라 Claude Haiku · Gemini Flash · GPT-4o-mini 라우팅. 사용자 요청 유형(요약·번역·분류)별 모델 선택 규칙.
- **왜**: zighang PE 우대 "AI 기반 프로덕트를 직접 개발·배포·운영" + 운영 비용 의사결정 흔적.
- **주요 파일**: `department/dev/web/lib/llm/router.ts` 신규
- **도입 난이도**: M

## 4. 우선순위

1. **1번 (PostHog A/B 분기)** — PostHog 이미 도입, PE 시그니처 키워드 가장 강함
2. **2번 (Core Web Vitals)** — 1일 작업, Sentry·PostHog 연동 즉시
3. **4번 (funnel 정의)** — 1번과 묶어 한 번에 PR
4. **5번 (E2E CI)** — Playwright 이미 도입, GitHub Actions만 추가
5. **3번 (sprint sub-agent 추출)** — zighang PE 우대 키워드 가장 강함, 시간은 좀 더 필요
6. **6번 (PRD 템플릿)** — 가벼우나 효과 가시성 작음
7. **7번 (LLM 라우팅)** — 후속 질문 기능 도입과 묶어야 의미

## 5. 안 하는 것 (의도적 제외)

- **음성 에이전트 파이프라인** — zighang 일부 공고에 우대로 등장하나 mindgraph 도메인과 거리 멀음
- **의료/핀테크/SaaS/B2B 도메인 매칭** — 도메인 변경은 프로덕트 정체성 변형, 가이드 범위 밖
- **마이크로프론트엔드 분리** — 현재 단일 Next.js app 규모에서 과잉 설계, 사용자 가설 검증 속도를 늦춤
