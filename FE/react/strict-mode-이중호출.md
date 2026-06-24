---
title: StrictMode 이중 호출
aliases:
  - StrictMode
  - strict mode
  - 이중호출
  - 이중 렌더
  - double invoke
type: concept
status: budding
created: 2026-06-23
updated: 2026-06-23
tags:
  - fe/react
  - status/budding
related:
  - "[[_MOC]]"
  - "[[lifecycle-useEffect]]"
  - "[[리렌더링-트리거]]"
  - "[[study/_MOC]]"
source:
  - "react.dev: StrictMode"
  - "react.dev: Synchronizing with Effects (cleanup)"
---

# StrictMode 이중 호출

> TL;DR: 개발 모드의 `<StrictMode>`는 컴포넌트 함수와 effect를 일부러 두 번 실행해 순수성 위반과 클린업 누락을 마운트 시점에 드러낸다. 프로덕션 빌드에서는 한 번만 실행된다.

## What

`<StrictMode>`는 자식 트리에서 다음을 개발 모드에서만 추가로 실행한다.

- 컴포넌트 함수 본문(렌더 로직)을 두 번 호출
- `useState`, `useMemo`, `useReducer` 등의 초기화 함수를 두 번 호출
- effect를 setup → cleanup → setup 순서로 실행 (마운트 직후 한 번 더 정리하고 다시 설정)

목적은 두 가지다. 첫째, 렌더 함수와 초기화 함수는 순수해야 하는데 두 번 호출해 결과가 같은지 노출시킨다. 외부 변수를 변경하거나 매번 다른 값을 반환하면 두 번째 호출에서 표시가 난다. 둘째, effect에 cleanup이 빠졌거나 잘못 작성됐는지 마운트 시점에 드러낸다. React는 setup 직후 cleanup을 한 번 호출해 "언마운트 후 재마운트" 상황을 시뮬레이션한다.

프로덕션 빌드에서는 이 추가 호출이 전부 사라진다. 빌드 산출물에서 `<StrictMode>`는 아무 동작도 하지 않는다.

## Why it matters

개발 중 `console.log`가 두 번 찍히거나 fetch가 두 번 나가는 현상의 원인이 대부분 StrictMode다. 모르면 "버그"로 오인해 호출을 막는 임시 코드를 넣게 된다. 면접에서는 "왜 effect가 두 번 실행되나요", "그걸 끄면 되나요"라는 질문으로 이어지고, 끄는 대신 cleanup으로 해결할 수 있는지를 본다. 실무에서는 이벤트 리스너 등록, 구독, 타이머, 외부 라이브러리 인스턴스 바인딩처럼 setup이 누적되면 메모리 누수나 중복 바인딩이 되는 코드를 StrictMode가 미리 잡아준다.

## How

`<StrictMode>`로 트리를 감싸면 활성화된다.

```tsx
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";

createRoot(document.getElementById("root")!).render(
  <StrictMode>
    <App />
  </StrictMode>
);
```

cleanup이 있는 effect는 개발 모드에서 다음 순서로 실행된다.

```tsx
function ChatRoom({ roomId }: { roomId: string }) {
  useEffect(() => {
    const conn = createConnection(roomId);
    conn.connect();
    console.log("connect", roomId);
    return () => {
      conn.disconnect();
      console.log("disconnect", roomId);
    };
  }, [roomId]);
  return <h1>{roomId} 입장</h1>;
}
```

마운트 시 콘솔 출력 순서:

```
connect general      // 1차 setup
disconnect general   // StrictMode가 강제한 cleanup
connect general      // 2차 setup
```

`connect`와 `disconnect`가 짝이 맞으므로 연결이 하나만 살아남는다. cleanup이 setup을 정확히 되돌리면 두 번 실행돼도 최종 상태는 한 번 실행과 같다.

순수성 위반은 렌더 두 번 호출로 드러난다.

```tsx
let renderCount = 0; // 외부 변수 변경은 순수성 위반

function Bad() {
  renderCount += 1; // StrictMode 개발 모드에서 한 번 렌더에 2씩 증가
  return <p>{renderCount}</p>;
}
```

## Pitfalls

cleanup을 빼면 setup이 두 번 누적되고, 두 연결 중 하나가 정리되지 않은 채 남는다.

```tsx
useEffect(() => {
  const conn = createConnection(roomId);
  conn.connect();
  // return 없음 → disconnect 호출 안 됨
}, [roomId]);
// 출력: connect / connect  → 연결 2개 중 1개 누수
```

호출을 막으려고 플래그로 우회하면 StrictMode가 잡으려던 버그를 그대로 덮는다.

```tsx
// 안티패턴: cleanup 누락을 가린다
const ran = useRef(false);
useEffect(() => {
  if (ran.current) return; // 두 번째 setup 차단
  ran.current = true;
  createConnection(roomId).connect();
}, [roomId]);
```

이 플래그는 roomId가 바뀌어 effect가 다시 실행돼야 할 때도 막아버려, 실제 상황에서 새 연결이 생기지 않는다. 올바른 해법은 cleanup에서 정리하는 것이다. 또한 `useState`의 초기화 함수도 두 번 호출되므로, 초기화에 부수 효과(전역 카운터 증가, 로깅, 외부 등록)를 넣으면 두 번 발생한다.

## 직접 확인

1. `createRoot` 호출부에서 `<StrictMode>`를 한 번은 감싸고 한 번은 벗긴 상태로, 위 `ChatRoom` effect의 콘솔 출력 횟수를 직접 비교한다. cleanup이 있을 때와 없을 때 각각 `connect`/`disconnect`가 몇 번 찍히는지 기록한다.
2. `npm run build` 후 빌드 산출물을 `npm run preview`(또는 정적 서버)로 띄워, 같은 effect의 콘솔 출력이 개발 모드와 어떻게 달라지는지 횟수로 확인한다.

## 스스로 답하기

1. StrictMode가 effect를 setup → cleanup → setup으로 실행하는 이유는 무엇이고, 어떤 종류의 버그를 노출시키려는 것인가?
2. fetch가 두 번 나가는 문제를 ref 플래그로 막는 방식과 cleanup으로 처리하는 방식은 roomId가 바뀌는 상황에서 어떻게 다르게 동작하는가?
3. 프로덕션에서 한 번만 실행된다면 개발 모드의 이중 호출은 무엇을 보장해 주는가?

## 내 프로젝트 연결

chatGraph의 D3 그래프를 데이터 조인으로 재설계하면서, svg 프레임과 forceSimulation을 만드는 마운트 effect에 cleanup(simulation.stop과 컨테이너 정리)을 넣었다. StrictMode 개발 모드의 setup → cleanup → setup 이중 마운트에서, cleanup이 이전 시뮬레이션을 멈추고 DOM·ref를 정리하므로 두 번째 setup이 깨끗한 상태에서 다시 생성된다. cleanup이 없으면 첫 시뮬레이션이 멈추지 않고 두 번째와 겹쳐 노드가 떨리거나 이벤트가 중복 바인딩된다. StrictMode를 끄는 우회 대신 effect를 정리 가능하게(idempotent) 만드는 게 정석이다. 끄는 대신 cleanup으로 고친다면 effect가 어떤 형태여야 하는지 직접 설계해보라. (과거 MindGraph는 D3 시절 reactStrictMode를 꺼서 우회했지만, 지금은 그래프 엔진이 Cytoscape로 이관됐다.)

## Related
- [[_MOC]]
- [[lifecycle-useEffect]]
- [[리렌더링-트리거]]
- [[study/_MOC]]

## Sources
- react.dev: StrictMode
- react.dev: Synchronizing with Effects (cleanup)
