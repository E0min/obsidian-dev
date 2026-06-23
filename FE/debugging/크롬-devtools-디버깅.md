---
title: 크롬 DevTools와 가설 우선 디버깅
aliases: [devtools, 크롬 개발자도구, breakpoint, 디버깅, Network 탭, Performance 탭]
type: concept
status: budding
created: 2026-06-23
updated: 2026-06-23
tags: [fe/debugging, status/budding]
related:
  - "[[../_MOC]]"
  - "[[../browser/렌더링-파이프라인]]"
  - "[[../performance/core-web-vitals/웹-성능-측정]]"
  - "[[../_roadmap/_MOC]]"
source: ["Chrome DevTools docs", "MDN: Firefox/Chrome debugger"]
---

# 크롬 DevTools와 가설 우선 디버깅

> TL;DR: 버그를 만나면 코드를 추측해 고치기 전에 Sources의 중단점, Network 탭, Console, Performance 탭으로 "어디서 무엇이 어긋났는지" 가설을 세우고 실측해 좁힌다.

## What

크롬 DevTools는 실행 중인 페이지의 상태를 실시간으로 들여다보는 브라우저 내장 도구다. 주요 탭의 역할:

- **Sources**: 자바스크립트 실행을 특정 줄에서 멈추는 중단점(breakpoint) 설정. 멈춘 시점의 변수값, 콜 스택, 스코프를 확인.
- **Network**: 페이지가 보낸 모든 HTTP 요청의 URL, 메서드, 상태 코드, 요청/응답 헤더, 페이로드, 타이밍(DNS, 연결, TTFB, 다운로드)을 기록.
- **Console**: 자바스크립트를 즉석 실행하고, `console.log`로 찍은 값과 런타임 에러를 출력.
- **Performance**: 일정 구간을 녹화해 메인 스레드의 작업(스크립팅, 렌더, 페인트), 레이아웃 재계산(reflow), 프레임 드롭을 타임라인으로 측정.

가설 우선 디버깅은 "이 줄이 문제일 것 같다"는 추측으로 코드를 바꾸는 대신, 관찰 가능한 증상에서 가설을 세우고(예: "콜백에 toggle 값이 false로 들어온다") 중단점이나 Network 로그로 그 가설을 참/거짓으로 판정한 뒤 원인을 좁히는 절차다.

## Why it matters

FE 실무에서 버그의 상당수는 코드 자체가 아니라 실행 시점의 데이터에서 생긴다. props가 undefined로 들어오거나, API가 401을 반환하거나, 상태 업데이트가 한 박자 늦게 반영되는 경우다. 소스만 읽어서는 이 값들이 보이지 않는다. 면접에서도 "API 응답이 200인데 화면이 안 바뀐다, 어떻게 디버깅하느냐" 같은 질문은 Network 탭으로 응답 본문을 먼저 까보고 Console에서 상태를 추적하는 절차를 설명할 수 있는지를 본다.

## How

**조건부 중단점**: 반복문이나 자주 호출되는 콜백에서 특정 조건일 때만 멈춘다. Sources에서 줄 번호를 우클릭 → "Add conditional breakpoint" → 조건식 입력.

```js
function renderRow(user, index) {
  // index === 42 일 때만 멈추도록 조건부 중단점 설정
  return `<tr><td>${user.name}</td></tr>`;
}
```

위에서 `index === 42`를 조건으로 걸면 43번째 행을 그릴 때만 실행이 멈추고, 그 시점의 `user` 객체를 Scope 패널에서 확인할 수 있다.

**watch와 Console 객체 추적**: Sources의 Watch 패널에 `user.profile.avatarUrl` 같은 식을 등록하면 단계 실행마다 값이 갱신된다. Console에서는 객체를 그대로 찍어 펼쳐 본다.

```js
const state = { count: 0, items: [{ id: 1 }] };
console.log(state);        // 펼쳐서 중첩 값 확인
console.table(state.items); // 배열을 표로 출력
console.log({ state });    // 변수명까지 라벨로 남김
```

**Network 탭으로 요청 진단**: 요청 한 건을 클릭하면 Headers(요청/응답 헤더), Payload(보낸 본문), Response(받은 본문), Timing(단계별 소요)이 나뉘어 표시된다. 401이면 Headers에서 `Authorization` 헤더가 실제로 붙었는지, Timing에서 TTFB가 길면 서버 처리가 느린 건지 본다.

**Performance로 병목 측정**: 녹화 버튼을 누르고 느린 동작을 재현한 뒤 멈추면, 메인 스레드 타임라인에 긴 작업이 노란(스크립팅) 또는 보라(렌더) 블록으로 나온다. 레이아웃을 강제로 다시 계산하는 코드는 "Recalculate Style"과 "Layout" 막대로 잡힌다.

```js
// 반복문 안에서 offsetHeight를 읽어 강제 reflow를 유발하는 안티패턴
items.forEach((el) => {
  el.style.height = el.offsetHeight + 10 + "px"; // 읽기와 쓰기가 번갈아 발생
});
```

Performance 녹화에서 이 코드는 forEach 반복 횟수만큼 Layout 막대가 촘촘히 찍혀 병목 위치를 가리킨다.

## Pitfalls

- `console.log(obj)`로 찍은 객체는 콘솔에서 펼치는 시점의 값을 보여줘서, 로그 직후 객체가 바뀌면 과거 값이 아니라 현재 값이 보일 수 있다. 스냅샷이 필요하면 `console.log(JSON.parse(JSON.stringify(obj)))`로 깊은 복사를 찍는다.
- Network 탭을 열기 전에 일어난 요청은 기록되지 않는다. 페이지 로드 시점 요청을 보려면 탭을 먼저 연 뒤 새로고침한다. "Preserve log"를 켜지 않으면 페이지 이동 시 기록이 지워진다.
- 소스맵이 없거나 깨지면 Sources에 번들된 난독화 코드만 보여 중단점을 원래 코드 위치에 걸 수 없다. 빌드 설정에서 소스맵 생성 여부를 확인한다.
- `debugger;` 문을 코드에 남긴 채 배포하면 DevTools가 열린 사용자 환경에서 실행이 멈춘다.

## 직접 확인

1. 임의의 공개 사이트에서 Network 탭을 열고 새로고침한 뒤, XHR/Fetch만 필터링해 가장 느린 요청 한 건을 골라 Timing 탭의 TTFB 값을 적어 본다. 그 값이 전체 응답 시간의 몇 퍼센트인지 계산한다.
2. 본인 프로젝트에서 클릭 시 살짝 버벅이는 동작을 하나 골라 Performance를 녹화하고, 가장 긴 Task(50ms 이상)의 이름과 소요 시간을 기록한 뒤 그 함수가 어느 컴포넌트에서 호출되는지 콜 스택으로 역추적한다.

## 스스로 답하기

1. API 응답 상태 코드가 200인데 화면이 갱신되지 않는다. Network 탭과 Console 중 무엇을 먼저 보고, 각각에서 무엇을 확인하겠는가?
2. 조건부 중단점과 `console.log`를 같은 디버깅에 쓸 때, 어떤 상황에서 조건부 중단점이 더 효율적인가?
3. Performance 탭에서 "Recalculate Style"과 "Layout" 막대가 반복적으로 길게 찍힌다면, 코드의 어떤 패턴을 의심하고 어떻게 고치겠는가?

## 내 프로젝트 연결

Fit의 WebRTC 연결이 실패할 때는 Console에서 `RTCPeerConnection`의 `iceconnectionstatechange` 이벤트 로그와 시그널링 메시지를 먼저 확인하고, ICE 후보 교환이 어느 단계에서 끊겼는지(checking에서 멈췄는지, failed로 갔는지) 본다. 시그널링 서버와의 WebSocket 프레임은 Network 탭의 WS 항목에서 주고받은 메시지를 시간순으로 펼쳐 SDP offer/answer가 양쪽에 도달했는지 검증한다.

OAuth 콜백 오류는 Network 탭에서 콜백 요청을 찾아 Headers의 요청 파라미터(`code`, `state`)와 응답 상태 코드를 확인하고, 토큰 교환 요청의 응답 본문에서 에러 메시지를 읽는다. redirect_uri 불일치인지, state 검증 실패인지가 응답에서 드러난다.

다음 버그를 만나면 AI에 묻기 전에 DevTools에서 Network 응답과 Console 상태를 먼저 확인해 가설을 참/거짓으로 판정하고, 어긋난 지점을 데이터로 좁힌 뒤 질문 범위를 줄인다.

## Related

- [[../_MOC]]
- [[../browser/렌더링-파이프라인]]
- [[../performance/core-web-vitals/웹-성능-측정]]
- [[../_roadmap/_MOC]]

## Sources

- Chrome DevTools docs
- MDN: Firefox/Chrome debugger
