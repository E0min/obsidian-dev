---
type: upgrade-guide
job: AI-Native-Builder
target_project: mindgraph
based_on: zighang ai native + builder 합본 74건 + matrix.md
created: 2026-05-26
last_updated: 2026-06-03
---

# AI-Native Builder 관점 mindgraph 업그레이드 로드맵

## 1. 직무 핵심 빈출 자격·우대 (zighang AIN 74건 합본 Top 6)

- 컨텍스트 엔지니어링·하네스 엔지니어링·에이전트 환경 설계 (사용자 자산과 정확 매칭) — `requirements/AI-Native-Builder.md`
- 직접 만들고 검증하는 빌더 정신
- 빠른 의사결정·실행
- "무엇을 할지 / 무엇을 버릴지" 판단
- 영역 무관 1년 이상의 치열한 업무 경험
- (우대) 자기 힘으로 높은 허들을 넘어 본 경험·세상을 변화시킨 경험 (Antler·Amazon 어조)

추가 우대 빈출: RAG·임베딩 추천, 검색 품질 정량 지표(recall@k·mAP·nDCG), Langfuse 등 LLM 관측성, Structured Output·Tool Calling, 한국어 특화 LLM 활용.

> 표본 교체 이력: 2026-05-30 LLM Engineer 30건 → AI Native + Builder 74건. 컨텍스트·하네스·에이전트 환경 키워드가 mindgraph 자산과 1:1 대응되어 시그니처 매칭이 강해짐.

## 2. mindgraph 현재 자산 매칭 (matrix.md §4 인용, 2026-05-28~29 시스템 재편 반영)

매칭됨:
- 4 LLM API 통합 표면 → `department/dev/src/content/detector.ts` SELECTORS 상수에 ChatGPT·Gemini·Grok·Claude DOM 선택자 모음 + hostname 자동 감지
- 컨텍스트 엔지니어링 5층 영속화 → Conversation · Memory · CLAUDE.md · Hook · Skill 5층 분산
- 하네스 엔지니어링 9개 훅 → `.claude/hooks/` 차단 게이트 4개(spec-gate · linear-done-gate · build-pr-block · inp-cycle-guard) + 보조 알림 5개(stale-warn · inp-reuse-suggest · integrity-sync · context-pack-stale · worktree-env-symlink)
- 에이전트 환경 설계 → 9개 에이전트(ceo · frontend/backend/qa-engineer · product-manager · ui-ux-designer · marketing-strategist · ops-engineer · knowledge-logger) + 7개 부서(design · dev · docs · marketing · ops · product · qa) 분리
- 컨텍스트 자동 라우팅 → `RULES/context-map.md` + `SYSTEM/schemas/code-doc-mapping.yaml` task_type 6종 · 코드 path glob → must-read doc 자동 매핑, CEO → 워커 위임 시 합집합 5개 내외만 prompt에 첨부
- /sprint 3 phase 워크플로우 → plan(Linear Cycle · SPRINT.md · RESEARCH.md 자동 기록) · qa(미완료 INP 강제 결정, 이월 옵션 mechanism 차단) · ship(git tag · CHANGELOG · RETRO.md 자동 기록). 옛 6단계는 plan의 RESEARCH.md 자동 기록과 ship의 RETRO.md 자동 기록으로 흡수
- 4중 SSOT → SPRINT.md · Linear Cycle · Git · CHANGELOG
- 권위 계층 L1~L4 → L1 Canonical Principles(RULES/principles/ + RULES/decisions/ + PRD) · L2 Domain SSOT(department/{team}/docs/active/) + Operational Playbook(RULES/playbooks/ + RULES/templates/) · L3 Cycle Records(department/docs/artifacts/sprints/v{X.Y}/) · L4 Generated Cache(RULES/generated/)
- 신규 5 skill → `/feature-contract` · `/adr-record` · `/review-swarm` · `/context-pack-regen` · `/cycle-brief` (2026-05-28 AI 네이티브 재편)

Gap:
- RAG 임베딩 파이프라인 → `lib/auto-link/embedding-trigger.ts` + `embed-client.ts` + Supabase Edge Function `functions/embed` + pgvector 저장 + `lib/auto-link/related-nodes.ts` 코사인 유사도 top-K + `lib/auto-link/backfill.ts` 일괄 임베딩 — 코드 미구현(2026-06-03 확인)
- 풀텍스트 + 임베딩 통합 검색 → `lib/search/fulltext-index.ts` + `lib/search/index.ts` 양쪽 결과 머지 + `lib/search/highlight.ts` — 코드 미구현(2026-06-03 확인)
- 추천 정확도 정량 측정 → `lib/telemetry.ts`의 AccuracyEvent(`hitInTop3` 자동 계산, H1 가설 top-3 ≥ 60%) + InteractionEvent(click · ignore · hide, H3 가설 sidebar 클릭률 ≥ 60%) — 코드 미구현(2026-06-03 확인)
- LLM 호출 관측성 (Langfuse · OpenTelemetry GenAI semantic convention) → Sentry · PostHog · OpenTelemetry SDK는 도입됐으나 LLM 호출 단위 attribute(model · prompt_tokens · completion_tokens · cost_usd) 표준화 미확인
- Structured Output · Tool Calling LLM API 활용 → 코드 미확인
- 검색 품질 추가 지표 (recall@k · MRR · nDCG) → AccuracyEvent·InteractionEvent 기반 H1/H3는 있으나 평가 셋 기반 recall@k · MRR 자동 측정 미확인
- 다중 LLM API 직접 호출 (후속 질문·요약) → 캡처는 4 LLM 동작하나 후속 LLM API 호출 어댑터 미확인
- 한국어 특화 LLM (HyperCLOVA X · Solar) → 코드 미확인
- 프롬프트 SemVer 버전 관리 → 프롬프트는 5층 영속화로 분산 관리되나 호출별 prompt_version 메타 미확인
- Python 기반 AI 개발 · PyTorch · TensorFlow · 모델 학습 · 파인튜닝 → mindgraph는 TypeScript 풀스택 (의도적 제외 — §5 참조)

## 3. 업그레이드 후보

> 2026-06-03 미구현 확인. RAG 임베딩 추천·H1/H3 정량 측정·풀텍스트+임베딩 통합 검색 3건은 Gap에 그대로 두고 §3 업그레이드 후보로 우선순위 상향.

### 1. LLM 호출 관측성 (Langfuse 또는 OpenTelemetry GenAI semantic convention)
- **무엇**: 임베딩 호출(`functions/embed`)과 향후 후속 질문·요약 LLM API 호출을 Langfuse 또는 OpenTelemetry GenAI semantic convention attribute(model · prompt_tokens · completion_tokens · cost_usd)로 추적. 프롬프트·응답·토큰·비용을 시간별·모델별로 비교.
- **왜**: zighang AIN 우대 빈출 "LLM 관측성"·"Langfuse" + FDE 가이드 1번과 공통 후보.
- **주요 파일**: `department/dev/web/instrumentation.ts`, `department/dev/web/lib/llm/telemetry.ts` 신규
- **도입 난이도**: S (OpenTelemetry SDK 이미 도입)
- **우대 키워드 매핑**: "LLM 관측성", "운영 환경 이슈 모니터링·QA 체계"
- **메모**: RAG 임베딩 파이프라인 자체가 미구현 상태이므로 임베딩 자체 구축이 선결.

### 2. 검색 품질 평가 셋 자동 측정 (recall@k · MRR)
- **무엇**: 직접 작성한 평가 셋(질문 30~50개 + 정답 노드 ID)을 기준으로 검색 결과 상위 k에 정답이 포함되는 비율(recall@k)과 평균 역순위(MRR)를 자동 측정. 임베딩 모델 교체 시 평가 점수 변화를 SPRINT.md에 박는다. 현재 H1·H3는 사용자 클릭 기반 운영 측정이므로 출시 전에는 평가 셋 기반 측정이 보완재.
- **왜**: zighang AIN 우대 빈출 "검색 품질을 정량적 지표 기반으로 측정하고 개선(recall@k · mAP · nDCG)" 직접 매칭. 출시 전 임베딩 모델 의사결정 근거.
- **주요 파일**: `department/dev/web/scripts/eval-search.ts` 신규, `department/dev/web/__evals__/dataset.json`
- **도입 난이도**: M
- **우대 키워드 매핑**: "검색 품질을 정량적 지표 기반으로 측정"
- **메모**: RAG 임베딩 파이프라인 자체가 미구현 상태이므로 임베딩 자체 구축이 선결.

### 3. Structured Output · Tool Calling으로 노드 자동 분류
- **무엇**: 캡처한 LLM 답변을 LLM에게 한 번 더 통과시켜 (Claude · GPT) Structured Output 형식(JSON schema)으로 카테고리·키워드·요약을 추출해 UnifiedNode 메타데이터에 저장. Tool Calling으로 검색·태깅·요약 도구 호출.
- **왜**: zighang AIN 자격 빈출 "Structured Output · Tool Calling 등 LLM API 기능을 실제 기능 구현에 활용해 본 경험" 직접 매칭.
- **주요 파일**: `department/dev/web/lib/llm/structured.ts` 신규, `department/dev/web/supabase/migrations/<n>_node_metadata.sql`
- **도입 난이도**: M
- **우대 키워드 매핑**: "Structured Output · Tool Calling 등 LLM API 기능"

### 4. 다중 LLM API 통합 표면 — 캡처에서 API 호출로 확장
- **무엇**: 현재 4개 LLM은 DOM 캡처 대상이지 직접 API 호출은 없음. `detector.ts` SELECTORS 상수와 동등한 위치에 LLM API client 어댑터(OpenAI · Anthropic · Google · xAI)를 두고 사용자가 후속 질문을 던지면 같은 LLM 모델로 API 라우팅.
- **왜**: zighang AIN 자격 "프롬프트 설계와 컨텍스트 구성"·"하나의 LLM 모델을 처음부터 끝까지 책임지고 고도화"에 부분 매칭. 4 LLM 통합 표면을 캡처에서 API 호출로 확장하면 detector.ts 통합 사례의 가치가 두 배.
- **주요 파일**: `department/dev/web/lib/llm/clients/` 신규, `department/dev/web/app/api/chat/`
- **도입 난이도**: M

### 5. 프롬프트 SemVer 버전 관리
- **무엇**: 현재 5층 영속화에 분산된 프롬프트(CLAUDE.md · Hook · Skill)에 `prompts/<task>.md` 디렉토리로 SemVer를 부여하고, 각 LLM 호출 메타에 사용된 prompt_version 기록. 4번 LLM API 어댑터·1번 관측성 레이어와 함께 호출별 추적 가능.
- **왜**: zighang AIN 우대 "프롬프트 템플릿화" + AI 네이티브 운영 신뢰도 시그널.
- **주요 파일**: `mindgraph/prompts/` 신규
- **도입 난이도**: S

### 6. 한국어 특화 LLM 옵션
- **무엇**: 4번 어댑터 위에 HyperCLOVA X · Solar 같은 한국어 특화 LLM 호출 옵션 추가. 한국어 사용자가 한국어 답변을 받을 때 모델 선택 가능.
- **왜**: zighang AIN 우대 "한국어 특화 LLM 또는 국내 모델 활용 경험" 직접 매칭. 한국 채용 시장 시그니처 키워드.
- **주요 파일**: `department/dev/web/lib/llm/clients/hyperclova.ts` 신규
- **도입 난이도**: S~M (API 키 발급·호출 어댑터)

### 7. 자체 하네스(9훅·3 phase·context-map) 외부 사용 가능 형태 추출
- **무엇**: `.claude/hooks/` 10개, `.claude/skills/{sprint,feature-contract,adr-record,review-swarm,context-pack-regen,cycle-brief}/`, `RULES/context-map.md` + `SYSTEM/schemas/code-doc-mapping.yaml`를 npm 패키지 또는 별도 저장소로 추출해 다른 1인 개발자가 설치·사용 가능하게 만들기. README · 설치 가이드 · 예제 포함.
- **왜**: zighang AIN 시그니처 키워드 "컨텍스트 엔지니어링 · 하네스 엔지니어링 · 에이전트 환경 설계"의 외부 검증 가능 자산화. Antler·Amazon 어조 우대 "세상을 변화시킨 경험"과도 매칭.
- **주요 파일**: `mindgraph/.claude/` + `RULES/` 일부 추출 → 신규 저장소 또는 `packages/harness-kit/`
- **도입 난이도**: M~L (코드 추출 · 일반화 · 문서화)
- **우대 키워드 매핑**: "컨텍스트 엔지니어링", "하네스 엔지니어링", "에이전트 환경 설계"

## 4. 우선순위

1. **1번 (LLM 관측성)** — OpenTelemetry SDK 이미 도입, 가장 가벼우면서 운영 신뢰도 시그널 강함
2. **2번 (recall@k · MRR 평가)** — 출시 전 임베딩 모델 결정 근거, 이미 구현된 telemetry와 보완재
3. **3번 (Structured Output · Tool Calling)** — 임베딩 추천 품질을 메타데이터 측에서 끌어올림
4. **4번 (LLM API 어댑터)** — 후속 질문 기능 도입과 묶어, detector.ts 통합 사례 두 배 가치
5. **5번 (프롬프트 SemVer)** — 1번·4번 도입 후 호출 추적 완성
6. **7번 (하네스 외부 추출)** — AIN 시그니처, 시간 소요 크나 외부 검증 가능
7. **6번 (한국어 LLM)** — 4번 이후 한국 채용 시장 시그널 부여

## 5. 안 하는 것 (의도적 제외)

- **PyTorch · TensorFlow 모델 학습** — zighang AIN 자격에 등장하나 GPU 인프라 부담 큼, mindgraph 도메인과 거리 멀음
- **Custom Backbone · LLM 파인튜닝** — 우대 빈출이나 학습 데이터 확보·GPU 운영 비용 부담 큼
- **Top-tier AI 학회 논문** — 시간 비용 큼, 본 가이드 범위 밖
- **Vector DB 교체 (Faiss · Milvus · Weaviate)** — pgvector로 출시 전 1인 프로토타입 단계에 충분, 교체 필요성 없음
- **금융 공시 데이터(SEC · DART) 처리** — 도메인 특화 우대, mindgraph 변경 범위 큼
- **자율주행 · 컴퓨터비전 · 음성 AI** — 도메인 매칭 없음
