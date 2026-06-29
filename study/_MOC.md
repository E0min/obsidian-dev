---
type: moc
title: study — 학습·커리어 허브
aliases: [study, 학습 허브, 커리어 허브, 취업 전략, comeback]
status: budding
updated: 2026-06-24
tags: [moc, study, career/fe, fe/roadmap]
---

# study — 학습·커리어 허브

> 개발자로서 무엇을 공부하고(기초), 무엇을 꾸준히 쌓고, MindGraph를 만들며 무엇을 기록할지를 모은 진입점. 학습 노트 자체는 `FE/`·`CS/` 등 카테고리에 있고, 여기는 계획·방향·습관만 다룬다.

## 세 축

1. **기초과정** — AI에 위임했던 이해를 12주에 걸쳐 손으로 되찾는다. → [[00-로드맵-12주]] · [[02-학습-인덱스]] · [[01-습관과-원칙]]
2. **꾸준히 해야 할 것** — 기초를 뗀 뒤에도 꺾이지 않고 쌓을 영역과 습관. → [[꾸준히-해야할-것]]
3. **MindGraph 개발 기록** — 서비스를 만들며 더 주의 깊게 기록·사고할 지점. → [[mindgraph-개발기록-포인트]]

## 2026 취업 전략 4중점

영상 "2026 개발자 취업전략"(큰돌)에서, 네이버·카카오 합격자들의 공통점으로 제시한 네 가지. 자세한 매핑은 [[05-채용시장-요구사항]].

1. **기본기** — 자료구조·알고리즘·네트워크·OS·DB, 코딩테스트. AI가 만든 코드의 품질을 판단하려면 기본이 있어야 한다("AI 잘 쓰는 사람 + 기본 아는 사람"을 뽑는다).
2. **AI 활용** — 코덱스·클로드 코드로 리뷰·리팩토링을 하되, 최종 PR 머지는 사람이 검토한다. → [[04-ai-native-엔지니어]]
3. **숫자로 증명** — 문제 해결을 수치로(예: 1.8초→350ms, 비용 절감, UX 변화). 단순 구축은 단순 나열로. → [[06-제대로된-코드-작성]]
4. **서비스 운영 경험** — 기획→설계→구현→배포→운영→개선 전 과정을 겪는 사이드 프로젝트. → [[mindgraph-개발기록-포인트]]

추가: 팀플 · 기술 블로그·트러블슈팅 기록 꾸준히 · 오픈소스 작은 PR 3개+ · 자격증은 후순위.

## 문서

- [[00-로드맵-12주]] — 주차별 주제·맨손 과제·면접 질문
- [[01-습관과-원칙]] — 이해 외주 끊기·손코딩·디버깅 가설 먼저·AI 튜터
- [[02-학습-인덱스]] — 영역별 학습할 문서 전부 (체크리스트)
- [[03-프로젝트-소유권]] — Fit·chatGraph·xAB·MindGraph 결정 재유도
- [[04-ai-native-엔지니어]] — 검증·명세·분해·튜터·판단
- [[05-채용시장-요구사항]] — 시장이 요구하는 4축(동작원리·측정·설계·태도)과 공부 방향 매핑
- [[06-제대로된-코드-작성]] — 동작하는 코드 너머 제대로 된 코드를 짜는 7원칙
- [[꾸준히-해야할-것]] — 기초 이후 지속 트랙(CS·코테·AI·측정·기록·오픈소스·팀플)
- [[mindgraph-개발기록-포인트]] — MindGraph 개발 중 기록·사고 체크리스트

## 12주 체크리스트 (기초과정)

- [ ] 1주 JavaScript 코어 (1): 실행 컨텍스트·호이스팅·클로저
- [ ] 2주 JavaScript 코어 (2): 이벤트 루프·프로토타입·복사
- [ ] 3주 브라우저: 렌더링 파이프라인·이벤트 위임·CORS·저장소
- [ ] 4주 React (1): 리렌더 트리거·reconciliation/key·memo
- [ ] 5주 React (2): useEffect·StrictMode·하이드레이션
- [ ] 6주 TypeScript: 제네릭·유틸리티 타입
- [ ] 7주 성능·디버깅: Core Web Vitals·DevTools
- [ ] 8주 네트워크: HTTP·인증·토큰 보관
- [ ] 9주 CS 기초: 자료구조·알고리즘·코딩테스트
- [ ] 10주 프로젝트 소유권 재유도
- [ ] 11주 AI-native 체화: 검증·명세·분해
- [ ] 12주 통합: 사이드 프로젝트 맨손 재구현·모의면접

## 기본기 노트 진행률

```dataview
TABLE confidence as "익숙도", last-reviewed as "마지막", study-count as "횟수"
FROM "FE/javascript" OR "FE/browser" OR "FE/react" OR "FE/typescript" OR "FE/debugging"
WHERE file.name != "_MOC"
SORT confidence ASC, file.folder ASC
```

## 아직 학습 안 한 기본기 노트

```dataview
TABLE WITHOUT ID file.link as "노트", file.folder as "폴더"
FROM "FE/javascript" OR "FE/browser" OR "FE/react" OR "FE/typescript" OR "FE/debugging"
WHERE !confidence AND file.name != "_MOC"
SORT file.folder ASC
```

## See also

- [[../FE/_MOC]] — FE 전체 Map of Contents
- [[../취업/_INDEX]] — 이력서·포폴·JD 분석
- [[../취업/이력서_포폴/interviews/_MOC]] — 프로젝트별 면접 자료
- [[../CS/_MOC]] — CS 전공지식
- [[../AI-Native/_MOC]] — AI-native 기술
