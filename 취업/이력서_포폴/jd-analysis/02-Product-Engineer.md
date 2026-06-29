---
type: jd-analysis
job: Product-Engineer
created: 2026-05-23
sample_size: 4
sample_kr: 3
sample_global: 1
---

# 02. Product Engineer

이 문서의 키워드·문장은 `companies/` 안 4건의 공고 원문에서 직접 인용했습니다. 한국 3건(알고케어·삼양식품·완드), 글로벌 1건(Linear).

한국 시장에서 "Product Engineer"라는 직무명을 그대로 쓰는 공고는 알고케어 1건. 삼양식품·완드는 "풀스택 엔지니어" 명칭이지만 책임 범위(기획→출시→반복 개선, 사용자 지표 기반 우선순위)가 Linear의 PE 정의와 일치해 함께 분석.

## 1. 직무 정의 — 공고 원문 인용

### KR

- 알고케어: "B2B·B2C 제품의 백엔드 서버 개발 및 운영" + "기획자·디자이너·운영팀과 협업하며 제품 문제 정의 및 해결" (`companies/wanted-algocare-pe.md:23-26`)
- 삼양식품: "React (Next.js)를 기반으로 기획부터 출시, 반복 개선까지 주도하거나 깊이 관여" + "사용자 지표 기반 기능 우선순위 설정과 반복 개발" (`companies/wanted-samyang-fullstack-pe.md:14, 25`)
- 완드: "Django REST API 설계/구현" + "React + TypeScript 화면 개발" + "E2E·단위 테스트 작성" (`companies/wanted-wand-fullstack-pe.md:25-29`)

### GLOBAL

- Linear: "5+ years building customer-facing products" + "track record of driving complex, end-to-end features with visible product impact" + "product sensibility regarding UX, speed, and polish" (`companies/linear-product-engineer.md:14, 16`)

공통 패턴: **풀스택 + 사용자 지표 기반 우선순위 + 출시까지 단일 책임**.

## 2. 필수 자격요건 빈도 (4건 기준)

| 키워드 | KR (n=3) | GLOBAL (n=1) | 총 (n=4) |
|--------|----------|--------------|----------|
| 풀스택(프론트+백엔드) 또는 양쪽 협업 경험 | 3 | 1 | 4 |
| React + TypeScript 사용 | 2 | 1 | 3 |
| 제품 라이프사이클(기획→출시→개선) 직접 참여 | 2 | 1 | 3 |
| Next.js 사용 | 2 | 0 | 2 |
| 사용자 지표·UX·우선순위 판단 | 1 | 1 | 2 |
| AI 코딩 에이전트(Cursor/Claude Code/Copilot) 활용 | 2 | 0 | 2 |
| LLM·AI Agent API 활용 | 1 | 1 | 2 |
| 클라우드 환경(AWS/GCP/Azure) 배포 | 2 | 0 | 2 |
| Supabase·BaaS 백엔드 연동 | 1 | 0 | 1 |
| GraphQL·Temporal·PostgreSQL | 0 | 1 | 1 |
| 3년 이상 경력 (최소 연차) | 3 | 0 | 3 |
| 5년 이상 경력 (최소 연차) | 0 | 1 | 1 |
| 6년 이상 경력 (최소 연차) | 1 | 0 | 1 |

핵심 발견:
- **공통 4건 일치**: 풀스택 경험 + React/TypeScript + 제품 라이프사이클 직접 참여 — 3축이 PE의 핵심 정의.
- **KR 특화**: AI 코딩 에이전트 활용을 PE 필수로 명시한 사례 다수(알고케어·삼양식품). 클라우드 배포 경험 강조.
- **GLOBAL 특화**: Linear는 Temporal·GraphQL·MobX 등 자사 스택 학습 의지 강조. UX/속도/polish의 제품 감각을 별도 항목으로.

## 3. 우대 사항 빈도 (4건 기준)

| 키워드 | KR (n=3) | GLOBAL (n=1) | 총 |
|--------|----------|--------------|----|
| 빠른 학습 능력·기술 학습 의지 | 1 | 0 | 1 |
| 외부 리소스·다른 팀과의 협업 조율 | 1 | 0 | 1 |
| 기술 아키텍처 설계 경험 | 1 | 0 | 1 |
| 테스트 가능한 코드(원문 "깔끔한 모듈화") | 1 | 0 | 1 |
| Remote/async-first 환경 적응 | 0 | 1 | 1 |
| Temporal·GraphQL·MobX·styled-components | 0 | 1 | 1 |

KR은 우대 사항이 공고별로 빈약(알고케어 1건, 완드 4건, 삼양식품 2건).

## 4. 회사별 차이점

| 회사 | 강조 책임 | 차별 키워드 |
|------|-----------|-------------|
| 알고케어 | B2B·B2C 백엔드 + AI Agent API 통합 | LLM 기반 AI Agent 실무 적용 필수 |
| 삼양식품 | 글로벌 콘텐츠 플랫폼 React/Next.js + Supabase + 사용자 지표 우선순위 | Cursor·Claude Code·NotebookLM 활용 필수(원문 표현 "능숙"), 미국 사용자 대상 운영 |
| 완드 | Django + React/TypeScript 풀스택, 검색·로그 통계 | TanStack Query/Router, Vite, AWS S3 Presign |
| Linear | React/TS 풀스택 + 실시간 협업·AI 기능 + 성능 | Temporal, GraphQL, PostgreSQL, MobX 자사 스택 |

같은 PE라도:
- 한국 일반: **풀스택 + AI 도구 활용 + 단일 제품 라이프사이클**
- Linear: **고품질 제품 감각 + 자사 스택 깊이 + AI 기능 통합**

## 5. 사용자 4개 프로젝트와 매칭

| 프로젝트 | PE 키워드 매칭 | 검증된 근거 |
|----------|-----------------|------------|
| **mindgraph** | 1인 운영·기획→출시→개선 단일 책임, AI 코딩 에이전트 활용, Supabase 백엔드 | `content/resume/Product-Engineer/mindgraph_이력서.md` (사용자 데이터 신뢰성 중심), `refs/mindgraph/department/dev/web/lib/storage/` (Write-Behind) |
| **chatGraph** | React/TypeScript 풀스택, Optimistic UX, 사용자 흐름(빈 화면 제거), Vitest 회귀 | `content/resume/Product-Engineer/chatGraph_이력서.md` (UX 우선 정렬) |
| **Fit** | React 풀스택, 사용자 가치(저지연 청취), 인원 쏠림 표시 등 사용자 흐름 | `content/resume/Product-Engineer/Fit_이력서.md` |
| **xAB** | Next.js App Router 풀스택, 사용자 시나리오(피드 맥락 유지·실시간 동기화) | `content/resume/Product-Engineer/xab_이력서.md` |

**PE 적합 강도**: mindgraph ◎ (1인 운영 = PE 정의 그대로) → chatGraph ◎ (UX·회귀 테스트) → xAB ○ (사용자 흐름) → Fit ○ (현장 UX).

## 6. 한국 시장 진입 전략

- 한국에서 "Product Engineer" 직무명을 직접 쓰는 회사는 제한적 — 알고케어 1건만 확인. 대다수는 "풀스택 엔지니어" 또는 "프로덕트 개발자"로 채용.
- 삼양식품 공고 본문에 "Cursor, Claude Code, NotebookLM 등 AI 도구 능숙 사용"이 필수 자격요건으로 명시(원문 인용, `companies/wanted-samyang-fullstack-pe.md:20`) — 사용자의 mindgraph 운영 경험과 직접 매칭.
- 글로벌 Linear급 회사를 노리려면: React/TypeScript 풀스택 깊이 + 사용자 지표 기반 의사결정 경험을 이력서 본문에 더 강조 필요.

## 7. 출처 URL

- KR 알고케어: <https://www.wanted.co.kr/wd/290226>
- KR 삼양식품: <https://www.wanted.co.kr/wd/295999>
- KR 완드: <https://www.wanted.co.kr/wd/317705>
- GLOBAL Linear: <https://linear.app/careers/069c4628-88d7-4e4d-b393-c996fc7f3076>

## 8. 표본 한계 명시

- "Product Engineer" 직무명 한국 표본 부족(1건). "풀스택 엔지니어" 명칭으로 PE 책임을 채우는 공고를 함께 집계함을 명시.
- 토스(`toss.im/career/jobs`)·당근(`about.daangn.com/jobs/`)·라이너(`liner.com/careers`) careers 목록 페이지는 fetch했으나 개별 공고 상세까지는 미진입.
- Vercel(`vercel.com/careers/product-engineer-v0-5466858004`)은 목록 페이지로 표시되어 상세 추출 실패.

## 9. zighang.com 보강 표본 (2026-05-25 수집, 30건)

기존 표본(3건)의 한계를 해소하기 위해 zighang.com API에서 직무 매칭 공고 30건을 수집했습니다.
수집 결과 원본은 `companies/zighang-Product-Engineer-*.md`에 박제했습니다.

### 9.1 수집 메타

- **수집 일자**: 2026-05-25
- **수집 채널**: zighang.com API `api.zighang.com/api/recruitments/v3`
- **검색 쿼리**: `keyword=Product Engineer`
- **한국 시장 전체 규모**: 91건 (해당 쿼리 기준)
- **본 분석 표본 수**: 30건 (ZIGHANG_SCORE 상위 30건)

### 9.2 기술 키워드 빈도 (30건 중 N건에서 언급)

| 키워드 | 등장 공고 수 | 비율 |
|--------|--------------|------|
| TypeScript | 16 | 53% |
| Claude | 15 | 50% |
| React | 14 | 47% |
| AWS | 13 | 43% |
| Git | 11 | 37% |
| Python | 9 | 30% |
| PostgreSQL | 9 | 30% |
| LLM | 9 | 30% |
| Next.js | 8 | 27% |
| Docker | 8 | 27% |
| Java | 7 | 23% |
| Node.js | 7 | 23% |
| 에이전트 | 7 | 23% |
| Agent | 6 | 20% |
| JavaScript | 5 | 17% |
| Go | 5 | 17% |
| Spring | 5 | 17% |
| Django | 5 | 17% |
| REST | 5 | 17% |
| FastAPI | 4 | 13% |
| MySQL | 4 | 13% |
| Redis | 4 | 13% |
| GCP | 4 | 13% |
| Gemini | 4 | 13% |
| CI/CD | 4 | 13% |

### 9.3 한국어 핵심어 빈도

| 키워드 | 등장 공고 수 | 비율 |
|--------|--------------|------|
| AI | 24 | 80% |
| 데이터 | 18 | 60% |
| 협업 | 15 | 50% |
| 고객 | 15 | 50% |
| 백엔드 | 14 | 47% |
| 프론트엔드 | 12 | 40% |
| 주도적 | 12 | 40% |
| 성능 | 10 | 33% |
| 최적화 | 10 | 33% |
| 테스트 | 10 | 33% |
| 프로덕트 | 9 | 30% |
| 스타트업 | 8 | 27% |
| 글로벌 | 8 | 27% |
| 풀스택 | 6 | 20% |
| 성능 최적화 | 5 | 17% |
| 커뮤니케이션 | 5 | 17% |
| 현장 | 4 | 13% |
| 오너십 | 4 | 13% |
| 재택 | 3 | 10% |

### 9.4 회사 분포 (상위 10)

- 메라키플레이스(2)
- 당근서비스(2)
- 피트(2)
- 로위랩코리아(1)
- 플랜핏(1)
- 플렉스(1)
- 하이퍼노바(HYPERNOVA)(1)
- 쏘카(SOCAR)(1)
- 뭉클 (mnkl.)(1)
- 우주에이엠에프(1)

### 9.5 경력 분포

- 1~3년: 17건
- 신입~3년: 7건
- 4~6년: 4건
- 7년+: 2건

### 9.6 지역 분포 (상위 5)

- 서울: 26건
- 경기: 3건
- 기타: 1건

### 9.7 본 직무의 차별 소구점 (zighang 30건 표본 기준)

4 직무 표본을 비교했을 때 Product Engineer만 두드러진 키워드는 다음과 같습니다.

| 키워드 | PE 빈도 | 타 직무 비교 |
|--------|---------|--------------|
| Claude | 15 | FE: 1 · AI: 1 · PE: 15 · FDE: 5 |
| 프로덕트 | 9 | FE: 0 · AI: 1 · PE: 9 · FDE: 5 |
| 풀스택 | 6 | FE: 0 · AI: 1 · PE: 6 · FDE: 6 |
| 스타트업 | 8 | FE: 1 · AI: 4 · PE: 8 · FDE: 5 |

**해석**: Claude(15/30) 명시는 PE 표본의 특이점. 타 직무 표본에서 Claude 명시 빈도는 0~5건. "AI 코딩 도구 활용 능력 + 풀스택 + 스타트업 환경 + 고객 중심 프로덕트 사고"가 PE의 차별 소구점.
