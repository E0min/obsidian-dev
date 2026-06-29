# Dev/ — LLM Wiki Schema

> Karpathy LLM-Wiki 패턴의 **Schema layer**. LLM(Claude Code, Codex 등)이 이 wiki를 어떻게 읽고·쓰고·유지해야 하는지 알려주는 메뉴얼.

## 1. 3-Layer Architecture

```
Dev/
├── _sources/        ← Layer 1: Raw Sources (immutable, 사람이 모음)
├── <카테고리>/      ← Layer 2: The Wiki (LLM-owned, LLM이 추출·통합·유지)
└── CLAUDE.md        ← Layer 3: Schema (이 문서 — wiki 운영 규칙)
```

- **Layer 1 (`_sources/`)**: 원본 자료. 글/논문/영상/스크린샷/raw 노트. LLM은 **읽기만**, 절대 수정 금지.
- **Layer 2 (카테고리 폴더)**: LLM이 sources에서 추출·통합한 atomic 노트. summaries, concept pages, comparisons. LLM이 **소유 + 유지**.
- **Layer 3 (이 파일)**: LLM이 wiki를 어떻게 운영하는지 정의. 규칙·템플릿·승격 트리거.

## 2. LLM 운영 워크플로

### A. 새 source 추가 시 (Ingest)
1. 원본 파일은 `_sources/{articles|papers|videos|books|screenshots|raw-notes}/`에 저장 (immutable)
2. `_sources/_index.md`에 한 줄 등록 (제목 + 카테고리 태그 + 날짜)
3. 핵심 개념 추출 → 적절한 카테고리 `_concepts/<concept>.md`에 atomic 노트 생성/업데이트
4. atomic 노트의 `source:` frontmatter에 `_sources/...` 경로 명시 (양방향 추적)
5. 관련 MOC에 wikilink 추가 (`Currently learning` 섹션에 push)
6. 다른 카테고리와 cross-link 가능하면 `## Related`에 추가

### B. Wiki 유지 (Maintain)
- 매주: `_journal/` 노트 중 **재사용 가능한 atomic**을 `<카테고리>/_concepts/`로 **승격**(promote)
  - 원본 journal의 `promoted-to:` frontmatter에 승격 경로 기록
  - 승격된 atomic의 `status: seedling → budding`
- 매월: MOC 갱신 — `Core Ideas (evergreen)` 섹션에 시간 검증된 노트 이동
- 분기: budding 중 자주 참조되는 노트를 `evergreen` 승격

### C. 질문 응답 시 (Query)
LLM이 사용자 질문을 받으면:
1. 먼저 `_index.md` + 관련 카테고리 `_MOC.md` 스캔
2. `_concepts/` atomic 노트로 drill-down
3. 답이 불충분하면 `_sources/` 원본 자료 인용
4. 답변에 사용한 wikilink를 user에게 함께 제시

## 3. Atomic Note 작성 규칙

**원칙**: 한 노트 = 한 개념. 재사용 가능. 시간 불문.

**필수 frontmatter**:
```yaml
---
title:           # 명확한 한 줄
aliases: []      # 한↔영 동의어 (그래프 연결 강화)
type: concept    # concept | journal | decision | retro | post | project-index | moc
status: seedling # seedling | budding | evergreen  (= 노트 본문 작성 단계)
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: []         # 도메인 + 상태 + 직무 태그
related: []      # 명시적 wikilink (그래프 활성화)
source: []       # _sources/... 경로 또는 외부 URL
migrated-from:   # 이전 시 원본 경로 (출처 추적)

# 학습 추적 (선택 — 공부 시작 시 채움. status와 독립된 축)
confidence:      # 1-5 (1=얼핏만, 5=면접에서 설명 가능)
last-reviewed:   # YYYY-MM-DD (ISO 형식 필수 — Dataview date() 인식)
study-count:     # 정수 (학습 누적 횟수)
---
```

**학습 추적 필드 사용법**:
- `status`는 "노트 본문이 얼마나 작성됐는가" (seedling→budding→evergreen).
- `confidence`는 "내가 얼마나 익숙한가" (1~5) — **status와 독립**. budding이어도 confidence 5일 수 있고, evergreen이어도 처음 보는 노트면 1.
- `confidence` 입력 기준: `1` 거의 못 떠올림 / `2` 개념은 알지만 코드 못 짬 / `3` 도움 받으면 가능 / `4` 자신있게 사용 / `5` 설명·면접까지 자유로움
- 공부 시작 시: `confidence: 1`, `study-count: 1`, `last-reviewed: <오늘>` 세팅.
- 복습 끝낼 때: `last-reviewed: <오늘>`로 갱신, `study-count` +1, 익숙도 재평가해 `confidence` 상향.
- 빈 필드 (`confidence: `)는 "아직 공부 안 함" — Dataview에서 미학습으로 자동 집계.

**노트 수정 시**:
- `updated: <오늘>` 필드 갱신 (수동) — frontmatter의 정식 "마지막 수정일"
- **본문 보강이 곧 학습 행위**인 경우 (예제 추가·정리 정정·심화 메모) → `last-reviewed`도 함께 오늘로 갱신, `study-count` +1. 보강하면서 다시 읽었으니 사실상 복습한 것.
- 단순 typo·링크 수정만이면 `last-reviewed`는 건드리지 말 것.
- `file.mtime`은 옵시디언이 자동 기록 — 변경 활동(소소한 수정 포함) 추적용. Dataview에서 `file.mtime > date(today) - dur(7 days)`로 최근 활동 노트 가시화.

**복습 주기 — 간격 반복 (Spaced Repetition)**:
익숙도 낮을수록 짧은 주기. Dataview "복습 필요" 쿼리는 아래 표 기준.

| confidence | 복습 주기 |
|---|---|
| 1 | 3일 |
| 2 | 7일 |
| 3 | 14일 |
| 4 | 30일 |
| 5 | 60일 |

**본문 구조** (재사용 가능한 atomic):
```markdown
# {{title}}

> TL;DR: 한 문장 요약

## What     ← 개념 정의
## Why it matters     ← 왜 중요한가
## How      ← 구체적 예시·코드·다이어그램
## Pitfalls ← 함정·반례
## Related  ← [[wikilink]] 최소 2개
## Sources  ← _sources/... 또는 외부 URL
```

## 4. 폴더 컨벤션

- **`_index.md`**: 진입점 (vault 또는 카테고리)
- **`_MOC.md`**: Map of Contents (카테고리 진입점, 인간 + LLM 둘 다 사용)
- **`_concepts/`**: 카테고리 산하 평탄(flat) atomic 노트
- **`_sources/`**: Raw 자료 (수정 금지)
- **`_journal/`**: 날짜 기반 TIL (카테고리 횡단)
- **`_templates/`**: Templater 템플릿
- **`_attachments/`**: 이미지/PDF
- 최대 깊이: 3단계 (`Dev/<카테고리>/<서브>/<note>.md`)

## 5. 태그 컨벤션 (계층형)

- **상태**: `#status/seedling` `#status/budding` `#status/evergreen` `#status/archived`
- **타입**: `#type/concept` `#type/journal` `#type/adr` `#type/retro` `#type/post` `#type/moc`
- **도메인**: `#fe/react` `#fe/nextjs` `#fe/perf` `#be/api` `#be/observability` `#cs/algorithm` `#cs/network` `#ai/claude-code` `#ai/agent-pattern` `#ai/prompt` `#product/discovery` `#product/metric`
- **프로젝트**: `#project/<name>`
- **직무**: `#career/fe` `#career/product-engineer` `#career/fdd` `#career/ai-native`
- **메타**: `#question` `#contradiction` `#review-2026-Q2`

## 6. 링크 규칙 (그래프 활성화)

- 모든 atomic 노트는 최소 **2개 wikilink** 보유 (상위 MOC + 옆 관련 개념)
- `aliases:` 적극 사용 (한↔영)
- 링크에 context cue 추가: `LSM은 [[B-Tree]]와 달리 write-heavy에서 유리하다`
- MOC 간 cross-link로 카테고리 경계 횡단
- 비어있는 sub-MOC도 stub으로 유지 (옵시디언 unresolved link는 seedling 신호)
- **역방향 백링크 필수**: 새 노트 생성 또는 기존 노트 수정 시, 관련 기존 파일의 `## Related`에도 **역방향 링크를 추가**한다. 단방향 링크는 그래프를 단절시킨다. 예: A → B 링크를 추가했다면, B의 `## Related`에도 A를 추가.
- **기존 파일 연결 우선**: 새 내용 작성 전에 **연결 가능한 기존 파일이 있는지 먼저 확인**하고, 있다면 `## Related`에 추가해 그래프를 먼저 연결한다.

## 7. 승격(Promotion) 트리거

| 트리거 | 행동 |
|--------|------|
| journal에 같은 패턴 3회 이상 등장 | atomic 노트로 추출 → `<카테고리>/_concepts/` |
| atomic이 다른 노트에서 5회 이상 참조 | `status: budding → evergreen` |
| `confidence >= 4` + 본문 충실 | `status: budding → evergreen` 후보 (학습 검증된 노트) |
| evergreen 노트 3개가 한 주제로 묶임 | 새 sub-MOC 생성 |
| 같은 atomic이 두 카테고리에서 다 쓰임 | 더 적합한 곳으로 이동 + 다른 쪽은 wikilink만 |

## 8. 직무 매핑 (priority routing)

사용자는 4개 직무를 준비 중:

| 직무 | 핵심 카테고리 | 보조 |
|------|---------------|------|
| **FE** | FE/, CS/algorithms, CS/data-structures | DESIGN/ |
| **Product Engineer** | Product/, FE/, AI-Native/ | DESIGN/, Projects/ |
| **Forward Deployed Developer** | BE/, AI-Native/, CS/system-design | FE/, Product/discovery |
| **AI-Native Builder** | AI-Native/, FE/, BE/ | Product/, _journal/ |

직무 횡단 검색: `#career/<role> AND #status/evergreen`로 평가받을 자산만 추출.

## 9. 금지 사항

- ❌ `_sources/` 안의 파일 수정 (immutable)
- ❌ `~/깃허브/<repo>/` 안의 코드 복사해서 Wiki에 붙여넣기 (포인터만 — `Projects/<name>/links-to-code.md`)
- ❌ 같은 개념을 두 atomic에 중복 작성 (한 곳만, 다른 곳은 wikilink)
- ❌ 의미 없는 `_concepts/<concept>.md` stub 양산 — 최소 TL;DR이라도 채울 것
- ❌ frontmatter 누락 (검색·필터링 무력화)

## 9-1. 권장 사항 (기존 파일 활용)

- ✅ **기존 파일 보충 우선**: 동일하거나 관련된 개념을 다루는 파일이 이미 있다면 **새 파일 생성 대신 기존 파일에 보충**한다. 새 섹션 추가, 예시 보강, 누락된 관점 확장 등. 새 파일은 기존 파일로 커버되지 않는 독립 개념일 때만 생성.
- ✅ **기존 파일에 내용 추가 시 역방향 링크도 함께**: 기존 파일 A에 내용을 보충하면서 파일 B를 새로 만들었다면, A의 `## Related`에 B를, B의 `## Related`에 A를 모두 추가.
- ✅ **연관 파일 탐색**: 새 내용 작성 전 `find`, 파일 목록 탐색 등으로 기존 파일 존재 여부 확인. 비슷한 제목·태그의 파일이 있으면 먼저 읽고 판단.

## 10. Migration 컨텍스트

이 wiki는 기존 `MindGraph-TIL/` (01~05 폴더, posts/drafts/moc)에서 6주 점진적 이주 중. 모든 이전 노트는 `migrated-from:` frontmatter에 원본 경로 명시. 원본 vault는 2026-08까지 read-only 병행 후 archive.

상세 plan: `/Users/leeyoungmin/.claude/plans/obsidian-dev-rustling-blossom.md`

## 11. 취업/포폴 자산 sync 규칙

`Projects/취업/`은 `~/깃허브/취업/`의 컨텐츠를 흡수한다. **2026-05-23부터 이력서·포폴 MD도 옵시디언 vault가 SSOT** — `pdf-generator/content`는 symlink로 옵시디언을 가리킨다.

### SSOT 위치 (현행)

| 자산 | SSOT 위치 | 코드 접근 방식 |
|------|-----------|---------------|
| 이력서·포폴 MD | `~/obsidian/Dev/Projects/취업/이력서_포폴/content/` | symlink + `PDF_CONTENT_DIR` env var |
| 생성된 PDF | `~/obsidian/Dev/Projects/취업/이력서_포폴/outputs/` | `DEFAULT_OUTPUT_DIR` + `PDF_OUTPUT_DIR` env var |
| 작성 규칙 | `~/깃허브/취업/이력서_포폴/pdf-generator/CLAUDE.md` | 코드 디렉토리 (sync to 옵시디언 §11) |
| 가이드 | `~/obsidian/Dev/Projects/취업/이력서_포폴/guides/` | (옵시디언 working copy) |
| 면접 자료 | `~/obsidian/Dev/Projects/취업/이력서_포폴/interviews/projects/` | (옵시디언 working copy) |

### Sync 의무 (양방향)

| 변경 위치 | sync 대상 | 트리거 |
|-----------|-----------|--------|
| `pdf-generator/claude.md` (작성 규칙 변경) | 옵시디언 `Projects/취업/이력서_포폴/guides/_MOC.md`에 변경 사항 노트 | 규칙 의사결정 시 |
| `pdf-generator/content/resume|portfolio/{role}/` (이력서·포폴 컨텐츠 변경) | 옵시디언 cross-link 갱신 X (포인터만 유지) | — |
| 옵시디언 `Projects/취업/이력서_포폴/guides/이력서가이드.md` 또는 `포폴가이드.md` 변경 | `~/깃허브/취업/이력서_포폴/이력서가이드.md` 또는 `포폴가이드.md`로 sync | 가이드 발견 즉시 |
| 옵시디언 `Projects/취업/이력서_포폴/interviews/projects/*.md` 면접 자료 갱신 | (옵시디언이 working copy, sync 불필요) | — |
| **PDF 출력 위치** (`scripts/generate-pdf.ts` `DEFAULT_OUTPUT_DIR` 변경) | `Dev/Projects/취업/이력서_포폴/outputs/_MOC.md` + `Dev/Projects/pdf-generator/{architecture,links-to-code}.md` 경로 갱신 | DEFAULT_OUTPUT_DIR 상수 변경 시 |

### PDF 출력 위치 (2026-05-23부터)

- **기본 출력**: `~/obsidian/Dev/Projects/취업/이력서_포폴/outputs/{role}/{N}/{이력서|포트폴리오}.pdf`
- pdf-generator 깃허브 레포에는 PDF 저장되지 않음 (`output/` 디렉토리 비어있음, `.gitignore` 처리됨)
- override 우선순위: `--output=<path>` CLI > `PDF_OUTPUT_DIR` env > 옵시디언 vault default
- 관련 노트: [[취업/이력서_포폴/outputs/_MOC]]

### 직무 매핑 일관성

`Projects/취업/_INDEX.md`의 4직무 어필 매핑은 **`pdf-generator/content/{resume|portfolio}/{role}/`의 실제 직무 디렉토리 이름과 일치**해야 함 (대문자 + 하이픈 형식):
- `FDE` = Forward Deployed Developer (또는 Forward Deployed Engineer)
- `Product-Engineer` = Product Engineer
- `AI-Native-Builder` = AI-Native Builder
- `FE` = Frontend

매핑이 어긋나면 옵시디언 메타 지식이 stale → 즉시 정정. 실제 디렉토리 ls로 진실 원천 확인.

### 금지

- ❌ pdf-generator/content/ symlink 끊기 (코드 정적 import 깨짐) — 깨지면 `ln -s ~/obsidian/Dev/Projects/취업/이력서_포폴/content ~/깃허브/취업/이력서_포폴/pdf-generator/content`로 복구
- ❌ 옵시디언 vault 이동 시 symlink 재생성 잊기 — 또는 `PDF_CONTENT_DIR` env var로 우회
- ❌ 증명서류 PDF를 옵시디언으로 복사 (개인정보)
- ❌ `pdf-generator/CLAUDE.md` 변경하면서 옵시디언 가이드 안 갱신 (정합성 깨짐)
- ❌ content를 두 곳에 복제 (옵시디언 + 깃허브 디렉토리) — symlink 또는 env var 둘 중 하나만
