---
type: project-index
status: active
created: 2026-05-23
last-touched: 2026-05-23
repo: ~/깃허브/취업/이력서_포폴/pdf-generator
tags: [project/pdf-generator, status/active, career/product-engineer, career/ai-native]
---

# pdf-generator — 이력서·포폴 PDF 자동 생성기

> Next.js + TypeScript + puppeteer. 4직무(FDE/PE/AI-Native-Builder/FE) × 이력서·포폴 8세트 MD를 PDF로 렌더. `claude.md`가 작성 규칙 SSOT.

## Status
- 현재: 4직무 컨텐츠 운영 중
- 다음 액션: 직무별 컨텐츠 갱신 sprint

## Stack
- Next.js + TypeScript
- puppeteer (PDF 렌더링)
- React (페이지 컴포넌트)

## Content 구조 (SSOT는 옵시디언, 코드는 symlink)
```
~/obsidian/Dev/Projects/취업/이력서_포폴/content/                     ← SSOT (옵시디언)
├── _about.md                                              # 공통 프로필 헤더
├── me.jpg                                                 # 프로필 이미지
├── pdf.config.json                                        # 직무별 files 순서
├── resume/{FDE,Product-Engineer,AI-Native-Builder,FE}/    # 직무별 4세트
└── portfolio/{FDE,Product-Engineer,AI-Native-Builder,FE}/

~/깃허브/취업/이력서_포폴/pdf-generator/
├── content/  →  symlink → 위 옵시디언 경로
├── src/                                                   # Next.js 페이지 + PDF 렌더
├── scripts/generate-pdf.ts                                # PDF 생성 스크립트
├── CLAUDE.md                                              # 작성 규칙 SSOT
└── refs/mindgraph                                         # 옵시디언 참조 심링크

# PDF 출력은 별도 위치:
~/obsidian/Dev/Projects/취업/이력서_포폴/outputs/{role}/{N}/{이력서|포트폴리오}.pdf  ← 직무 자산
```

## Map
- [[architecture]] — Next.js + content + claude.md SSOT 구조
- [[Projects/pdf-generator/links-to-code]] — `~/깃허브/취업/이력서_포폴/pdf-generator/` 파일 포인터
- [[decisions/_MOC]] — ADR
- [[retro/_MOC]] — 회고
- [[jd-mapping/_MOC]] — JD ↔ 포폴 항목 매핑 규칙

## 4직무 어필 매핑

| 직무 | content key | 핵심 메시지 |
|------|-------------|------------|
| FDE | `resume/FDE/`, `portfolio/FDE/` | Forward Deployed — 고객과 함께 짓는 엔지니어 |
| Product-Engineer | `resume/Product-Engineer/`, `portfolio/Product-Engineer/` | Product Engineer — 의사결정 + 구현 |
| AI-Native-Builder | `resume/AI-Native-Builder/`, `portfolio/AI-Native-Builder/` | AI 네이티브 워크플로 운영 |
| FE | `resume/FE/`, `portfolio/FE/` | 프론트엔드 깊이 + 시각화 |

## 외부 링크
- 깃허브: `~/깃허브/취업/이력서_포폴/pdf-generator/`
- 작성 규칙 SSOT: `pdf-generator/claude.md` ↔ [[../../CLAUDE]]

## See also
- [[취업/_INDEX]] — 직무 준비 메타 프로젝트
- [[취업/이력서_포폴/guides/_MOC]] — 이력서/포폴 가이드
- [[취업/이력서_포폴/interviews/_MOC]] — 면접 준비
