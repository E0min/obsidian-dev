---
type: now
updated: 2026-05-25
tags: [now]
---

# Now — 2026-05-25

> 카파시 personal site의 "now" 페이지 컨셉. 이 한 페이지가 항상 현재를 비춘다.

## 현재 학습 중
- [[FE/react/_MOC]] — React 딥다이브 시작 (기초 4개 → 상태 → 훅 → 성능 → 상태관리 심화)

## 현재 sprint
- [ ] FE/react 기초 4개 노트 (MPA-SPA, react-앱-만들기, react-app-구동원리, 컴포넌트-라이프사이클) 학습 + frontmatter `confidence/last-reviewed/study-count` 입력
- [ ] react MOC §1~§4 완주 후 §5 성능 최적화 진입

## 현재 가장 자주 쓰는 atomic
- 

## 이번 주 발행 후보
- 

## 이번 주 승격 후보 (journal → _concepts)
- 

## 직무 준비 진행
- 타겟 회사: [[Projects/취업/target-companies]]
- 포폴 우선순위: [[Projects/취업/portfolio-strategy]]
- 다음 면접 준비: [[Projects/취업/이력서_포폴/interviews]]

---

## 이번 주 학습한 노트 (최근 7일)

```dataview
TABLE confidence as "익숙도", file.folder as "폴더", study-count as "횟수"
FROM "FE" OR "BE" OR "CS" OR "AI-Native" OR "Product" OR "DESIGN" OR "CodingTest"
WHERE last-reviewed AND date(today) - date(last-reviewed) <= dur(7 days)
SORT last-reviewed DESC
```

## 복습 필요 (vault 전체, 간격 반복)

```dataview
TABLE confidence as "익숙도", file.folder as "폴더", last-reviewed as "마지막", (date(today) - date(last-reviewed)).day as "경과일"
FROM "FE" OR "BE" OR "CS" OR "AI-Native" OR "Product" OR "DESIGN" OR "CodingTest"
WHERE confidence AND last-reviewed AND
  ((confidence = 1 AND date(today) - date(last-reviewed) > dur(3 days)) OR
   (confidence = 2 AND date(today) - date(last-reviewed) > dur(7 days)) OR
   (confidence = 3 AND date(today) - date(last-reviewed) > dur(14 days)) OR
   (confidence = 4 AND date(today) - date(last-reviewed) > dur(30 days)) OR
   (confidence = 5 AND date(today) - date(last-reviewed) > dur(60 days)))
SORT confidence ASC, last-reviewed ASC
LIMIT 30
```

## 최근 7일 수정된 노트 (vault 전체)

본문 보강이 있었다면 학습 행위로 간주하고 `last-reviewed`도 같이 갱신할 것.

```dataview
TABLE file.mtime as "파일 수정", file.folder as "폴더", confidence
FROM "FE" OR "BE" OR "CS" OR "AI-Native" OR "Product" OR "DESIGN" OR "CodingTest"
WHERE file.mtime >= date(today) - dur(7 days) AND file.name != "_MOC" AND file.name != "_now"
SORT file.mtime DESC
LIMIT 30
```

## 카테고리별 학습 시작률

```dataview
TABLE WITHOUT ID
    file.folder as "폴더",
    length(filter(rows, (r) => r.confidence)) as "학습 시작",
    length(rows) as "전체",
    round(length(filter(rows, (r) => r.confidence)) / length(rows) * 100) + "%" as "비율"
FROM "FE" OR "BE" OR "CS" OR "AI-Native" OR "Product" OR "DESIGN" OR "CodingTest"
WHERE file.name != "_MOC" AND file.name != "_now"
GROUP BY file.folder
SORT length(rows) DESC
LIMIT 15
```

---

## 학습 추적 메타 (필드 정의)

`confidence` (1-5), `last-reviewed` (YYYY-MM-DD), `study-count` (정수). 상세: [[CLAUDE]] §3.

대시보드: [[FE/_MOC]] · [[FE/react/_MOC]]
