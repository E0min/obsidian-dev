---
type: links-to-code
project: 취업
updated: 2026-05-23
tags: [project/취업]
---

# 취업 — Links to Code

> `~/깃허브/취업/` 자산 매핑. **컨텐츠는 옵시디언이 SSOT, 코드는 깃허브 유지** (symlink로 연결).

## 코드 (pdf-generator)

| 경로 | 역할 | 옵시디언 |
|------|------|---------|
| `~/깃허브/취업/이력서_포폴/pdf-generator/` | Next.js 코드 (puppeteer + content 로더) | [[../pdf-generator/_INDEX]] |
| `~/깃허브/취업/이력서_포폴/pdf-generator/CLAUDE.md` | **작성 규칙 SSOT** | [[../../CLAUDE]] §11 |
| `~/깃허브/취업/이력서_포폴/pdf-generator/content` | **symlink** → `~/obsidian/Dev/Projects/취업/이력서_포폴/content/` | [[취업/이력서_포폴/content/_MOC]] |
| `~/깃허브/취업/이력서_포폴/pdf-generator/scripts/generate-pdf.ts` | PDF 생성 + 출력 경로 결정 | [[../pdf-generator/links-to-code]] |
| `~/깃허브/취업/이력서_포폴/pdf-generator/src/lib/content.ts` | content 로더 (env var fallback) | — |

## 옵시디언 이전된 컨텐츠

| 원본 | 옵시디언 위치 |
|------|---------------|
| `~/깃허브/취업/이력서_포폴/이력서가이드.md` | [[이력서가이드]] |
| `~/깃허브/취업/이력서_포폴/포폴가이드.md` | [[포폴가이드]] |
| `~/깃허브/취업/이력서_포폴/프롬프트.md` | [[프롬프트]] |
| `~/깃허브/취업/이력서_포폴/이력서_포폴_v2/fit_interview_prep.md` | [[fit]] |
| `~/깃허브/취업/이력서_포폴/이력서_포폴_v2/chatgraph_interview_prep.md` | [[chatgraph]] |
| `~/깃허브/취업/이력서_포폴/이력서_포폴_v2/xab_interview_prep.md` | [[xab]] |

## 레거시 (요약/포인터만)

| 원본 | 옵시디언 |
|------|---------|
| `~/깃허브/취업/이력서_포폴/이력서_포폴_v1/` | [[legacy-v1]] |
| `~/깃허브/취업/이력서_포폴/이력서_포폴_v2/{resume,portfolio}.md` | [[legacy-v2]] |
| `~/깃허브/취업/이력서_포폴/informations/` | [[informations]] |

## 증명서류 (코드 위치 유지, 메타만 옵시디언)

| 원본 | 옵시디언 |
|------|---------|
| `~/깃허브/취업/신분증, 통장사본/졸업예정증명서.pdf` | [[credentials]] |
| `~/깃허브/취업/신분증, 통장사본/근로계약서.pdf` | [[credentials]] |

## 갱신 워크플로

1. 이력서/포폴 컨텐츠 변경 → **`pdf-generator/content/`만 수정** (옵시디언 복사본 없음)
2. 작성 규칙 변경 → **`pdf-generator/claude.md` + `Dev/CLAUDE.md §11` 동시 sync**
3. 면접 준비 자료 → **옵시디언이 working copy**, 깃허브 v2는 archive
4. 새 가이드 추가 → 옵시디언 `guides/`에 + 필요 시 깃허브로 복사

## See also
- [[_INDEX]]
- [[../pdf-generator/links-to-code]]
- [[../../CLAUDE]]
