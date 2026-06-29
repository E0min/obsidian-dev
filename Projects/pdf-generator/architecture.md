---
type: architecture
project: pdf-generator
status: budding
updated: 2026-05-23
tags: [project/pdf-generator, architecture]
---

# pdf-generator — Architecture

> Next.js 렌더링 + puppeteer PDF 추출 + content/ MD SSOT + claude.md 규칙.

## 데이터 흐름

```
~/obsidian/Dev/Projects/취업/이력서_포폴/content/{resume|portfolio}/{FDE|Product-Engineer|AI-Native-Builder|FE}/*.md   ← SSOT (옵시디언)
              │
              │  (symlink: pdf-generator/content → 옵시디언 vault)
              │
              ▼
        Next.js 페이지 (src/) — http://localhost:3210/pdf/{resume|portfolio}?role=R
              │  (src/lib/content.ts가 fs.readFile + gray-matter로 로드)
              │
              ▼ (puppeteer in scripts/generate-pdf.ts)
              │
~/obsidian/Dev/Projects/취업/이력서_포폴/outputs/{role}/{N}/{이력서|포트폴리오}.pdf   ← 옵시디언 vault
```

**Content 경로 우선순위** (in `src/lib/content.ts`):
1. `PDF_CONTENT_DIR=<path>` 환경변수 (override)
2. `pdf-generator/content/` (symlink → 옵시디언 vault)

**Output 경로 우선순위** (in `scripts/generate-pdf.ts`):
1. `--output=<path>` CLI 옵션
2. `PDF_OUTPUT_DIR=<path>` 환경변수
3. 기본값: `~/obsidian/Dev/Projects/취업/이력서_포폴/outputs/` (옵시디언 vault)

## 핵심 모듈

- **`content/_about.md`** — 모든 직무 공통 프로필 헤더 (이름, 연락처, 한 줄 소개)
- **`content/me.jpg`** — 프로필 이미지
- **`content/pdf.config.json`** — 출력 설정 (content/ 안에 위치)
- **`content/resume/{FDE,Product-Engineer,AI-Native-Builder,FE}/`** — 직무별 이력서 항목
- **`content/portfolio/{FDE,Product-Engineer,AI-Native-Builder,FE}/`** — 직무별 포트폴리오 상세
- **`claude.md`** — 작성 규칙 SSOT (사실 기반, 직무 차별화, 포폴 헤더 구조)
- **`src/pages/[role]/[type].tsx`** — Next.js 동적 라우팅 (resume/portfolio × 4직무)
- **`refs/mindgraph`** — 옵시디언 vault의 mindgraph 노트 참조 (심링크)

## 4직무 × 2타입 = 8세트

직무 디렉토리: `FDE`, `Product-Engineer`, `AI-Native-Builder`, `FE` (대문자 + 하이픈, pdf-generator 표준).

## 핵심 invariant

- **이력서/포폴 MD는 `content/`가 유일 SSOT** — 옵시디언에 복사 X, links-to-code로 참조만
- **`claude.md` 규칙 변경 시 `Dev/CLAUDE.md §11`로 sync 의무**
- **직무별 어필 메시지가 일관**되어야 함 (`portfolio-strategy.md` 참조)

## See also
- [[_INDEX]]
- [[Projects/pdf-generator/links-to-code]]
- [[취업/_INDEX]]
