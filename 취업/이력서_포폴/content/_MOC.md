---
type: moc
title: 취업/이력서_포폴/content — SSOT 이력서·포폴 컨텐츠
status: evergreen
updated: 2026-06-06
tags: [moc, career, content-ssot]
---

# Content — 이력서·포폴 마크다운 SSOT

> 2026-05-23부터 **옵시디언이 SSOT**. 실제 경로는 `~/obsidian/Dev/취업/이력서_포폴/content/`.
> `~/깃허브/취업/이력서_포폴/이력서_포폴_v2/pdf-generator/content`가 symlink로 이 폴더를 가리킴.
> 여기서 편집하면 다음 `npm run dev` / `npm run pdf`에 즉시 반영.

## 구조

```
content/
├── _about.md                          # 모든 직무 공통 프로필 헤더
├── me.jpg                             # 프로필 이미지
├── pdf.config.json                    # 직무별 files 순서 + outputs 설정
├── resume/
│   ├── FDE/*_이력서.md
│   ├── Product-Engineer/*_이력서.md
│   ├── AI-Native-Builder/*_이력서.md
│   └── FE/*_이력서.md
└── portfolio/
    ├── FDE/*_portfolio.md
    ├── Product-Engineer/*_portfolio.md
    ├── AI-Native-Builder/*_portfolio.md
    └── FE/*_portfolio.md
```

## 직무별 노출 프로젝트 (`pdf.config.json` 기준, 2026-06-06)

| 직무 | 노출 프로젝트 | 비고 |
|------|--------------|------|
| FDE | mindgraph + chatGraph | 2개 |
| Product-Engineer | mindgraph + chatGraph + Fit + xab | 4개 |
| AI-Native-Builder | mindgraph + chatGraph | 2개 (chatGraph는 △ 등급이나 최소 2개 노출 규정 충족) |
| FE | mindgraph + chatGraph + Fit + xab | 4개 |

> `content/{resume,portfolio}/{role}/`에는 4 프로젝트 파일이 모두 존재하지만, PDF에는 위 노출 목록만 합본됨.

## 편집 워크플로

1. **옵시디언에서 직접 편집** (이 vault 폴더 안)
2. `pdf-generator` dev 서버 재시작 또는 `npm run pdf` 실행
3. 생성된 PDF → [[취업/이력서_포폴/outputs/_MOC]]

## SSOT 변경 (2026-05-23)

| 이전 | 이후 |
|------|------|
| `pdf-generator/content/` (코드 디렉토리) | `~/obsidian/Dev/취업/이력서_포폴/content/` (옵시디언 vault) |
| 코드와 함께 관리 | 옵시디언이 working copy |
| 한 곳만 편집 (코드 디렉토리) | 한 곳만 편집 (옵시디언) |

## 코드 측 참조 경로

- **정적 import**: `import config from "../../content/pdf.config.json"` (symlink 통해 동작)
- **런타임 fs.readFile**: `process.cwd()/content/` (symlink 통해 동작)
- **env var override**: `PDF_CONTENT_DIR=<path> npm run pdf`

## 작성 규칙 SSOT (계층화, 2026-06-03)

작성 규칙은 `~/깃허브/취업/이력서_포폴/이력서_포폴_v2/pdf-generator/` 아래에 계층화됨.

- `CLAUDE.md` — 공통 원칙 + 인덱스맵 (박-어휘 금지·INP 식별자 금지·미구현 코드 노출 금지 룰 A)
- `docs/writing.md` — 작성 수준·AI-slop 회피·금지 어휘·점검 체크리스트
- `docs/resume.md` — 이력서 분량 강제(한 불릿 한 문장·두 줄 이내)·작성 공식
- `docs/portfolio.md` — 포폴 헤더 형식·Case 3단 구조
- `docs/pdf-build.md` — PDF 빌드·파일명·SSOT 위치·검증
- `content/CLAUDE.md` — 직무별 강조 어순·노출 프로젝트·금지 키워드
- 외부 가이드 3종(이력서가이드·포폴가이드·AI-slop 방지 가이드)을 작성 전 항상 먼저 읽음

## 직무별 컨텐츠

### FDE — Forward Deployed Engineer
- `resume/FDE/` — 1인 LLM 솔루션 프로토타입(출시 전)·출시 후 응대 인프라 사전 구축·4 LLM 통합·프로토타이핑
- `portfolio/FDE/`

### Product-Engineer
- `resume/Product-Engineer/` — 1인 PO·문제 정의 우선·AI 워크플로우 자산·풀스택 라이프사이클
- `portfolio/Product-Engineer/`

### AI-Native-Builder
- `resume/AI-Native-Builder/` — 컨텍스트 엔지니어링·하네스 엔지니어링(9훅·3 phase·context-map 자동 라우팅)·4 LLM 통합 표면
- `portfolio/AI-Native-Builder/`

### FE — Frontend
- `resume/FE/` — React 19·Next.js 16 App Router·Vite 3종 빌드·D3 SSR 격리·Tiptap·MV3 브리지
- `portfolio/FE/`

## mindgraph 사실 상태 (2026-06-06 확정)

- **출시 전 1인 프로토타입** (도메인 getmindgraph.com 등록 후 출시 전, 실서비스 운영 아님)
- AI 운영 자산: **9개 훅**(차단 4 + 보조 5, commit-user-gate 폐기) · **plan·qa·ship 3 phase** /sprint · 4중 SSOT · 7부서·9에이전트 분리 + context-map 자동 라우팅
- 본문에서 제거한 미구현(또는 미완성 판단) 기능: 임베딩 추천(auto-link)·H1/H3 정량 측정(telemetry)·Force 시뮬레이션 정착 tick 단축 → 향후 업그레이드 후보는 [[취업/이력서_포폴/jd-analysis/upgrade-guide/AI-Native-Builder]] Gap에만 둠

## See also
- [[취업/_INDEX]] — 직무 어필 매핑
- [[취업/이력서_포폴/guides/_MOC]] — 작성 가이드
- [[취업/이력서_포폴/outputs/_MOC]] — 생성된 PDF
- [[../../../CLAUDE]] §11 — sync 규칙
