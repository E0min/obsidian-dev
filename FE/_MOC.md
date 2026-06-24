---
type: moc
title: FE — Map of Contents
status: budding
updated: 2026-05-23
tags: [moc, fe]
---

# FE — Frontend

> 가장 두꺼워질 카테고리. React/Next.js 중심 + browser internals + visualization.

## Sub-areas
- [[react/_MOC|react]] — rendering, hooks, compiler, patterns
- [[nextjs/_MOC|nextjs]] — App Router, RSC, middleware
- [[performance/_MOC|performance]] — Core Web Vitals, bundling, runtime
- [[typescript/_MOC|typescript]]
- [[css-styling/_MOC|css-styling]] — Tailwind, layout
- [[browser/_MOC|browser]] — Event loop, layout, paint
- [[tooling/_MOC|tooling]] — Vite, Turbopack, Biome
- [[d3-visualization/_MOC|d3-visualization]]
- [[debugging/_MOC|debugging]] — Chrome DevTools

## Core Ideas (evergreen)
- 

## Currently learning (budding)
- [[react/_MOC]] — 딥다이브 시작 (32개, 1-2주 분량)
- [[performance/core-web-vitals/웹-성능-측정]] — LCP·CLS·INP 측정·개선
- [[css-styling/html-css-기초]] — 박스 모델·시맨틱·접근성
- [[nextjs/이미지-최적화]] — next/image 활용
- [[tooling/webpack]] — 번들러 핵심
- (Week 2 이전 예정) 02-Problem-Solving/* → 여기로

## Seeds (seedling)
- 

---

## 학습 진행률 (FE 전체)

```dataview
TABLE confidence as "익숙도", last-reviewed as "마지막 학습", study-count as "횟수"
FROM "FE"
WHERE confidence
SORT confidence ASC, last-reviewed ASC
```

## 복습 필요 (간격 반복)

```dataview
TABLE confidence as "익숙도", last-reviewed as "마지막", (date(today) - date(last-reviewed)).day as "경과일"
FROM "FE"
WHERE confidence AND last-reviewed AND
  ((confidence = 1 AND date(today) - date(last-reviewed) > dur(3 days)) OR
   (confidence = 2 AND date(today) - date(last-reviewed) > dur(7 days)) OR
   (confidence = 3 AND date(today) - date(last-reviewed) > dur(14 days)) OR
   (confidence = 4 AND date(today) - date(last-reviewed) > dur(30 days)) OR
   (confidence = 5 AND date(today) - date(last-reviewed) > dur(60 days)))
SORT confidence ASC, last-reviewed ASC
```

## 최근 7일 수정된 노트 (FE 전체)

```dataview
TABLE file.mtime as "파일 수정", confidence
FROM "FE"
WHERE file.mtime >= date(today) - dur(7 days) AND file.name != "_MOC"
SORT file.mtime DESC
LIMIT 30
```

## 익숙도 분포 (FE 전체)

```dataview
TABLE WITHOUT ID confidence as "익숙도", length(rows) as "노트 수"
FROM "FE"
WHERE confidence
GROUP BY confidence
SORT confidence ASC
```

## 미학습 노트 수 (서브카테고리별)

```dataview
TABLE WITHOUT ID file.folder as "폴더", length(rows) as "미학습"
FROM "FE"
WHERE !confidence AND file.name != "_MOC"
GROUP BY file.folder
SORT length(rows) DESC
```

---

## See also
- [[../study/_MOC]] — 학습·커리어 허브 (기초 12주·꾸준히 할 것·MindGraph 기록)
- [[CS/compiler-runtime/_MOC]] — V8, JIT
- [[AI-Native/claude-code/_MOC]] — FE 개발 워크플로
- [[Projects/mindgraph/_INDEX]] — D3 활용 사례
