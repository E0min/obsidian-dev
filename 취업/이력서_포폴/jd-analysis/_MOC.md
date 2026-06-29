---
type: MOC
created: 2026-05-23
---

# JD Analysis — Map of Content

4개 직무(FDE, Product-Engineer, AI-Native-Builder, FE) 채용공고 분석 산출물의 진입점.

## 진행 상태 (2026-05-23 기준)

| 단계 | 상태 |
|------|------|
| 수집 방법·룰 박제 | [[00-method]] 완료 |
| WebSearch 한국 8 사이트 + 글로벌 5사 | 완료 (50회 미달, 12회로 종료 — 봇 차단 사이트 다수) |
| WebFetch 공고 원문 | 완료 (18건 박제, 목표 120건 미달) |
| 직무별 분석 4건 | [[01-FDE]] [[02-Product-Engineer]] [[03-AI-Native-Builder]] [[04-FE]] 완료 |
| 키워드 × 프로젝트 매트릭스 | [[matrix]] 완료 |
| 후속: 이력서 톤 재정렬·target-companies | 미진행 |

## 핵심 산출물

- [[00-method]] — 수집 방법, 룰, 키워드, 표준 프롬프트 템플릿
- [[01-FDE]] — Forward Deployed Engineer 분석 (n=3: KR 2 + GLOBAL 1)
- [[02-Product-Engineer]] — Product Engineer 분석 (n=4: KR 3 + GLOBAL 1)
- [[03-AI-Native-Builder]] — AI-Native Builder (한국명: AI/LLM 엔지니어) 분석 (n=6: KR 5 + GLOBAL 1)
- [[04-FE]] — Frontend Engineer 분석 (n=5: KR 5)
- [[matrix]] — 4 직무 × 키워드 × 사용자 4 프로젝트 매핑

## companies/ (원문 박제)

- 18건. 각 파일은 frontmatter(company/title/region/posted_at/expires_at/url/fetched_at/job) + 본문(required/preferred/responsibilities/tech_stack/years) 표준 형식.
- 직무 분포: FDE 3, PE 4, AIN 6, FE 5
- 지역 분포: KR 15, GLOBAL 3

## 분석 결과 한 줄 요약 (직무별)

- **FDE**: LLM 활용 + 고객 문제 정의 + 비개발 직군 협업 + 독립 수행이 4축. 한국에선 채널톡·와이큐가 Claude Code/Cursor 활용을 필수로 명시.
- **PE**: 풀스택 + React/TS + 제품 라이프사이클 단일 책임 3축. 한국에선 "Product Engineer" 직무명보단 "풀스택 엔지니어" 명칭이 다수.
- **AI-Native Builder**: 한국 표본은 LLM·RAG·PyTorch 중심 ML 엔지니어 색채. 글로벌(Anthropic Applied AI)은 MCP·agent skills 같은 재사용 인프라 산출 중심.
- **FE**: React 5/5, TypeScript 4/5, Next.js 4/5. 시니어 기준 5년 이상 경력 다수.

## 사용자 4 프로젝트 적합도 한 줄 요약

- **mindgraph**: FDE ◎ · PE ◎ · AIN ◎◎ · FE ◎ — 4 직무 모두에 강한 카드. 핵심 자산은 9개 훅·6단계 /sprint·4중 SSOT·Claude Code 운영.
- **chatGraph**: FE ◎ · PE ◎ · AIN △ · FDE △ — FE·PE에 강함.
- **Fit**: FE ◎ · PE ○ — FE 정통.
- **xAB**: FE ◎ · PE ○ — App Router 패턴 깊이.

## 표본 한계

- 사용자 목표 120건 대비 실제 18건 수집. 한국 채용 사이트(catch.co.kr·greetinghr·blindhire)의 봇 차단으로 fetch 실패 다수. 빈도 통계의 통계적 신뢰도는 제한적.
- 후속 세션에서 표본 보강 시 다음 직무가 우선: FDE(글로벌 추가), FE(글로벌 추가), Product-Engineer(토스·당근·라이너 개별 공고).

## 다음 단계 후보

- [ ] 이력서·포트폴리오 톤 재정렬 (`content/resume/**`, `content/portfolio/**`)
- [ ] `target-companies.md` 신규 작성 (4 직무별 우선 지원 회사 5~10곳)
- [ ] 약점 영역(RAG·Vector DB·PyTorch·MCP 직접 산출) 사용자 확인 후 학습 계획
- [ ] 추가 채용 공고 표본 보강 (직무당 30+건 목표)
