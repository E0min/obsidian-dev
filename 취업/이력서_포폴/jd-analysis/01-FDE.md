---
type: jd-analysis
job: FDE
created: 2026-05-23
sample_size: 3
sample_kr: 2
sample_global: 1
---

# 01. Forward Deployed Engineer (FDE)

이 문서의 모든 키워드·문장은 `companies/` 디렉토리 안 3건의 공고 원문에서 직접 인용했습니다. 한국 시장은 표본 2건(채널톡, 와이큐), 글로벌 1건(Anthropic)으로 분리 집계했습니다.

## 1. 직무 정의 — 공고 원문 인용

### KR

- 채널톡(Channel.io): "discover, design, and implement AX (AI Transformation) projects" + "diagnose actual customer problems and design solutions rapidly" (`companies/lever-channelio-fde.md:21-22`)
- 와이큐(PROPER MARKET): "AI 기반 업무 자동화 및 최대화 프로젝트 수행" + "자동화 결과물의 운영 안정화 및 현업 이관 지원" (`companies/wanted-wiq-fde.md:23-29`)

### GLOBAL

- Anthropic: "embed directly with their most strategic customers to drive transformational AI adoption" + "build production applications with Claude models in customer systems" + "deliver technical artifacts: MCP servers, sub-agents, agent skills" (`companies/greenhouse-anthropic-fde.md:24-26`)

세 공고가 공통적으로 명시한 행위: **고객 문제 직접 정의 → AI 솔루션 설계·구현 → 운영 이관·재사용 자산화**.

## 2. 필수 자격요건 빈도 (3건 기준)

| 키워드 | KR (n=2) | GLOBAL (n=1) | 총 (n=3) |
|--------|----------|--------------|----------|
| LLM·AI API 활용 경험 (OpenAI/Anthropic/Claude 등) | 2 | 1 | 3 |
| 고객·비즈니스 문제를 기술 솔루션으로 번역 | 2 | 1 | 3 |
| 비개발·사업 직군과의 커뮤니케이션 | 2 | 1 | 3 |
| 문제 정의부터 구현·운영까지 단독 수행 | 2 | 1 | 3 |
| 코딩 에이전트(Claude Code/Cursor/Codex/Antigravity) 활용 | 2 | 0 | 2 |
| Production LLM 경험 (prompt·agent·eval·deploy 시스템) | 0 | 1 | 1 |
| Python (필수 언어 명시) | 0 | 1 | 1 |
| 3년 이상 customer-facing 기술직 경력 | 0 | 1 | 1 |

핵심 발견:
- **공통 3건 일치**: LLM 활용 / 고객 문제 정의 / 비개발 직군 협업 / 독립 수행 — 4축이 FDE의 정의를 구성.
- **KR 특화**: AI 코딩 에이전트(Claude Code 등) 활용 명시. 와이큐·채널톡 둘 다 "AI Native 개발" 또는 "ALF AI agent" 언급.
- **GLOBAL 특화**: Anthropic은 Production LLM 시스템(prompt engineering, agent dev, eval framework, deployment)을 명시 — 한국 공고보다 시스템 깊이 강조.

## 3. 우대 사항 빈도 (3건 기준)

| 키워드 | KR (n=2) | GLOBAL (n=1) | 총 |
|--------|----------|--------------|----|
| 직접 고객 응대(consulting·professional services) 경험 | 1 | 1 | 2 |
| 비즈니스 감각·고객 중심 사고 | 1 | 1 | 2 |
| 기술 창업자(technical founder) 경험 | 0 | 1 | 1 |
| 금융·헬스케어·엔터프라이즈 도메인 | 0 | 1 | 1 |
| 군 병역특례 가능 (산업·전문연구요원) | 1 | 0 | 1 |

KR 우대 사항은 공고마다 빈약(와이큐는 "확인 못함"). GLOBAL은 도메인 전문성·창업 경험을 명시.

## 4. 회사별 차이점

| 회사 | 강조 책임 | 차별 키워드 |
|------|-----------|-------------|
| 채널톡 | AX(AI Transformation) 컨설팅·구현, 영업·CS·제품 협업 | ALF AI agent (자체) |
| 와이큐 | 사내 업무 자동화 PoC·운영 이관, 전사 AI 교육 | Creative Tool, 다중 AI 도구 활용 |
| Anthropic | 전략 고객 사이트에 임베드, MCP·sub-agent·agent skills 자산 산출 | 25% 출장, Claude 모델, 엔터프라이즈 |

같은 직무명이지만 책임 범위가 다름:
- 채널톡·와이큐: **인하우스 AI 적용** 중심 (자사 제품·자사 운영에 AI 적용)
- Anthropic: **외부 전략 고객 임베드** 중심 (모델 공급사가 고객사로 파견)

## 5. 사용자 4개 프로젝트와 매칭

근거 자료: `~/obsidian/Dev/Projects/취업/이력서_포폴/content/resume/FDE/*.md`, `pdf-generator/refs/mindgraph/`

| 프로젝트 | FDE 키워드 매칭 | 검증된 근거 |
|----------|-----------------|------------|
| **mindgraph** | LLM/AI API 활용, AI Native 코딩 에이전트, PO 관점 단독 수행, MCP·sub-agent·agent skills 인접 자산 | 9개 훅 + 6단계 /sprint(`refs/mindgraph/.claude/skills/sprint/SKILL.md`), Claude Code 기반 운영, 1인 운영·실서비스 배포 |
| chatGraph | LLM 응답 클라이언트 통합, Optimistic 라우팅 | 본문 `content/resume/FDE/chatGraph_이력서.md`. AI Transformation 컨설팅·MCP 자산은 직접 매칭 없음 |
| Fit | (매칭 없음) | WebRTC·STOMP·실시간 오디오. AI 도메인 아님 |
| xAB | (매칭 없음) | SNS·Realtime DB. AI 직접 적용 X |

**FDE 적합 강도**: mindgraph ◎ (Anthropic 명시 자산 MCP/sub-agent/agent skills와 사용자의 9개 훅·SDD·4중 SSOT 운영 자산이 1:1 대응) → chatGraph △ → Fit/xAB ×.

## 6. 한국 시장 진입 전략

3건 표본 한계 안에서 다음만 사실로 확인:

- **채널톡은 시니어 가능** (`주니어 to 시니어` 명시, `companies/lever-channelio-fde.md:36`)
- **와이큐는 신입~경력 8년** (와이큐 `companies/wanted-wiq-fde.md:43`) — 신입에도 열려 있음
- **두 회사 모두 Claude Code·Cursor 등 코딩 에이전트 활용 능력을 필수 요건으로 명시** — 사용자의 mindgraph 운영 경험과 직접 매칭

## 7. 출처 URL

- KR 채널톡: <https://channel.io/en/careers/905bc3bd-d788-4d17-b463-ae23b6a910b2>
- KR 와이큐: <https://www.wanted.co.kr/wd/354048>
- GLOBAL Anthropic: <https://job-boards.greenhouse.io/anthropic/jobs/4985877008>

## 8. 표본 한계 명시

- 한국 FDE 직무명을 직접 사용하는 공고가 적음(3개월 윈도우 안에서 채널톡·와이큐 2건 + 만료 공고 다수). 표본 부족으로 빈도 통계의 신뢰도는 제한적.
- 글로벌은 Anthropic만 1건. Palantir lever 페이지는 HTTP 403으로 fetch 실패(`url-pool.md` 참고).
- 향후 추가 수집 후보(이번 세션에는 미수집): 스캐터엑스·마키나락스·크래프톤 한국 FDE, OpenAI 글로벌 FDE.

## 9. zighang.com 보강 표본 (2026-05-25 수집, 30건)

기존 표본(3건)의 한계를 해소하기 위해 zighang.com API에서 직무 매칭 공고 30건을 수집했습니다.
수집 결과 원본은 `companies/zighang-FDE-*.md`에 박제했습니다.

### 9.1 수집 메타

- **수집 일자**: 2026-05-25
- **수집 채널**: zighang.com API `api.zighang.com/api/recruitments/v3`
- **검색 쿼리**: `keyword=Forward Deployed`
- **한국 시장 전체 규모**: 45건 (해당 쿼리 기준)
- **본 분석 표본 수**: 30건 (ZIGHANG_SCORE 상위 30건)

### 9.2 기술 키워드 빈도 (30건 중 N건에서 언급)

| 키워드 | 등장 공고 수 | 비율 |
|--------|--------------|------|
| LLM | 18 | 60% |
| Python | 12 | 40% |
| 에이전트 | 12 | 40% |
| Docker | 10 | 33% |
| RAG | 9 | 30% |
| Agent | 9 | 30% |
| Kubernetes | 8 | 27% |
| REST | 6 | 20% |
| Linux | 6 | 20% |
| LangChain | 5 | 17% |
| Claude | 5 | 17% |
| PyTorch | 5 | 17% |
| AWS | 4 | 13% |
| Llama | 4 | 13% |
| 프롬프트 | 4 | 13% |
| Git | 4 | 13% |
| Go | 3 | 10% |
| FastAPI | 3 | 10% |
| MLOps | 3 | 10% |
| CI/CD | 3 | 10% |

### 9.3 한국어 핵심어 빈도

| 키워드 | 등장 공고 수 | 비율 |
|--------|--------------|------|
| AI | 26 | 87% |
| 현장 | 20 | 67% |
| 고객 | 19 | 63% |
| 데이터 | 17 | 57% |
| 협업 | 16 | 53% |
| 커뮤니케이션 | 12 | 40% |
| 성능 | 10 | 33% |
| 최적화 | 10 | 33% |
| 백엔드 | 8 | 27% |
| 글로벌 | 8 | 27% |
| 코드 리뷰 | 8 | 27% |
| 풀스택 | 6 | 20% |
| 주도적 | 6 | 20% |
| 프로덕트 | 5 | 17% |
| 스타트업 | 5 | 17% |
| 테스트 | 4 | 13% |
| 딥러닝 | 4 | 13% |
| 성능 최적화 | 3 | 10% |
| 원격 | 3 | 10% |
| 재택 | 3 | 10% |

### 9.4 회사 분포 (상위 10)

- 마키나락스(7)
- 포트로직스(2)
- 센드버드(2)
- 한국딥러닝(2)
- 리얼월드(2)
- vox.ai(2)
- 카야(1)
- 리벨리온(1)
- 홀리데이로보틱스(1)
- 주식회사 에임인텔리전스(1)

### 9.5 경력 분포

- 1~3년: 16건
- 신입~3년: 8건
- 4~6년: 6건

### 9.6 지역 분포 (상위 5)

- 서울: 23건
- 경기: 4건
- 부산: 1건
- 해외: 1건
- 경남: 1건

### 9.7 본 직무의 차별 소구점 (zighang 30건 표본 기준)

4 직무 표본을 비교했을 때 FDE만 두드러진 키워드는 다음과 같습니다.

| 키워드 | FDE 빈도 | 타 직무 비교 |
|--------|---------|--------------|
| 현장 | 20 | FE: 2 · AI: 4 · PE: 4 · FDE: 20 |
| 고객 | 19 | FE: 5 · AI: 6 · PE: 15 · FDE: 19 |
| 커뮤니케이션 | 12 | FE: 10 · AI: 6 · PE: 5 · FDE: 12 |
| 에이전트(한글) | 12 | FE: 1 · AI: 9 · PE: 7 |

**해석**: 현장(20/30)·고객(19/30)은 FDE 표본에서만 65%+ 빈도. 다른 직무는 모두 한 자리수. "기술 + 출장·대면 컨설팅"이 FDE의 직무 정의에 박힌 차별점.
