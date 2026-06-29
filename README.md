# Dev/ — 세컨드 브레인

> 평생 운영할 컴퓨터 공부 위키. **Karpathy LLM-Wiki 3-Layer + Andy Matuschak evergreen notes** 패턴.
> 코드는 `~/깃허브/`, 지식 레이어는 여기.

직무 준비: **FE / Product Engineer / Forward Deployed Developer / AI-Native Builder**
구축 시작일: **2026-05-23**

---

## 목차

- [핵심 철학](#핵심-철학)
- [빠른 시작](#빠른-시작)
- [디렉토리 구조](#디렉토리-구조)
- [카파시 LLM-Wiki 3-Layer](#카파시-llm-wiki-3-layer)
- [9개 카테고리](#9개-카테고리)
- [노트 종류 + 라이프사이클](#노트-종류--라이프사이클)
- [태그 컨벤션](#태그-컨벤션)
- [운영 루틴](#운영-루틴)
- [외부 자산 연결](#외부-자산-연결)
- [직무 매핑](#직무-매핑)
- [통계 (2026-05-23)](#통계-2026-05-23)
- [Migration 컨텍스트](#migration-컨텍스트)
- [Pitfalls / 함정](#pitfalls--함정)
- [참고 자료](#참고-자료)

---

## 핵심 철학

| 원칙 | 설명 |
|------|------|
| **atomic note** | 한 노트 = 한 개념. 재사용 가능. 시간 불문 |
| **링크 우선, 폴더는 얕게** | 폴더 최대 3단계. 사고의 연결은 `[[wikilink]]`로 |
| **MOC = hub** | 각 카테고리 `_MOC.md`가 그래프 뷰의 중심 노드 |
| **status 라이프사이클** | `seedling → budding → evergreen` (Andy Matuschak) |
| **승격(Promote)** | journal에서 재사용 가능한 atomic 추출 → `_concepts/` |
| **LLM이 wiki를 소유** | Karpathy 패턴 — `CLAUDE.md` schema가 운영 규칙을 LLM에게 전달 |
| **Single Source of Truth** | 같은 개념을 두 곳에 적지 않음. 한 곳 + wikilink |
| **사실 기반** | 직무 자산은 Anti-Hallucination 원칙 (`pdf-generator/CLAUDE.md`) |

영감:
- [Andrej Karpathy LLM-Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) — 3-Layer (Raw Sources / Wiki / Schema)
- Andy Matuschak — evergreen notes (status 라이프사이클)
- Linking Your Thinking (LYT) — MOC 패턴

---

## 빠른 시작

### 1. 옵시디언 설정 (1회)

| 설정 | 값 |
|------|-----|
| **Files & Links → Default attachment folder** | `Dev/_attachments/` |
| **Templates → Template folder location** | `Dev/_templates/` |
| **Graph View → 시작 노드** | `Dev/_index.md` (개인 즐겨찾기) |

### 2. 진입점

- **`_index.md`** — vault 홈 (Karpathy wiki Home 역할)
- **`_MOC.md`** — 9개 카테고리 마스터 허브
- **`_now.md`** — 현재 sprint / 학습 주제 한 페이지

### 3. 자주 하는 작업

| 작업 | 위치 |
|------|------|
| 새 atomic 노트 | `<카테고리>/_concepts/<concept>.md` + Templater `atomic-note` |
| TIL 작성 | `_journal/YYYY/YYYY-MM/YYYY-MM-DD-<slug>.md` |
| 새 프로젝트 시작 | `Projects/<name>/_INDEX.md` + `architecture.md` + `links-to-code.md` |
| ADR 작성 | `Projects/<name>/decisions/00X-<topic>.md` |
| 회고 | `Projects/<name>/retro/YYYY-MM-Wn.md` |
| 블로그 draft | `Blog/drafts/YYYY-MM-DD-<slug>.md` + Templater `blog-draft` |
| 새 source 보관 | `_sources/{articles,papers,videos,books,screenshots,raw-notes}/` |

---

## 디렉토리 구조

```
Dev/
├── _index.md                      # vault 진입점 (홈)
├── _MOC.md                        # 9개 카테고리 마스터 허브
├── _now.md                        # 현재 sprint / 학습 주제
├── README.md                      # 이 파일
├── CLAUDE.md                      # LLM 운영 규칙 (Karpathy schema)
│
├── _sources/                      # Layer 1: Raw Sources (immutable)
│   ├── articles/                  # 블로그/뉴스레터 스크랩
│   ├── papers/                    # 논문 PDF + 요약
│   ├── videos/                    # 영상 URL + 트랜스크립트
│   ├── books/                     # 책 노트
│   ├── screenshots/               # UI/디자인 영감
│   └── raw-notes/                 # 정제 안 된 메모
│
├── _templates/                    # Templater 표준 템플릿 8종
│   ├── atomic-note.md
│   ├── moc.md
│   ├── journal-til.md
│   ├── project-index.md
│   ├── project-decision.md        # ADR
│   ├── project-retro.md
│   ├── blog-draft.md
│   └── concept-stub.md
│
├── _attachments/                  # 이미지/PDF (옵시디언 기본)
├── _journal/                      # 날짜 기반 TIL (카테고리 횡단)
│
├── CS/                            # 컴퓨터 사이언스 기초
├── FE/                            # 프론트엔드 (React/Next.js/D3/...)
├── BE/                            # 백엔드 (API/DB/infra/observability)
├── Product/                       # 프로덕트 사고 + 기획 + PM
├── DESIGN/                        # 디자인 시스템 + UX
├── AI-Native/                     # AI 네이티브 워크플로
├── CodingTest/                    # 알고리즘 풀이 (CS/algorithms와 분리)
├── Projects/                      # 프로젝트별 지식 레이어
└── Blog/                          # 발행 / draft / ideas
```

각 카테고리 내부 표준:
```
<카테고리>/
├── _MOC.md                        # 카테고리 진입점 (그래프 hub)
├── _concepts/                     # 재사용 가능 atomic 노트 (평탄)
└── <서브토픽>/                    # 그룹화된 노트 (필요 시만)
```

각 프로젝트 폴더 표준:
```
Projects/<name>/
├── _INDEX.md                      # 진입점 (status, repo 경로, 최근 활동)
├── architecture.md                # 시스템 다이어그램 + 데이터 흐름
├── links-to-code.md               # ~/깃허브/<name>/ 핵심 파일 포인터
├── decisions/                     # ADR (Architecture Decision Records)
├── retro/                         # 스프린트 회고
└── learnings/                     # atomic 학습 (재사용 가능하면 카테고리로 승격)
```

---

## 카파시 LLM-Wiki 3-Layer

```
┌───────────────────────────────────────────────────────────┐
│ Layer 1 — Raw Sources (immutable, 사람이 모음)            │
│   Dev/_sources/                                           │
│   원본 자료. LLM은 읽기만, 절대 수정 금지.                │
├───────────────────────────────────────────────────────────┤
│ Layer 2 — The Wiki (LLM-owned, 점진적 유지)               │
│   Dev/{CS,FE,BE,Product,DESIGN,AI-Native,                 │
│        CodingTest,Projects,Blog}/                         │
│   LLM이 sources에서 추출 + 통합 + 유지.                   │
│   atomic 노트, MOC, ADR, 회고, 발행글.                    │
├───────────────────────────────────────────────────────────┤
│ Layer 3 — Schema (LLM 운영 메뉴얼)                        │
│   Dev/CLAUDE.md                                           │
│   LLM이 wiki를 어떻게 읽고·쓰고·유지하는지 규칙.          │
│   §1~11: 3-layer / 워크플로 / atomic 규칙 / 태그 /        │
│         링크 / 승격 / 직무 매핑 / 금지 사항 /             │
│         migration / 취업·포폴 sync                        │
└───────────────────────────────────────────────────────────┘
```

자세한 운영 규칙은 [[CLAUDE]] 참조.

---

## 9개 카테고리

| # | 카테고리 | MOC | 핵심 주제 |
|---|----------|-----|----------|
| 1 | CS | [[CS/_MOC]] | 알고리즘 이론, 자료구조, 네트워크, OS, DB, 시스템 디자인 |
| 2 | FE | [[FE/_MOC]] | React, Next.js, performance, browser, D3, TypeScript |
| 3 | BE | [[BE/_MOC]] | API design, auth, databases, infra, observability |
| 4 | Product | [[Product/_MOC]] | 프로덕트 사고, JTBD, metrics, strategy, case studies |
| 5 | DESIGN | [[DESIGN/_MOC]] | 디자인 시스템, typography, UX patterns |
| 6 | AI-Native | [[AI-Native/_MOC]] | Claude Code, agents, prompts, spec-driven, 184 스킬 |
| 7 | CodingTest | [[CodingTest/_MOC]] | 알고리즘 풀이, 패턴 atomic (CS/algorithms와 분리) |
| 8 | Projects | [[Projects/_MOC]] | 14개 프로젝트의 지식 레이어 (코드는 `~/깃허브/`) |
| 9 | Blog | [[Blog/_MOC]] | 발행 글, drafts, 시리즈 |

횡단:
- [[_journal/_MOC]] — 날짜 기반 TIL
- [[_sources/_MOC]] — Layer 1 Raw Sources

---

## 노트 종류 + 라이프사이클

### 4가지 노트 종류

| 종류 | 위치 | 정의 | 예시 |
|------|------|------|------|
| **Atomic Concept** | `<카테고리>/_concepts/<concept>.md` 또는 `<카테고리>/<서브>/<concept>.md` | 한 개념, 재사용 가능, 시간 불문 | `react-compiler-memo-불필요.md` |
| **Journal / TIL** | `_journal/YYYY/YYYY-MM/YYYY-MM-DD-*.md` | 날짜·맥락·그날 깨달은 것 | `2026-05-04-next-intl-cache.md` |
| **Project note** | `Projects/<proj>/...` | 특정 프로젝트 종속 (ADR, 회고, learnings) | `decisions/001-fx-fy-dual-semantics.md` |
| **Blog draft/post** | `Blog/drafts/` 또는 `Blog/published/` | 외부 발행용 (atomic 합성) | `2026-05-11-1인-개발-워크플로우-1편.md` |

### Status 라이프사이클 (Andy Matuschak)

```
seedling → budding → evergreen
   ↓          ↓          ↓
   "씨앗"   "자라는중"  "시간 검증됨"
   미완성   구조 잡힘   자주 참조됨
```

### 승격(Promotion) 트리거 ([[CLAUDE]] §7)

| 트리거 | 행동 |
|--------|------|
| journal에 같은 패턴 3회 이상 등장 | atomic 노트로 추출 → `<카테고리>/_concepts/` |
| atomic이 다른 노트에서 5회 이상 참조 | `status: budding → evergreen` |
| evergreen 노트 3개가 한 주제로 묶임 | 새 sub-MOC 생성 |
| 같은 atomic이 두 카테고리에서 다 쓰임 | 더 적합한 곳으로 이동 + 다른 쪽은 wikilink만 |

---

## 태그 컨벤션

폴더와 중복되지 않게 **횡단 분류**에만 태그. 계층형 사용.

| 종류 | 예시 |
|------|------|
| **상태** | `#status/seedling` `#status/budding` `#status/evergreen` `#status/archived` |
| **타입** | `#type/concept` `#type/journal` `#type/adr` `#type/retro` `#type/post` `#type/moc` |
| **도메인** | `#fe/react` `#fe/nextjs` `#fe/perf` `#be/api` `#be/observability` `#cs/algorithm` `#ai/claude-code` `#ai/agent-pattern` |
| **프로젝트** | `#project/mindgraph` `#project/pdf-generator` `#project/취업` |
| **직무** | `#career/fe` `#career/product-engineer` `#career/fdd` `#career/ai-native` |
| **메타** | `#question` `#contradiction` `#review-2026-Q2` |

직무 횡단 검색 예: `#career/fdd AND #status/evergreen` → FDD 면접 준비 자산만.

---

## 운영 루틴

| 주기 | 행동 |
|------|------|
| **매일** | `_journal/YYYY-MM-DD-*.md` 1~3개 작성 (Templater 단축키) |
| **매주 일요일** | 그 주 journal에서 `_concepts/`로 승격할 후보 선별 |
| **매월** | MOC 갱신 — `Core Ideas (evergreen)` 섹션에 시간 검증된 노트 이동, 그래프 뷰 캡처 |
| **분기** | budding → evergreen 심사, Blog 발행 후보 추출 |

---

## 외부 자산 연결

### `~/깃허브/` 코드 (Single Source of Truth = 코드)

옵시디언 노트는 **`Projects/<name>/links-to-code.md`로 포인터만** 유지. 코드 본문 복사 금지.

| 프로젝트 | 깃허브 위치 | 상태 | dev 서버 |
|----------|-------------|------|----------|
| mindgraph | `~/깃허브/mindgraph` | 활성 | `npm run dev` 가능 |
| chatGraph | `~/깃허브/chatGraph-FE-local` | 활성 | `npm run dev` 가능 |
| Fit | `~/깃허브/FiT` | 레거시 | 정적 검증만 |
| xab | `~/깃허브/xab` | 레거시 | 정적 검증만 |
| pdf-generator | `~/깃허브/취업/이력서_포폴/pdf-generator` | 활성 | content + outputs가 옵시디언 SSOT |
| CodingTest | `~/깃허브/CodingTest` | 활성 | 패턴 노트와 양방향 링크 |
| virtual-company | `~/깃허브/virtual-company` | monorepo | — |

### pdf-generator hybrid (특수)

```
~/obsidian/Dev/Projects/취업/이력서_포폴/content/   ← SSOT (옵시디언)
                  ↑ symlink
~/깃허브/취업/이력서_포폴/pdf-generator/content/
                  ↑ 코드가 정적 import + fs.readFile

~/obsidian/Dev/Projects/취업/이력서_포폴/outputs/    ← 기본 출력 (옵시디언)
                  ↑ DEFAULT_OUTPUT_DIR in scripts/generate-pdf.ts
~/깃허브/취업/이력서_포폴/pdf-generator/scripts/generate-pdf.ts
```

자세한 sync 규칙은 [[CLAUDE]] §11 참조.

---

## 직무 매핑

vault는 4직무 동시 준비를 지원합니다.

| 직무 | 핵심 카테고리 | 보조 |
|------|---------------|------|
| **FE** (Frontend) | FE/, CS/algorithms, CS/data-structures | DESIGN/ |
| **Product Engineer** | Product/, FE/, AI-Native/ | DESIGN/, Projects/ |
| **Forward Deployed Developer** | BE/, AI-Native/, CS/system-design | FE/, Product/discovery |
| **AI-Native Builder** | AI-Native/, FE/, BE/ | Product/, _journal/ |

직무별 자산 진입:
- [[취업/_INDEX]] — 4직무 어필 매핑 + 프로젝트 매트릭스
- [[취업/이력서_포폴/content/_MOC]] — 이력서·포폴 SSOT
- [[취업/이력서_포폴/outputs/_MOC]] — 생성된 PDF
- [[취업/이력서_포폴/interviews/_MOC]] — 면접 준비 자료

---

## 통계 (2026-05-23)

| 지표 | 값 |
|------|----|
| 총 마크다운 노트 | **122개** |
| 총 디렉토리 | **132+개** |
| 9개 카테고리 _MOC | **9/9** |
| 표준 템플릿 | **8개** |
| **status: evergreen** | 16개 |
| **status: budding** | 28+개 |
| **status: seedling** | 12개 |
| `migrated-from:` 박제 노트 | 29개 (MindGraph-TIL 이전) |
| Projects/취업 산하 자산 | 77개 (md + json + jpg + pdf) |
| content/ 안 SSOT 파일 | 36개 (이력서·포폴 32 + meta 4) |
| outputs/ 안 PDF | 26개 (FDE 8 + FE 6 + PE 6 + AI-N 6) |

---

## Migration 컨텍스트

이 vault는 기존 `MindGraph-TIL/`에서 점진적으로 이주했습니다.

| Week | 작업 | 상태 |
|------|------|------|
| Week 1 | 골격 + 템플릿 + MOC stub | 완료 |
| Week 2 | 02-Problem-Solving → FE/BE (7개) | 완료 |
| Week 3 | 03-D3-Graph-Logic → FE/d3 + Projects/mindgraph (7개 + ADR 2개) | 완료 |
| Week 4 | 01-Workflow-and-Harness → AI-Native (7개 + 5층 역전파 메타) | 완료 |
| Week 5 | Blog + 05-Ops + Projects 골격 | 완료 |
| Week 6 | 취업/CodingTest + content/outputs 이전 | 완료 |
| Week 7+ | 운영 루틴 (매일/주/월/분기) | 진행 중 |
| Week 12 (2026-08) | `MindGraph-TIL/` zip archive | 예정 |

상세 plan: `/Users/leeyoungmin/.claude/plans/obsidian-dev-rustling-blossom.md`

원본 `MindGraph-TIL/`은 2개월 병행 후 archive 예정. 모든 이전 노트의 `migrated-from:` frontmatter로 원본 추적 가능.

---

## Pitfalls / 함정

[[CLAUDE]] §9 + §11 금지 사항 참조. 가장 큰 함정:

1. **이력서/포폴 MD를 두 곳에 복제 X** — `~/obsidian/Dev/Projects/취업/이력서_포폴/content/`가 SSOT, 코드는 symlink로 참조
2. **`pdf-generator/content/` symlink 끊지 말 것** — 끊기면 `ln -s ~/obsidian/Dev/Projects/취업/이력서_포폴/content ~/깃허브/취업/이력서_포폴/pdf-generator/content`로 복구
3. **`_sources/` 파일 수정 X** — Layer 1은 immutable
4. **`~/깃허브/` 코드를 옵시디언으로 복사 X** — `links-to-code.md`로 포인터만
5. **frontmatter 누락 X** — 검색·필터링 무력화
6. **의미 없는 stub 양산 X** — 최소 TL;DR이라도 채울 것
7. **증명서류 PDF를 옵시디언으로 복사 X** — 개인정보 (cloud sync 노출 위험)
8. **pdf-generator/CLAUDE.md 변경 시 옵시디언 가이드 sync** — `Projects/취업/이력서_포폴/guides/_MOC.md`에 변경 사항 노트

---

## 참고 자료

### 핵심 schema 문서
- [[CLAUDE]] — LLM 운영 메뉴얼 (Karpathy Layer 3)
- [[_index]] — vault 홈
- [[_MOC]] — 마스터 MOC
- [[_now]] — 현재 활동 한 페이지

### 외부 영감
- [Andrej Karpathy LLM-Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
- [Beyond RAG: Karpathy's LLM Wiki Pattern](https://levelup.gitconnected.com/beyond-rag-how-andrej-karpathys-llm-wiki-pattern-builds-knowledge-that-actually-compounds-31a08528665e)
- Andy Matuschak — evergreen notes 시스템
- Nick Milo — Linking Your Thinking (LYT)

### 진행 중 / 보류 항목

- **Evidence Card 패턴** (보류) — 이력서·포폴 사실의 코드 증거 박제 시스템. dynamic verification (mindgraph, chatGraph) + static-only (Fit, xab) 두 트랙. 도입 시 `Projects/_conventions/evidence-card.md` 부터.
- **Skills 메타 인덱스** — `AI-Native/skills/_index-by-category.md` 184개 스킬 자동 인덱싱 (예정)
- **취업/이력서_포폴/jd-analysis/** — 타겟 회사 3~5개 JD 분석 (예정)
- **CodingTest 패턴 확장** — 현재 5패턴 (two-pointer, sliding-window, dfs-bfs, dp, monotonic-stack), 추가 5+ 예정

---

## 라이선스 / 저자

개인 wiki. 외부 공유 안 함. 발행은 `Blog/published/` 산하 글만 (Velog/Brunch 등 외부 채널로).

**Last updated**: 2026-05-23
**저자**: 이영민 (`bbok4yo@gmail.com`)
