---
type: moc
title: 취업/이력서_포폴/outputs — 생성된 PDF 인덱스
status: budding
updated: 2026-06-06
tags: [moc, career, pdf-output]
---

# Outputs — pdf-generator로 생성된 PDF

> `~/깃허브/취업/이력서_포폴/이력서_포폴_v2/pdf-generator/`로부터 생성된 PDF의 저장 위치.
> 직무별 × 버전별 누적. 기존 회차는 자동 삭제 안 함 (수동 정리).

## 최신 버전 (2026-06-06)

| 직무 | 최신 폴더 | 파일 |
|------|----------|------|
| FDE | `FDE/41/` | `이력서_FDE.pdf` · `포트폴리오_FDE.pdf` |
| Product-Engineer | `Product-Engineer/39/` | `이력서_Product-Engineer.pdf` · `포트폴리오_Product-Engineer.pdf` |
| AI-Native-Builder | `AI-Native-Builder/40/` | `이력서_AI-Native-Builder.pdf` · `포트폴리오_AI-Native-Builder.pdf` |
| FE | `FE/43/` | `이력서_FE.pdf` · `포트폴리오_FE.pdf` |

## 디렉토리 구조

```
outputs/
├── FDE/{N}/{이력서_FDE.pdf, 포트폴리오_FDE.pdf}
├── Product-Engineer/{N}/{이력서_Product-Engineer.pdf, 포트폴리오_Product-Engineer.pdf}
├── AI-Native-Builder/{N}/{이력서_AI-Native-Builder.pdf, 포트폴리오_AI-Native-Builder.pdf}
└── FE/{N}/{이력서_FE.pdf, 포트폴리오_FE.pdf}
```

> 파일명 규칙(2026-06-03~): `이력서_{role}.pdf` · `포트폴리오_{role}.pdf` (`scripts/generate-pdf.ts`가 `_{role}` 접미사 자동 삽입).

## 생성 명령

```bash
cd ~/깃허브/취업/이력서_포폴/이력서_포폴_v2/pdf-generator

# 전 직무 (lint:mermaid → next build → puppeteer)
npm run pdf

# 단일 직무
npm run pdf -- --role=FDE

# 버전 강제 지정 (덮어쓰기)
npm run pdf -- --role=FDE --version=3
```

기본 출력은 이 폴더(`~/obsidian/Dev/취업/이력서_포폴/outputs/`)로 저장됨.

## 출력 경로 override

| 우선순위 | 방법 | 예 |
|---------|------|-----|
| 1 (최우선) | `--output=<path>` CLI | `npm run pdf -- --output=/tmp/test-out` |
| 2 | `PDF_OUTPUT_DIR=<path>` env | `PDF_OUTPUT_DIR=/tmp/test-out npm run pdf` |
| 3 (기본) | `DEFAULT_OUTPUT_DIR` in `scripts/generate-pdf.ts` | 이 폴더 |

## 버전 관리 규칙

- N은 자동 증분 (기존 폴더 최댓값 + 1)
- `--version=N`으로 강제 지정 시 덮어쓰기
- 의미 있는 버전만 남기고 나머지 수동 삭제

## 직무별 어필 PDF 어디서 쓰나

| 직무 | 최신 PDF 위치 | 어필 매핑 |
|------|---------------|-----------|
| FDE | `FDE/{최신N}/` | [[취업/_INDEX#Forward Deployed Developer (FDE)]] |
| Product-Engineer | `Product-Engineer/{최신N}/` | [[취업/_INDEX#Product Engineer]] |
| AI-Native-Builder | `AI-Native-Builder/{최신N}/` | [[취업/_INDEX#AI-Native Builder]] |
| FE | `FE/{최신N}/` | [[취업/_INDEX#FE]] |

## 관련 SSOT

- 작성 규칙: `~/깃허브/취업/이력서_포폴/이력서_포폴_v2/pdf-generator/CLAUDE.md` + `docs/`
- 컨텐츠 SSOT: [[취업/이력서_포폴/content/_MOC]]
- 옵시디언 schema: [[../../../CLAUDE]] §11

## 보안

- 옵시디언 vault가 외부 sync(Obsidian Sync, iCloud 등) 중이면 개인정보(이름·연락처) 노출 위험
- 필요 시 `outputs/`를 sync 제외하거나 별도 vault로 분리

## See also
- [[취업/_INDEX]]
- [[취업/이력서_포폴/content/_MOC]]
