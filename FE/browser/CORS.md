---
title: CORS
aliases:
  - cors
  - 교차 출처
  - preflight
  - SOP
  - same-origin policy
type: concept
status: budding
created: 2026-06-23
updated: 2026-06-23
tags:
  - fe/browser
  - status/budding
related:
  - "[[../_MOC]]"
  - "[[브라우저-저장소]]"
  - "[[FE/_Roadmap/_MOC]]"
source:
  - "MDN: CORS"
  - "MDN: Same-origin policy"
---

# CORS

> TL;DR: 브라우저는 동일 출처 정책(SOP)으로 다른 출처의 응답 접근을 막고, 서버가 `Access-Control-Allow-Origin` 헤더로 허용을 명시해야 교차 출처 요청 결과를 읽을 수 있다.

## What

출처(origin)는 `scheme + host + port` 세 가지가 모두 같을 때만 동일하다. `https://a.com`과 `https://a.com:8080`은 포트가 달라 다른 출처이고, `http://a.com`과 `https://a.com`도 scheme이 달라 다른 출처다.

동일 출처 정책(Same-Origin Policy, SOP)은 한 출처에서 로드된 스크립트가 다른 출처의 응답을 읽지 못하게 막는 브라우저 보안 규칙이다. CORS(Cross-Origin Resource Sharing)는 서버가 특정 출처에 한해 SOP를 완화하도록 허용하는 HTTP 헤더 기반 메커니즘이다.

요청 자체는 보통 서버까지 전달되지만, 서버 응답에 허용 헤더가 없으면 브라우저가 응답을 JS에 넘기지 않고 차단한다. 차단 주체는 서버가 아니라 브라우저다.

## Why it matters

FE에서 API 서버 도메인이 프론트 도메인과 다를 때 거의 항상 마주친다. `fetch`로 받은 응답이 콘솔에 `blocked by CORS policy`로 찍히면 SOP에 걸린 것이다. 네트워크 탭에서 요청은 200으로 보이는데 JS에서 응답을 못 읽는 상황이 전형적인 신호다.

면접에서는 출처의 정의, preflight 발생 조건, `Access-Control-Allow-Credentials`와 와일드카드(`*`)를 함께 못 쓰는 이유를 묻는다.

## How

서버가 허용 출처를 응답 헤더로 명시한다.

```js
// 서버(Express) - 특정 출처만 허용
app.use((req, res, next) => {
  res.setHeader("Access-Control-Allow-Origin", "https://front.example.com");
  res.setHeader("Access-Control-Allow-Methods", "GET, POST, PUT, DELETE");
  res.setHeader("Access-Control-Allow-Headers", "Content-Type, Authorization");
  next();
});
```

단순 요청(simple request)은 preflight 없이 바로 전송된다. 조건은 메서드가 `GET`, `HEAD`, `POST` 중 하나이고, 헤더가 `Accept`·`Accept-Language`·`Content-Language`·`Content-Type` 정도로 제한되며, `Content-Type`이 `text/plain`·`multipart/form-data`·`application/x-www-form-urlencoded` 중 하나일 때다.

이 조건을 벗어나면 브라우저가 본 요청 전에 `OPTIONS` 메서드로 preflight를 먼저 보낸다.

```js
// 클라이언트 - application/json + Authorization 헤더 → preflight 발생
fetch("https://api.example.com/posts", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    Authorization: "Bearer token",
  },
  body: JSON.stringify({ title: "hi" }),
});
```

위 요청의 실행 순서:

1. 브라우저가 `OPTIONS https://api.example.com/posts`를 보냄 (`Access-Control-Request-Method: POST`, `Access-Control-Request-Headers: content-type, authorization` 포함)
2. 서버가 `Access-Control-Allow-Methods`, `Access-Control-Allow-Headers`로 허용 여부를 응답
3. 허용되면 브라우저가 실제 `POST`를 전송
4. 허용 안 되면 실제 요청 없이 차단

쿠키나 인증 정보를 함께 보낼 때:

```js
// 클라이언트
fetch("https://api.example.com/me", { credentials: "include" });
```

```js
// 서버 - credentials 허용 시 Origin을 와일드카드로 두면 안 됨
res.setHeader("Access-Control-Allow-Origin", "https://front.example.com");
res.setHeader("Access-Control-Allow-Credentials", "true");
```

## Pitfalls

`credentials: include`와 `Access-Control-Allow-Origin: *`는 함께 동작하지 않는다. 인증 정보를 보내면 서버가 출처를 정확한 값으로 응답해야 한다.

```js
// 동작 안 함: credentials 요청에 와일드카드 응답
res.setHeader("Access-Control-Allow-Origin", "*");
res.setHeader("Access-Control-Allow-Credentials", "true");
// → 브라우저가 응답 차단
```

`Authorization` 같은 커스텀 헤더를 보내면서 서버 `Access-Control-Allow-Headers`에 해당 헤더를 안 넣으면 preflight 단계에서 막힌다. 응답 본문이 200이어도 JS는 응답을 못 읽는다.

포트만 달라도 다른 출처다. `localhost:3000`(프론트)에서 `localhost:8080`(API)로 요청하면 CORS 대상이다.

## 직접 확인

1. `localhost:3000`에서 React 앱을 띄우고 `localhost:8080`의 Express 서버로 `fetch` POST(`Content-Type: application/json`)를 보낸다. 서버에서 CORS 헤더를 빼고 한 번, 넣고 한 번 호출해 네트워크 탭에서 `OPTIONS` 요청 유무와 차단 메시지를 비교한다.
2. 같은 요청을 `Content-Type: text/plain`으로 바꿔 보내고, `OPTIONS` preflight가 사라지는지 네트워크 탭에서 확인한다.

## 스스로 답하기

- `https://a.com`, `https://a.com:8080`, `http://a.com` 세 URL 중 동일 출처는 어느 것끼리이고 왜인가?
- 단순 요청과 preflight 요청을 가르는 조건은 무엇이고, `application/json` body는 어느 쪽인가?
- `Access-Control-Allow-Credentials: true`일 때 `Access-Control-Allow-Origin`을 `*`로 둘 수 없는 이유는 무엇인가?

## 내 프로젝트 연결

xAB에서 로드밸런서 뒤에 둔 OAuth 콜백이 출처 오류로 실패했다. 직접 설명할 포인트는 두 가지다. 첫째, 클라이언트는 `https://app.example.com`으로 접속했지만 LB가 내부 인스턴스로 요청을 넘기면서 백엔드가 받은 `Host`가 내부 호스트로 바뀌어, 백엔드가 만든 콜백 URL의 출처가 실제 사용자 출처와 어긋났다. 둘째, LB가 원래 출처를 `X-Forwarded-Host` 헤더로 전달하고 있었으므로, 콜백 출처를 만들 때 `Host` 대신 `X-Forwarded-Host`를 우선 참조하도록 바꿔 사용자가 처음 접속한 출처를 복원했다. 왜 프록시 뒤에서 출처가 어긋났는지, 어떤 헤더로 원래 출처를 되살렸는지 코드 경로까지 짚어 말할 수 있어야 한다.

## Related

- [[../_MOC]]
- [[브라우저-저장소]]
- [[FE/_Roadmap/_MOC]]

## Sources

- MDN: CORS
- MDN: Same-origin policy
