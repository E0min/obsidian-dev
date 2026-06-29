---
type: upgrade-guide
job: FDE
target_project: mindgraph
based_on: zighang Forward Deployed + AI 솔루션 + Customer Engineer 합본 104건 + matrix.md
created: 2026-05-26
last_updated: 2026-05-31
---

# FDE 관점 mindgraph 업그레이드 로드맵

## 1. 직무 핵심 빈출 자격·우대 (zighang FDE 104건 합본 Top 6)

- 영어·한국어 유창성 (customer-facing, local stakeholder 소통) — `requirements/FDE.md`
- 클라우드·온프레미스·가상화·컨테이너 엔지니어링 경험
- 프로그래밍·디버깅·시스템 디자인·프로토타이핑·데모·고객 워크숍 경험
- 기술 스테이크홀더·임원 대상 발표·소통 경험
- 프로덕션 코드를 직접 작성하고 운영해 본 경험
- 협업·소통 능력

추가 우대 빈출: LLM 기반 음성 AI 에이전트 설계·배포, Langfuse 등 LLM 관측성 도구, BAML·AI SDK·Mastra 통합, 엔터프라이즈 0-1 도입.

> 표본 교체 이력: 2026-05-30 Forward Deployed 30건 → Forward Deployed + AI 솔루션 + Customer Engineer 104건 합본. 프로토타이핑·고객 워크숍·임원 발표 키워드 빈도 가시화.

## 2. mindgraph 현재 자산 매칭 (matrix.md §4 인용, 2026-05-28~29 시스템 재편 반영)

매칭됨:
- 4 LLM API 통합 표면 → `department/dev/src/content/detector.ts` SELECTORS 상수에 ChatGPT·Gemini·Grok·Claude DOM 선택자 모음 + hostname 자동 감지
- 1인 LLM 솔루션 프로토타입 → 도메인 getmindgraph.com 등록 후 출시 전 1인 프로토타입 단계 (실서비스 운영 X, 출시 후 응대 대비 인프라 사전 구축 중)
- 출시 후 응대 인프라 사전 구축 → PostHog 행동 이벤트(`posthog-client.ts`) + Sentry 클라이언트·서버 에러(`sentry.*.config.ts`) + OpenTelemetry 로그(`instrumentation*.ts`) + `app/api/feedback/route.ts` + `app/api/error-log/route.ts` 5개 채널을 코드 베이스에 사전 배치
- Claude Code 하네스 → `.claude/hooks/` 9개 훅(차단 게이트 4개: spec-gate · linear-done-gate · build-pr-block · inp-cycle-guard + 보조 알림 5개: stale-warn · inp-reuse-suggest · integrity-sync · context-pack-stale · worktree-env-symlink)
- /sprint 3 phase 워크플로우 → plan · qa · ship 단일 명령. 옛 6단계는 plan의 RESEARCH.md 자동 기록과 ship의 RETRO.md 자동 기록으로 흡수, 이월 옵션 mechanism 차단으로 출시 후 응대 사이클 안정성 사전 확보
- 4중 SSOT(SPRINT.md · Linear Cycle · Git · CHANGELOG) → 출시 후 사용자 신고 시 단일 진실 원천으로 상태 파악 가능한 동선 사전 구축
- 부서·에이전트 분리 + context-map 자동 라우팅 (신규 매칭) → 7개 부서(design · dev · docs · marketing · ops · product · qa) + 9개 에이전트(ceo · frontend/backend/qa-engineer · product-manager · ui-ux-designer · marketing-strategist · ops-engineer · knowledge-logger)별 CLAUDE.md + docs lifecycle 분리. `RULES/context-map.md` + `SYSTEM/schemas/code-doc-mapping.yaml`로 task_type 6종과 코드 path glob을 must-read doc에 자동 매핑, CEO → 워커 위임 시 합집합 5개 내외 doc만 prompt에 첨부 → 출시 후 사용자 신고 응대 시 LLM 응답 정확도·속도 사전 확보
- 오프라인-퍼스트 캐시 (신규 매칭) → IndexedDB 우선 저장 + Pending Operations 큐(`sync-engine.ts` MAX_RETRIES = 5) Supabase Write-Behind 동기화 + Realtime 멀티 디바이스 통합 → 출시 후 카페·지하철 환경 응대 대상 사전 제거
- MV3 ↔ Web 인증 통합 보안 (신규 매칭) → `bridge.ts` ALLOWED_ORIGINS 화이트리스트로 postMessage origin 검증 (`SECURITY_POLICY.md §8`)

Gap:
- 외부 고객사 대상 0-1 도입 사례 → mindgraph는 1인 자체 솔루션이라 직접 매칭 없음 (가장 큰 Gap, 룰 A에 따라 사례를 만들기 전 본문에 기록 불가)
- LLM 호출 단위 관측성 (Langfuse · OpenLLMetry · OpenTelemetry GenAI semantic convention) → Sentry · PostHog · OpenTelemetry SDK는 도입됐으나 LLM 호출 attribute(model · prompt_tokens · cost_usd) 표준화 미확인
- 후속 LLM API 호출 어댑터 (AI SDK · BAML · Mastra) → 캡처는 4 LLM 동작하나 사용자 후속 질문용 LLM API 호출 통합 어댑터 미확인
- MCP 서버화 → mindgraph 지식 그래프를 외부 Claude · Cursor에서 도구로 호출하는 MCP 서버 미확인
- E2E 오프라인 자동 검증 → Pending Ops 큐는 구현됐으나 Playwright 기반 네트워크 차단 시나리오 자동 회귀 미확인
- SemVer · 릴리즈노트 자동 발행 → `/sprint ship`이 git tag · CHANGELOG는 생성하나 GitHub Releases 자동 노트 연동 미확인

## 3. 업그레이드 후보

### 1. LLM 호출 관측성 레이어
- **무엇**: 4개 LLM API 호출 단위로 비용·토큰·실패율·지연을 기록하는 관측성 레이어. OpenTelemetry log exporter 위에 LLM 전용 attribute(model·prompt_tokens·completion_tokens·cost_usd) 표준화.
- **왜**: zighang FDE 우대 빈출 "Langfuse 등 LLM 관측성 도구로 프로덕션 LLM 시스템을 운영해 본 경험" 직접 매칭. 4개 LLM 멀티 벤더라 비교 가시성 자산.
- **주요 파일**: `department/dev/web/instrumentation.ts`, `department/dev/web/lib/` 안에 신규 `llm-telemetry.ts`
- **도입 난이도**: M (OpenTelemetry SDK 이미 도입, log attribute 표준화만)
- **우대 키워드 매핑**: "LLM API를 활용해 프로덕션 시스템", "LLM 관측성 도구"

### 2. 비기술 사용자 온보딩 흐름 + 응대 화면
- **무엇**: 첫 사용자 진입 시 캡처 데모를 3단계로 보여주는 온보딩. api/feedback·api/error-log·Sentry feedback에 들어올 문의를 한곳에 모아 보는 운영 화면(`app/admin/` 또는 별도 admin 라우트).
- **왜**: zighang FDE 자격 빈출 "비기술 청중에게 복잡한 기술 개념을 설명"·"프로토타이핑·데모·고객 워크숍" 매칭. 출시 후 1인이 응대까지 책임지는 동선 사전 구축.
- **주요 파일**: `department/dev/web/app/(onboarding)/` 라우트 신규, `department/dev/web/app/admin/` 신규
- **도입 난이도**: M (Sentry feedback · api/feedback 라우트 이미 존재)
- **우대 키워드 매핑**: "비기술 청중", "프로토타이핑·데모·고객 워크숍", "1인 개발로 서비스를 론칭해 운영"

### 3. LLM 통합 라이브러리 (Vercel AI SDK 또는 BAML) 적용
- **무엇**: 현재 4개 LLM은 캡처 대상 DOM이지 직접 API 호출은 없음. 사용자가 captured 응답에 후속 질문을 던지는 기능을 만들 때 Vercel AI SDK로 통합 호출 레이어 도입.
- **왜**: zighang FDE 우대 "BAML, AI SDK, Mastra 등을 활용해 LLM 에이전트나 통합 시스템을 빠르게 만들어 본 경험" 직접 매칭.
- **주요 파일**: `department/dev/web/lib/llm/` 신규, `department/dev/web/app/api/chat/`
- **도입 난이도**: M
- **우대 키워드 매핑**: "BAML, AI SDK, Mastra"

### 4. 오프라인-우선 쓰기 동기화 E2E 테스트
- **무엇**: Playwright로 네트워크 차단 상태에서 노드 캡처·복귀 시 자동 flush를 검증하는 E2E 시나리오. 현재 단위 테스트는 있으나 오프라인 시나리오 자동화 흔적 미확인.
- **왜**: zighang FDE 자격 빈출 "프로덕션 코드를 직접 작성하고 운영"·"모던 웹 스택으로 빠르게 통합 시스템" 매칭. 운영 신뢰도 증거.
- **주요 파일**: `department/dev/web/e2e/` 신규 시나리오, `department/dev/web/playwright.config.ts`
- **도입 난이도**: S (Playwright 이미 도입)
- **우대 키워드 매핑**: "프로덕션 코드를 직접 작성하고 운영"

### 5. 외부 고객사 도입 케이스 1건 기록
- **무엇**: 지인·소규모 팀·동호회 등 외부 사용자 1팀에 mindgraph를 배포·온보딩·피드백 수집·반영까지 한 사이클을 기록한 case study 문서.
- **왜**: zighang FDE 우대 빈출 "엔터프라이즈 고객을 대상으로 0-1 도입을 주도해 본 경험" 약화 매칭. mindgraph가 1인 자체 서비스라 외부 도입 사례 부재가 가장 큰 Gap.
- **주요 파일**: `mindgraph/docs/case-studies/<group>.md` 신규
- **도입 난이도**: L (외부 고객 확보·온보딩·피드백 수집 사이클 자체 소요)
- **우대 키워드 매핑**: "엔터프라이즈 고객을 대상으로 0-1 도입", "고객 대면 기술 역할"
- **주의**: 사실이 아닌 사례 기록은 룰 A 위반. 실제 외부 도입 1건을 만든 뒤에만 본문에 기록 가능.

### 6. MCP 서버로 mindgraph 자체 노출
- **무엇**: 자신의 mindgraph 지식 그래프를 외부 Claude·Cursor에서 MCP 도구로 호출할 수 있는 MCP 서버 구현. 노드 검색·자식 조회·새 캡처 트리거를 MCP tool로 노출.
- **왜**: zighang FDE 자격에서 직접 등장 빈도는 낮지만, Anthropic FDE 공고가 MCP를 시그니처 키워드로 사용. mindgraph가 LLM 데이터 자산 도구라 MCP 서버화의 자연스러운 후보.
- **주요 파일**: `mindgraph/mcp-server/` 신규 패키지 (Node 또는 Python)
- **도입 난이도**: M

### 7. SemVer·릴리즈노트 자동 생성 정착
- **무엇**: 현재 `/sprint ship` 단계가 CHANGELOG·Git tag를 생성하지만, GitHub Releases와 연동된 자동 릴리즈노트 발행 흐름 추가.
- **왜**: 1인 운영의 출시 안정성을 외부에 보여주는 가시 자산. zighang FDE 자격 "출시 가능한 형태까지 끌고 가실 수 있는 분" 매칭.
- **주요 파일**: `.claude/hooks/`, `.github/workflows/release.yml` 신규
- **도입 난이도**: S

## 4. 우선순위

1. **4번 (오프라인 E2E)** — Playwright 이미 도입, 비용 가장 낮음, 운영 신뢰도 직접 증거
2. **1번 (LLM 관측성)** — OpenTelemetry SDK 이미 도입, Langfuse 키워드 매칭 강함
3. **2번 (비기술 온보딩 + 응대)** — Sentry feedback 활용해 즉시 가시화 가능
4. **6번 (MCP 서버)** — Anthropic 시그니처 키워드, 글로벌 FDE 매칭에 유효
5. **3번 (AI SDK 통합)** — 후속 질문 기능과 묶어 한 번에
6. **7번 (자동 릴리즈)** — 단순하지만 효과 가시성 작음
7. **5번 (외부 도입 사례)** — 가장 무겁고 시간 소요 큼

## 5. 안 하는 것 (의도적 제외)

- **LLM 양자화 (Quantization-Aware Training, Post-Training Quantization)** — zighang FDE 우대 빈출이나 NPU·PyTorch·GPU 인프라 부담 큼, mindgraph 도메인과 거리 멀음
- **SIP·VoIP·WebRTC 텔레포니** — 음성 AI 에이전트 우대 항목이나 mindgraph는 텍스트 도메인, 별도 프로젝트(Fit)에서 매칭하는 편이 적합
- **Top-tier AI/ML 학회 논문** — 우대이나 시간·연구 인프라 부담 매우 큼
- **콜센터·CCaaS 통합** — 도메인 매칭 없음
