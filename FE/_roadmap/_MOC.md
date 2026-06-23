---
type: moc
title: _roadmap — FE 12주 재정비
aliases: [재정비, FE 로드맵 허브, comeback]
status: budding
updated: 2026-06-23
tags: [moc, fe, fe/roadmap, career/fe]
---

# _roadmap — FE 기본기 재정비

> AI에 위임했던 이해를 12주에 걸쳐 손으로 되찾기 위한 허브. 계획·습관·학습 인덱스·프로젝트 소유권·AI-native 작업법을 모았다.

## 시작하기

1. [[01-습관과-원칙]] 먼저 읽기 (이 폴더를 쓰는 법과 4가지 원칙)
2. [[00-로드맵-12주]]에서 이번 주 범위 확인
3. [[02-학습-인덱스]]에서 학습할 노트를 열고, 본문 덮고 세 칸부터 풀기
4. 끝낸 노트에 `confidence`·`last-reviewed` 기입 ([[01-습관과-원칙]] 참고)

## 문서

- [[00-로드맵-12주]] — 주차별 주제·맨손 과제·면접 질문
- [[01-습관과-원칙]] — 이해 외주 끊기·손코딩·디버깅 가설 먼저·AI 튜터
- [[02-학습-인덱스]] — 영역별 학습할 문서 전부 (체크리스트)
- [[03-프로젝트-소유권]] — Fit·chatGraph·xAB·MindGraph 결정 재유도
- [[04-ai-native-엔지니어]] — 검증·명세·분해·튜터·판단

## 12주 체크리스트

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

- [[../_MOC]] — FE 전체 Map of Contents
- [[../../취업/interviews/_MOC]] — 프로젝트별 면접 자료
- [[../../AI-Native/_MOC]] — AI-native 기술
