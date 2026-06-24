---
title: 호이스팅과 TDZ
aliases:
  - hoisting
  - 호이스팅
  - TDZ
  - temporal dead zone
type: concept
status: budding
created: 2026-06-23
updated: 2026-06-23
tags:
  - fe/javascript
  - status/budding
related:
  - "[[_MOC]]"
  - "[[const-let-var]]"
  - "[[실행-컨텍스트-메모리]]"
  - "[[study/_MOC]]"
source:
  - "MDN: Hoisting"
  - "MDN: let (Temporal dead zone)"
---

# 호이스팅과 TDZ

> TL;DR: 선언은 코드 실행 전에 스코프 최상단으로 끌어올려진다. var는 undefined로 초기화돼 선언 전 접근이 가능하지만, let/const는 선언 줄에 도달하기 전까지 TDZ에 묶여 접근 시 ReferenceError를 던진다.

## What

호이스팅은 함수/변수 선언이 컴파일 단계에서 스코프 최상단으로 끌어올려지는 동작이다. 실행 컨텍스트는 생성 단계(creation phase)와 실행 단계(execution phase)로 나뉜다. 생성 단계에서 엔진이 스코프 안의 선언을 먼저 메모리에 등록한다.

선언 종류별로 등록 방식이 다르다.

- `var`: 메모리에 등록 + `undefined`로 초기화. 선언 전에 읽으면 undefined.
- `function` 선언문: 함수 전체가 메모리에 올라감. 선언 전에 호출 가능.
- `let` / `const`: 메모리에 등록되지만 초기화되지 않음. 선언 줄에 도달해야 값이 들어간다. 그 전 구간이 TDZ(Temporal Dead Zone).

TDZ는 스코프 시작점부터 변수가 초기화되는 줄까지의 구간이다. 이 구간에서 해당 변수를 읽거나 쓰면 `ReferenceError: Cannot access 'x' before initialization`이 발생한다.

## Why it matters

`var`로 선언한 변수를 선언 전에 참조해도 에러 없이 `undefined`가 나오기 때문에, 오타나 선언 위치 실수가 런타임 에러 대신 조용한 버그로 이어진다. `let`/`const`는 같은 실수를 ReferenceError로 즉시 드러낸다. 면접에서는 "var와 let의 차이", "선언 전에 변수에 접근하면 어떻게 되는가", "함수 선언문과 표현식의 호이스팅 차이"를 묻는다. 실무에서는 반복문 안 `var` 클로저 버그, 모듈 상단에서의 참조 순서 문제로 부딪힌다.

## How

**var는 undefined로 초기화된다**:
```js
console.log(a); // undefined (에러 아님)
var a = 1;
console.log(a); // 1

// 엔진이 보는 순서:
// var a;          (생성 단계: undefined로 초기화)
// console.log(a); // undefined
// a = 1;          (실행 단계: 할당)
```

**let/const는 TDZ에 묶인다**:
```js
console.log(b); // ReferenceError: Cannot access 'b' before initialization
let b = 1;

console.log(c); // ReferenceError
const c = 2;
```

**함수 선언문 vs 함수 표현식**:
```js
hoisted();    // "동작함" — 함수 전체가 호이스팅됨
function hoisted() {
  console.log("동작함");
}

notYet();     // TypeError: notYet is not a function
var notYet = function () {
  console.log("표현식");
};
// var notYet은 undefined로 초기화된 상태라 호출하면 TypeError
```

함수 표현식을 `let`/`const`로 선언하면 호출 시 TDZ 때문에 ReferenceError가 난다.

## Pitfalls

**typeof도 TDZ를 못 피한다**: 선언 없는 식별자에 `typeof`를 쓰면 `"undefined"`가 나오지만, TDZ 안의 변수는 ReferenceError를 던진다.
```js
typeof undeclared; // "undefined" (선언 자체가 없음)

typeof d;          // ReferenceError
let d = 1;
```

**같은 스코프 매개변수 기본값에서의 TDZ**:
```js
function f(x = y, y = 2) {} // x 평가 시 y는 아직 TDZ
f(); // ReferenceError
```

**반복문 var 클로저**: `var`는 함수 스코프라 반복 변수가 하나만 공유된다.
```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i)); // 3, 3, 3
}
for (let j = 0; j < 3; j++) {
  setTimeout(() => console.log(j)); // 0, 1, 2 — let은 반복마다 새 바인딩
}
```

## 직접 확인

1. 빈 `.js` 파일에 `console.log(x); let x = 1;`을 쓰고 `node` 또는 브라우저 콘솔에서 실행해, 에러 메시지가 정확히 `Cannot access 'x' before initialization`인지 확인한다. 같은 코드를 `var x`로 바꿔 `undefined`가 나오는지 비교한다.
2. `for (var i = 0; i < 3; i++) setTimeout(() => console.log(i))`를 실행해 출력이 `3 3 3`인지 확인하고, `var`를 `let`으로 바꿔 `0 1 2`로 달라지는지 측정한다. 왜 바인딩 개수가 달라지는지 한 줄로 적어본다.

## 스스로 답하기

1. `var`는 선언 전에 접근하면 undefined가 나오는데, let/const는 왜 같은 위치에서 ReferenceError를 던지는가? 두 경우 모두 호이스팅은 일어나는가?
2. 함수 선언문은 호출을 먼저 써도 동작하는데, `const fn = () => {}`로 선언한 함수는 왜 선언 전에 호출하면 에러가 나는가?
3. `typeof`는 선언되지 않은 변수에 "undefined"를 돌려주는데, TDZ 안의 변수에 쓰면 왜 에러가 나는가?

## 내 프로젝트 연결

본인 코드에서 `const`/`let`만 쓰고 `var`를 안 쓴다면, 그 이유를 TDZ로 설명할 수 있는지 점검한다. TDZ 덕분에 선언 전 참조가 에러로 즉시 잡히므로 조용한 undefined 버그가 줄어든다. 과거 `var`를 쓴 코드가 있다면 반복문 안 setTimeout/콜백 클로저로 같은 변수가 공유되는 버그를 재현해보고, `let`으로 바꿨을 때 출력이 어떻게 달라지는지 비교한다.

## Related

- [[_MOC]]
- [[const-let-var]]
- [[실행-컨텍스트-메모리]]
- [[study/_MOC]]

## Sources

- MDN: Hoisting
- MDN: let (Temporal dead zone)
