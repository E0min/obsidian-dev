---
type: jd-analysis
job: AI-Native-Builder
created: 2026-05-23
sample_size: 6
sample_kr: 5
sample_global: 1
---

# 03. AI-Native Builder (AI·LLM Engineer)

이 문서의 키워드·문장은 `companies/` 안 6건의 공고 원문에서 직접 인용했습니다. 한국 5건(한국딥러닝·AI Works·웨이커·아미쿠스렉스·그래파이), 글로벌 1건(Anthropic Applied AI).

"AI-Native Builder"는 한국 시장 직무명으로 사용되지 않습니다. 가장 가까운 명칭은 "AI 엔지니어 / LLM 엔지니어 / NLP 엔지니어". 사용자가 정의한 AI-Native Builder의 책임(AI 워크플로우 자동화, Hooks, MCP, SDD, 에이전트 도구체인)은 한국 공고에서 부분적으로 보이고, 가장 명확하게 일치하는 것은 Anthropic Applied AI Engineer.

## 1. 직무 정의 — 공고 원문 인용

### KR

- 한국딥러닝: "Vision/LLM/RAG 최신 연구 동향 파악 후 Custom Backbone/Head 설계" + "비정형 대규모 데이터 전처리 및 RAG 파이프라인 구축" (`companies/rallit-koreadeep-ai.md:25-26`)
- AI Works: "AI 기반 NLP, 멀티모달 서비스 개발" + "LLM 기반 AI 서비스 개발" + "AI 데이터셋 자동 가공 모듈 개발" (`companies/wanted-aiworks-nlp-llm.md:23-26`)
- 웨이커: "고품질 명령 지침(Instruction)데이터셋 구축 협업" + "LLM 평가 및 Task 품질 평가 파이프라인 개발" (`companies/wanted-waker-llm.md:21-23`)
- 아미쿠스렉스: "법률문서 유즈케이스에 맞는 프롬프트·템플릿 설계" + "RAG 질의 템플릿 설계 및 근거 추적 로직 구현" (`companies/wanted-amicuslex-llm.md:23-24`)
- 그래파이: "멀티모달 모델 기반 RAG 파이프라인 설계 및 성능 최적화" + "멀티에이전트 기반 LLM 시스템 연구 및 개발" (`companies/wanted-graphi-llm.md:23-27`)

### GLOBAL

- Anthropic Applied AI: "Develop reusable infrastructure: MCP servers, benchmarks, agent skills" + "Identify deployment challenges and provide feedback to product teams" (`companies/greenhouse-anthropic-applied-ai.md:24-25`)

핵심 분리:
- **KR 5건은 LLM/RAG 파이프라인 구축**에 집중 (모델 학습·파인튜닝·평가)
- **GLOBAL은 재사용 가능 인프라(MCP·benchmark·agent skill) 산출**에 집중

이 차이가 "AI 엔지니어 ≠ AI-Native Builder"임을 보여줍니다. AI-Native Builder는 후자에 가깝습니다.

## 2. 필수 자격요건 빈도 (6건 기준)

| 키워드 | KR (n=5) | GLOBAL (n=1) | 총 (n=6) |
|--------|----------|--------------|----------|
| LLM API·LLM 모델 활용 | 5 | 1 | 6 |
| Python | 4 | 0 (Python은 우대 표기) | 4 |
| RAG 파이프라인 설계·구현 | 4 | 0 | 4 |
| Prompt Engineering | 3 | 1 (prompt engineering이 광범위 LLM 경험에 포함) | 4 |
| PyTorch · Tensorflow · 딥러닝 프레임워크 | 2 | 0 | 2 |
| Vector DB (Faiss·Milvus·Weaviate 등) | 2 | 0 | 2 |
| 멀티모달 · Vision + LLM | 2 | 0 | 2 |
| LLM 평가 프레임워크 · 평가 파이프라인 | 2 | 1 | 3 |
| MCP server · agent skills 등 재사용 인프라 산출 | 0 | 1 | 1 |
| 도메인 지식(법률·life sciences 등) | 1 | 1 | 2 |
| 3년 이상 경력 | 1 | 1 (4+) | 2 |
| 신입~5년 가능 (낮은 진입장벽) | 3 | 0 | 3 |

핵심 발견:
- **공통 6건 일치**: LLM 활용 + Prompt Engineering — 2축이 AI 엔지니어의 베이스라인.
- **KR 특화**: RAG 파이프라인·Vector DB·PyTorch·모델 학습 측면이 강함 — ML 엔지니어 + LLM 통합 색채.
- **GLOBAL 특화**: MCP server·agent skills·benchmark 같은 **재사용 가능 인프라 산출**이 직무 핵심. 한국 어느 공고에도 MCP/agent skills를 본문에 명시한 곳 없음.

## 3. 우대 사항 빈도 (6건 기준)

| 키워드 | KR (n=5) | GLOBAL (n=1) | 총 |
|--------|----------|--------------|----|
| 논문·특허·오픈소스 기여 | 1 | 0 | 1 |
| ONNX·TensorRT·Quantization·vllm 추론 최적화 | 1 | 0 | 1 |
| Vector DB 구축 경험 | 1 | 0 | 1 |
| 모델 경량화·Inference Optimization | 1 | 0 | 1 |
| 협업 툴(Git·Notion·Jira·DVC) | 1 | 0 | 1 |
| 학술적 기술 깊이 | 0 | 1 | 1 |
| 도메인 배경(genomics·neuroscience·drug discovery) | 0 | 1 | 1 |
| Multi-hat scrappy 마인드 | 0 | 1 | 1 |

KR 우대 사항은 한국딥러닝 1건에 집중. 다른 KR 공고는 "확인 못함".

## 4. 회사별 차이점

| 회사 | 강조 책임 | 차별 키워드 |
|------|-----------|-------------|
| 한국딥러닝 | Vision/LLM/RAG 연구·custom 모델 설계·추론 최적화 | ONNX, TensorRT, vllm |
| AI Works | NLP·멀티모달 서비스 개발, 데이터셋 자동 가공 | Huggingface Transformers |
| 웨이커 | Instruction 데이터셋 + Multi-Task LLM 평가 파이프라인 | FastAPI, Kafka |
| 아미쿠스렉스 | 법률 LLM/Prompt/RAG 설계, 근거 추적 | 법률 도메인 협업 |
| 그래파이 | 멀티모달 RAG + 멀티에이전트 LLM 시스템 연구 | Vector DB + Graph DB |
| Anthropic Applied AI | 재사용 인프라(MCP·benchmark·agent skill) 산출, 도메인 파트너 협업 | Claude, MCP servers |

같은 직무명이지만:
- 한국 AI 엔지니어 = **모델·파이프라인·인프라 빌더** 위주
- Anthropic Applied AI = **고객 자산(MCP·agent skills) 산출자** — 직무 분류상 FDE와 인접

## 5. 사용자 4개 프로젝트와 매칭

| 프로젝트 | AI-Native Builder 키워드 매칭 | 검증된 근거 |
|----------|----------------------------|------------|
| **mindgraph** | LLM API 활용·다중 AI 통합·9개 훅·6단계 /sprint·SDD·MCP/agent skills 인접 자산·재사용 워크플로우 | `refs/mindgraph/.claude/hooks/`, `refs/mindgraph/.claude/skills/sprint/SKILL.md`, `content/resume/AI-Native-Builder/mindgraph_이력서.md` |
| chatGraph | LLM 응답 통합·Vitest 회귀 테스트(LLM 통신 경로) | `content/resume/AI-Native-Builder/chatGraph_이력서.md` |
| Fit | (직접 매칭 없음 — WebRTC·STOMP 도메인) | - |
| xAB | (간접) 인증 게이트·실시간 구독 핸들 — AI 직접 적용 X | - |

**AI-Native Builder 적합 강도**: mindgraph ◎◎ (Anthropic Applied AI/FDE의 산출물 정의 — MCP·agent skills·재사용 인프라가 사용자의 9개 훅·sprint·4중 SSOT와 1:1 대응) → chatGraph △ → Fit/xAB ×.

## 6. 한국 시장 진입 전략

- 한국 공고에서 "AI-Native Builder" 그대로 매칭되는 직무는 없음. 가장 가까운 한국 직무명은 **AI 엔지니어 / LLM 엔지니어**.
- 다만 사용자의 mindgraph 운영 경험(9개 훅·sprint·4중 SSOT)은 한국 공고들이 요구하는 키워드와는 부분적으로만 매칭(LLM 활용·Prompt Engineering·RAG는 강하지만 PyTorch·모델 학습은 약함).
- **권장 전략**: 한국에서는 LLM 엔지니어 공고에 지원하되, 모델 학습·RAG 부분은 약점이므로 mindgraph의 sprint·hooks 운영 자산을 차별점으로 강조. 또는 글로벌(Anthropic Applied AI 등) 공고 직접 지원.

## 7. 출처 URL

- KR 한국딥러닝: <https://www.rallit.com/positions/3793>
- KR AI Works: <https://www.wanted.co.kr/wd/210245>
- KR 웨이커: <https://www.wanted.co.kr/wd/251780>
- KR 아미쿠스렉스: <https://www.wanted.co.kr/wd/315289>
- KR 그래파이: <https://www.wanted.co.kr/wd/301601>
- GLOBAL Anthropic Applied AI: <https://job-boards.greenhouse.io/anthropic/jobs/5111942008>

## 8. 표본 한계 명시

- "AI-Native Builder" 직무명 부재. 한국은 LLM·NLP·RAG 엔지니어 공고로 대체 분석.
- KR 5건 중 2건(웨이커 2025-02 만료, 한국딥러닝 2025-09 만료)은 3개월 윈도우 밖 보조 자료. 활성 공고만 보면 한국 표본 3건.
- 이스트소프트·바이트사이즈·LG전자·마키나락스 등 검색에서 잡힌 공고들은 봇 차단(blindhire ECONNREFUSED, greetinghr 403) 또는 정보 누락(jobkorea 바이트사이즈는 required 등 확인 못함)으로 미수집.

## 9. zighang.com 보강 표본 (2026-05-25 수집, 30건)

기존 표본(3건)의 한계를 해소하기 위해 zighang.com API에서 직무 매칭 공고 30건을 수집했습니다.
수집 결과 원본은 `companies/zighang-AI-Native-Builder-*.md`에 박제했습니다.

### 9.1 수집 메타

- **수집 일자**: 2026-05-25
- **수집 채널**: zighang.com API `api.zighang.com/api/recruitments/v3`
- **검색 쿼리**: `keyword=LLM`
- **한국 시장 전체 규모**: 440건 (해당 쿼리 기준)
- **본 분석 표본 수**: 30건 (ZIGHANG_SCORE 상위 30건)

### 9.2 기술 키워드 빈도 (30건 중 N건에서 언급)

| 키워드 | 등장 공고 수 | 비율 |
|--------|--------------|------|
| LLM | 27 | 90% |
| Agent | 15 | 50% |
| Python | 13 | 43% |
| RAG | 13 | 43% |
| 프롬프트 | 12 | 40% |
| 에이전트 | 9 | 30% |
| LangChain | 7 | 23% |
| OpenAI | 7 | 23% |
| PyTorch | 7 | 23% |
| Kubernetes | 6 | 20% |
| fine-tuning | 6 | 20% |
| vector | 6 | 20% |
| Llama | 5 | 17% |
| FastAPI | 4 | 13% |
| AWS | 4 | 13% |
| Azure | 4 | 13% |
| Docker | 4 | 13% |
| LangGraph | 4 | 13% |
| GCP | 3 | 10% |
| Anthropic | 3 | 10% |

### 9.3 한국어 핵심어 빈도

| 키워드 | 등장 공고 수 | 비율 |
|--------|--------------|------|
| AI | 26 | 87% |
| 데이터 | 17 | 57% |
| 성능 | 16 | 53% |
| 최적화 | 15 | 50% |
| 협업 | 13 | 43% |
| 글로벌 | 11 | 37% |
| 성능 최적화 | 7 | 23% |
| 재택 | 7 | 23% |
| 커뮤니케이션 | 6 | 20% |
| 고객 | 6 | 20% |
| 주도적 | 6 | 20% |
| 원격 | 5 | 17% |
| 테스트 | 5 | 17% |
| 머신러닝 | 5 | 17% |
| 딥러닝 | 5 | 17% |
| 백엔드 | 4 | 13% |
| 현장 | 4 | 13% |
| 스타트업 | 4 | 13% |
| 추천 | 4 | 13% |

### 9.4 회사 분포 (상위 10)

- 메크랩(3)
- 42dot(2)
- 베이비챗(2)
- 이자(2)
- 에이아이웍스(2)
- 씨어스(1)
- 인피닉(1)
- 지신(1)
- 나니아랩스(1)
- 엔닷라이트(1)

### 9.5 경력 분포

- 1~3년: 21건
- 4~6년: 5건
- 신입~3년: 3건
- 7년+: 1건

### 9.6 지역 분포 (상위 5)

- 서울: 19건
- 경기: 9건
- 기타: 2건

### 9.7 본 직무의 차별 소구점 (zighang 30건 표본 기준)

4 직무 표본을 비교했을 때 AI-Native-Builder만 두드러진 키워드는 다음과 같습니다.

| 키워드 | AI 빈도 | 타 직무 비교 |
|--------|---------|--------------|
| LLM | 27 | FE: 4 · AI: 27 · PE: 9 · FDE: 18 |
| RAG | 13 | FE: 0 · AI: 13 · PE: 3 · FDE: 9 |
| PyTorch | 7 | FE: 0 · AI: 7 · PE: 2 · FDE: 5 |
| fine-tuning | 6 | FE: 0 · AI: 6 · PE: 1 · FDE: 2 |
| vector | 6 | FE: 0 · AI: 6 · PE: 0 · FDE: 0 |

**해석**: LLM(27/30 = 90%), RAG(13/30), fine-tuning(6/30), vector(6/30), PyTorch(7/30)가 AI 표본에 집중. PE/FDE에도 LLM은 등장하지만 fine-tuning·vector는 거의 AI 표본 전용. "LLM 학습·추론 파이프라인을 깊이 다룬다"는 게 차별점.
