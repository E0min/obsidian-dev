---
type: matrix
created: 2026-05-23
sample_total: 18
---

# 직무 × 키워드 × 사용자 프로젝트 매트릭스

이 매트릭스의 모든 평가는 `companies/` 18건 공고 원문과 `~/obsidian/Dev/Projects/취업/이력서_포폴/content/resume/**` 본문, `pdf-generator/refs/mindgraph/` 실코드 기반 검증. 추정·일반화 없음.

## 1. 직무별 빈도 상위 키워드 (표본 18건 통합)

| 키워드 | FDE n=3 | PE n=4 | AIN n=6 | FE n=5 | 합 |
|--------|---------|--------|---------|--------|----|
| React | 0 | 3 | 0 | 5 | 8 |
| TypeScript | 0 | 2 | 0 | 4 | 6 |
| Next.js | 0 | 2 | 0 | 4 | 6 |
| Python | 1 | 1 | 4 | 0 | 6 |
| LLM API 활용 (OpenAI/Anthropic/Claude) | 3 | 2 | 6 | 0 | 11 |
| Prompt Engineering | 2 | 0 | 4 | 0 | 6 |
| RAG 파이프라인 | 0 | 0 | 4 | 0 | 4 |
| AI 코딩 에이전트 (Cursor/Claude Code/Codex) | 2 | 2 | 0 | 0 | 4 |
| MCP server·agent skills·sub-agents | 1 | 0 | 1 | 0 | 2 |
| 고객 문제 정의·번역 | 3 | 1 | 0 | 0 | 4 |
| 비개발 직군 협업 | 3 | 1 | 0 | 0 | 4 |
| 풀스택 (FE+BE) | 0 | 4 | 0 | 1 (데브게이트) | 5 |
| 사용자 지표 우선순위·UX 감각 | 0 | 2 | 0 | 1 | 3 |
| Vitest/Jest 테스트 | 0 | 1 | 0 | 1 | 2 |
| SSR 처리 경험 | 0 | 0 | 0 | 4 | 4 |
| 디자인 시스템·웹 접근성 | 0 | 0 | 0 | 3 | 3 |
| PyTorch·Tensorflow | 0 | 0 | 2 | 0 | 2 |
| Vector DB (Faiss·Milvus·Weaviate) | 0 | 0 | 2 | 0 | 2 |

핵심 패턴:
- **LLM API 활용**: FDE·PE·AIN 3개 직무에 걸쳐 11/18 등장. 가장 광범위한 키워드.
- **AI 코딩 에이전트**: FDE+PE 한국 공고에서 4건. 사용자 mindgraph의 Claude Code 운영 경험과 정확 매칭.
- **MCP·agent skills**: 단 2건(Anthropic FDE + Anthropic Applied AI)만 명시. 글로벌 Anthropic 특화 키워드.
- **React + TypeScript + Next.js 3종 세트**: FE 4/5, PE 2/4. 한국 시장 FE·PE의 기본기.

## 2. 사용자 4 프로젝트의 직무 적합도 (검증된 근거 기반)

| 프로젝트 | FDE | PE | AIN | FE | 강한 근거 |
|----------|-----|----|----|----|------|
| **mindgraph** | ◎ | ◎ | ◎◎ | ◎ | 9개 훅·6단계 /sprint·4중 SSOT (`refs/mindgraph/.claude/skills/sprint/SKILL.md`), Claude Code 운영, 실서비스 배포 |
| **chatGraph** | △ | ◎ | △ | ◎ | Feature-First, 843→355 책임 분리, useSuspenseQuery, Vitest 회귀 (`content/resume/FE/chatGraph_이력서.md`) |
| **Fit** | × | ○ | × | ◎ | WebRTC RTCPeerConnection, STOMP, IntersectionObserver, redux-persist whitelist (`content/resume/Fit_이력서.md`) |
| **xAB** | × | ○ | × | ◎ | Next.js App Router 병렬·인터셉팅 라우트, useInfiniteQuery, Supabase Realtime, @supabase/ssr 미들웨어 (`content/resume/xab_이력서.md`) |

표기 기준:
- ◎◎ = 직무 핵심 자산(MCP·agent skills 같은 시그니처 키워드)과 사용자 프로젝트가 1:1 대응
- ◎ = 다수 키워드(3건 이상)에서 직접 매칭
- ○ = 부분 매칭 또는 인접 책임 일치
- △ = 단편적 매칭
- × = 직접 매칭 없음

## 3. 직무별 사용자의 강한 카드와 약한 카드

### FDE
- **강한 카드**: mindgraph 1인 운영 + Claude Code 워크플로우 + sprint·hooks·SSOT 운영 자산
- **약한 카드**: 외부 고객사 임베드 경험·MCP 직접 산출 경험·B2B AI 컨설팅 이력 (사용자 코드 기반 확인 못함 → 룰 A에 따라 본문에 쓰지 않음)
- **사용자에게 확인 필요**: chatGraph가 외부 고객사 운영이었는지, B2B AX 프로젝트 경험이 있는지

### PE
- **강한 카드**: 4프로젝트 모두 React/TypeScript/Next.js 풀스택 + 사용자 흐름 중심 의사결정(chatGraph Optimistic·xAB 모달 라우팅) + 1인 운영 라이프사이클(mindgraph)
- **약한 카드**: GraphQL·Temporal·Postgres 같은 Linear 자사 스택 깊이는 본문 근거에서 확인 못함
- **사용자에게 확인 필요**: GraphQL·PostgreSQL 실무 경험 정도

### AIN
- **강한 카드**: mindgraph가 한국 LLM 엔지니어 공고 + Anthropic Applied AI 공고 책임의 교집합을 ◎◎로 충족
- **약한 카드**: 한국 LLM 엔지니어 공고가 요구하는 PyTorch 모델 학습·Custom Backbone·RAG Vector DB 구축은 본문 근거에서 확인 못함
- **사용자에게 확인 필요**: PyTorch/Vector DB/모델 파인튜닝 실무 경험 정도. mindgraph의 RAG·Vector DB 사용 흔적은 코드 검증 시 미확인(`graph-params.ts`·`pending-ops.ts` 등 비-LLM 자료구조 코드 위주).

### FE
- **강한 카드**: 4프로젝트 모두 한국 FE 시니어 공고의 필수 키워드(React/TS/Next/SSR/디자인 시스템 인접/접근성) 매칭. 라이프사이클 깊이·App Router 패턴·D3+SSR 격리·Suspense 경계 등 시니어급 토픽 풍부.
- **약한 카드**: 표본 공고의 5년 이상 경력 요건과 사용자 경력 매칭은 본 분석에서 확인하지 않음 (사용자에게 확인 필요).
- **사용자에게 확인 필요**: 시니어 FE 5년 요건 대비 실제 경력 햇수.

## 4. 키워드별 사용자 코드 매칭 표 (룰 A 출처 검증)

| 공고 빈출 키워드 | 사용자 프로젝트 근거 | 검증 위치 |
|------------------|----------------------|----------|
| LLM API 활용 (OpenAI/Anthropic) | mindgraph 4개 AI 통합 detector.ts | `refs/mindgraph/department/dev/src/content/detector.ts:25` |
| Claude Code 운영 워크플로우 | mindgraph 9개 훅 + 6단계 /sprint | `refs/mindgraph/.claude/hooks/`, `refs/mindgraph/.claude/skills/sprint/SKILL.md` |
| MCP server / agent skills | mindgraph SDD + sprint = agent skills 패턴 | `refs/mindgraph/.claude/skills/sprint/SKILL.md` (agent-skill 정의) |
| RAG 파이프라인 | (사용자 코드 미확인) | TODO: 사용자 확인 |
| Vector DB (Faiss·Milvus·Weaviate) | (사용자 코드 미확인) | TODO: 사용자 확인 |
| React Suspense / useSuspenseQuery | chatGraph 페이지 컴포넌트 분리 | `content/resume/FE/chatGraph_이력서.md` 본문 |
| Next.js App Router 병렬·인터셉팅 | xAB 모달 라우팅 | `content/resume/FE/xab_이력서.md` 본문 |
| D3 + Next.js SSR 격리 | mindgraph use client + transpilePackages | `refs/mindgraph/department/dev/web/next.config.ts`, `refs/mindgraph/.../canvas-view.tsx` |
| Supabase RLS · Realtime | mindgraph RLS 설계 + xAB Realtime postgres_changes 구독 | `content/resume/FDE/mindgraph_이력서.md`, `content/resume/FE/xab_이력서.md` |
| WebRTC RTCPeerConnection | Fit 시그널링 1:N | `content/resume/FE/Fit_이력서.md` 본문 |
| Vitest 회귀 테스트 | chatGraph 핵심 훅 회귀 보호 | `content/resume/AI-Native-Builder/chatGraph_이력서.md` 본문 |

## 5. 다음 작업 (분석 산출물 활용)

1. **이력서·포트폴리오 톤 재정렬** — 빈도 상위 키워드 ↔ 사용자 코드 매칭이 약한 부분 식별. 본 분석에서 "TODO: 사용자 확인"으로 표시된 RAG·Vector DB·PyTorch 영역은 룰 A에 따라 사용자 답변 후에만 본문 추가.
2. **target-companies.md 작성** — 직무별 강한 카드 ↔ 회사별 책임 매칭 (예: FDE/AIN ◎◎ = mindgraph → 채널톡·와이큐·Anthropic; FE ◎ × 4 = 세이프닥·오렌지스퀘어·월급쟁이부자들 등).
3. **약점 보강 학습 계획** — RAG·Vector DB·MCP 직접 구현 실습 등 사용자 확인 후 결정.
