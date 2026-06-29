---
type: method
created: 2026-05-23
updated: 2026-05-23
---

# 00. 수집 방법·룰·키워드

## 목적

4개 직무(FDE, Product-Engineer, AI-Native-Builder, FE)의 한국·글로벌 채용공고를 표준 형식으로 수집해 직무별 주안점·키워드 빈도를 근거 자료로 박제한다. 이력서·포트폴리오 톤 재정렬과 target-companies 선정의 1차 입력 자료가 된다.

## 룰 (claude.md 최우선 룰 A·B 준수)

- **룰 A**: 추정·의역·일반 지식 서술 금지. 공고 원문에 적힌 표현만 인용. 출처 URL 필수.
- **룰 B**: 모호어 사용 금지(`다양한 / 여러 / 효율적 / 쾌적한 / 원활한 / 적극 / 선제 / 유연하게 / 능숙 / 풍부한 / 뛰어난 / 체계적 / 안정적인 / 편리한 / 손쉽게 / 최적화 / 개선`). 모든 수치는 N/총 + 근거 파일 경로 인용.

## 수집 범위 (사용자 결정)

- 활성 + 최근 만료(~3개월) 공고. 게시일 또는 만료일이 2026-02-23 이후이면 포함.
- 한국 8개 사이트 + 글로벌 5개사 careers 보조.
- 직무당 30건 이상(총 120+건), 글로벌 직무당 5~10건.

## 사이트 목록

| 사이트 | URL | 비고 |
|--------|-----|------|
| 원티드 | wanted.co.kr | IT 스타트업·테크 |
| 사람인 | saramin.co.kr | 전 업종 범용 |
| 잡코리아 | jobkorea.co.kr | 전 업종 범용 |
| 직행 | zighang.com | 개발자 특화 |
| 로켓펀치 | rocketpunch.com | 스타트업 |
| 프로그래머스 | career.programmers.co.kr | 개발자 특화 |
| 점핏 | jumpit.co.kr | 개발자 특화 |
| 랠릿 | rallit.com | 스타트업·디자인·개발 |

글로벌 careers (보조):

- Anthropic (anthropic.com/careers)
- Palantir (palantir.com/careers)
- OpenAI (openai.com/careers)
- Linear (linear.app/careers)
- Vercel (vercel.com/careers)

## 키워드 매트릭스

| 직무 | 한국어 키워드 | 영문 키워드 | 보조 키워드 |
|------|---------------|-------------|-------------|
| FDE | "Forward Deployed Engineer", "포워드 디플로이드", "AI 솔루션 엔지니어", "AI 솔루션 아키텍트" | Forward Deployed Engineer, AI Solutions Engineer, Customer Engineer | 컨설팅 + 엔지니어, on-site engineer |
| Product-Engineer | "프로덕트 엔지니어", "프로덕트 개발자", "프로덕트 개발" | Product Engineer | 풀스택 + 제품, 그로스 엔지니어 |
| AI-Native-Builder | "AI 엔지니어", "LLM 엔지니어", "AI 개발자", "에이전트 엔지니어" | AI Engineer, LLM Engineer, Agent Engineer | Claude Code, MCP, RAG, prompt engineering |
| FE | "프론트엔드 개발자", "프론트엔드 엔지니어", "Frontend" | Frontend Engineer, Senior Frontend, Staff Frontend | Next.js, React, TypeScript |

## WebFetch 표준 프롬프트 (모든 공고 수집에 동일 적용)

```
이 채용공고에서 다음만 추출해줘. 추정·의역 금지. 공고에 없는 것은 "없음"이라고 적어줘.
모호어("다양한 / 여러 / 효율적 / ...")는 원문에 있더라도 그대로 인용하되 인용임을 표시.

- company: 회사명
- title: 공고 제목
- region: KR 또는 GLOBAL
- posted_at: 게시일 (없으면 "확인 못함")
- expires_at: 만료일 (없으면 "확인 못함")
- url: 원본 URL
- required: [필수 자격요건 항목들. 공고에 적힌 표현 그대로 bullet 단위]
- preferred: [우대 사항 항목들. 동일 형식]
- responsibilities: [주요 업무 항목들. 동일 형식]
- tech_stack: [언급된 기술 스택 키워드만]
- years: [요구 경력 연차 표현]
```

## companies/ 파일 형식

각 공고는 `companies/{site}-{회사슬러그}-{직무슬러그}.md` 1건. 예:

```yaml
---
company: 토스
title: Senior Frontend Engineer
region: KR
posted_at: 2026-04-10
expires_at: 2026-06-30
url: https://toss.im/career/senior-frontend
fetched_at: 2026-05-23
job: FE
---

## required
- 5년 이상 프론트엔드 개발 경험
- TypeScript 실무 경험
- ...

## preferred
- Next.js App Router 경험
- ...

## responsibilities
- ...

## tech_stack
- TypeScript, React, Next.js, ...

## years
- 5년 이상
```

## 진행 상황 로그

| 단계 | 상태 | 일시 |
|------|------|------|
| vault 디렉토리 생성 | 완료 | 2026-05-23 |
| 00-method.md 작성 | 완료 | 2026-05-23 |
| WebSearch 32회 (한국) | 진행 예정 | - |
| WebSearch 글로벌 보조 | 진행 예정 | - |
| WebFetch 120+건 | 진행 예정 | - |
| 직무별 분석 파일 4개 | 진행 예정 | - |
| matrix·MOC·INDEX | 진행 예정 | - |
| 모호어 검증 | 진행 예정 | - |
