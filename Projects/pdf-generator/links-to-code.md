---
type: links-to-code
project: pdf-generator
updated: 2026-05-23
tags: [project/pdf-generator]
---

# pdf-generator — Links to Code

> 옵시디언 ↔ `~/깃허브/취업/이력서_포폴/pdf-generator/` 양방향 포인터.
> **2026-05-23부터 content는 옵시디언 SSOT, 코드는 symlink로 참조**.

## SSOT 파일

| 파일 | 역할 | 위치 | 옵시디언 cross-link |
|------|------|------|---------------------|
| `CLAUDE.md` | **작성 규칙 SSOT** | 깃허브 (pdf-generator/) | [[../../CLAUDE]] §11 sync 의무 |
| `pdf.config.json` | 직무별 출력 순서·설정 | 옵시디언 (content/) | [[취업/이력서_포폴/content/_MOC]] |
| `_about.md` | 공통 프로필 헤더 | 옵시디언 (content/) | [[취업/이력서_포폴/content/_MOC]] |

## Content 파일 (직무 × 타입 = 8세트)

> 실제 위치: `~/obsidian/Dev/Projects/취업/이력서_포폴/content/` (옵시디언 SSOT)
> 코드 접근: `pdf-generator/content/` (symlink) 또는 `PDF_CONTENT_DIR` env var

### 이력서 (resume)

| 직무 | 옵시디언 경로 | 어필 매핑 |
|------|---------------|----------|
| FDE | [[취업/이력서_포폴/content/_MOC]] (`resume/FDE/`) | [[취업/_INDEX]] FDE 섹션 |
| Product-Engineer | [[취업/이력서_포폴/content/_MOC]] (`resume/Product-Engineer/`) | [[취업/_INDEX]] PE 섹션 |
| AI-Native-Builder | [[취업/이력서_포폴/content/_MOC]] (`resume/AI-Native-Builder/`) | [[취업/_INDEX]] AI-N 섹션 |
| FE | [[취업/이력서_포폴/content/_MOC]] (`resume/FE/`) | [[취업/_INDEX]] FE 섹션 |

### 포폴 (portfolio)

| 직무 | 옵시디언 경로 | 어필 매핑 |
|------|---------------|----------|
| FDE | [[취업/이력서_포폴/content/_MOC]] (`portfolio/FDE/`) | [[../취업/portfolio-strategy]] |
| Product-Engineer | [[취업/이력서_포폴/content/_MOC]] (`portfolio/Product-Engineer/`) | [[../취업/portfolio-strategy]] |
| AI-Native-Builder | [[취업/이력서_포폴/content/_MOC]] (`portfolio/AI-Native-Builder/`) | [[../취업/portfolio-strategy]] |
| FE | [[취업/이력서_포폴/content/_MOC]] (`portfolio/FE/`) | [[../취업/portfolio-strategy]] |

## src/ 핵심 파일

- `src/pages/[role]/resume.tsx` — Next.js 이력서 렌더링
- `src/pages/[role]/portfolio.tsx` — 포폴 렌더링
- `src/lib/markdown.ts` — MD → HTML 변환
- `scripts/generate-pdf.ts` — puppeteer PDF 생성 + 출력 경로 결정 (env/CLI/default)

## 출력 (Output) — 옵시디언 vault로 이전

| 종류 | 경로 | 비고 |
|------|------|------|
| **생성된 PDF** | `~/obsidian/Dev/Projects/취업/이력서_포폴/outputs/{role}/{N}/` | 기본 출력 위치 (2026-05-23 이전) |
| **옵시디언 인덱스** | [[취업/이력서_포폴/outputs/_MOC]] | 산출물 MOC |
| **출력 경로 코드** | `scripts/generate-pdf.ts` `DEFAULT_OUTPUT_DIR` 상수 | 변경 시 옵시디언 노트도 sync |

## 옵시디언 vault 참조

- `refs/mindgraph` (심링크) — 옵시디언 vault의 mindgraph 관련 노트 참조

## See also
- [[_INDEX]]
- [[architecture]]
- [[취업/이력서_포폴/links-to-code]]
