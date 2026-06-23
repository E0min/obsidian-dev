---
title: Reconciliation과 key
aliases: [reconciliation, diffing, virtual dom, key, 재조정, 가상돔]
type: concept
status: budding
created: 2026-06-23
updated: 2026-06-23
tags: [fe/react, status/budding]
related:
  - "[[_MOC]]"
  - "[[리렌더링-트리거]]"
  - "[[lifecycle-useEffect]]"
  - "[[../_roadmap/_MOC]]"
source: ["react.dev: Preserving and Resetting State", "react.dev: Rendering Lists (keys)"]
---

# Reconciliation과 key

> TL;DR: React는 렌더마다 만든 새 엘리먼트 트리를 이전 트리와 비교(reconciliation)해 바뀐 부분만 DOM에 반영한다. 비교는 트리의 같은 위치를 기준으로 하고, 같은 위치·같은 타입이면 DOM 노드와 state를 재사용하며, 타입이 다르면 폐기 후 새로 마운트한다. 리스트는 위치 대신 key로 항목을 식별한다.

## What

렌더가 일어나면 React는 컴포넌트를 호출해 새 엘리먼트 트리를 만든다. 이전 렌더의 트리와 새 트리를 비교해 무엇이 달라졌는지 계산하고, 달라진 노드만 실제 DOM에 적용한다. 이 비교 과정이 reconciliation이고, 비교에 쓰는 메모리상의 엘리먼트 트리가 virtual DOM이다.

비교 규칙:

- **같은 위치 + 같은 타입**: DOM 노드를 재사용하고 변경된 prop만 갱신한다. 컴포넌트라면 state도 유지된다.
- **같은 위치 + 다른 타입**(`<div>` → `<span>`, `Counter` → `Profile`): 기존 서브트리 전체를 unmount(state 폐기, effect cleanup 실행)하고 새 타입을 mount한다.
- **위치가 바뀐 형제 노드들**(리스트): 기본은 배열 인덱스 순서로 같은 위치끼리 비교한다. `key`를 주면 위치 대신 key로 같은 항목을 찾아 매칭한다.

핵심은 "위치"가 식별 기준이라는 점이다. React는 컴포넌트를 이름이나 내부 데이터로 추적하지 않고, 부모 트리에서 어느 자리에 렌더됐는지로 추적한다.

## Why it matters

- 조건부 렌더로 같은 자리에 다른 컴포넌트를 번갈아 그리면 state가 의도와 다르게 유지되거나 초기화된다.
- 리스트 렌더에서 key를 잘못 주면 입력값·체크 상태·스크롤 위치가 다른 항목으로 옮겨 붙는다. 무한 스크롤·드래그 정렬·필터 토글에서 자주 터진다.
- "key에 index 쓰지 마라"는 면접 단골이다. 이유를 동작 순서로 설명할 수 있어야 한다.
- 의도적으로 state를 초기화하고 싶을 때 key를 바꾸는 기법(remount)도 같은 원리에서 나온다.

## How

### 1. 같은 위치·같은 타입이면 state 유지

```tsx
function App() {
  const [isFancy, setIsFancy] = useState(false);
  return (
    <div>
      {isFancy ? (
        <Counter isFancy={true} />
      ) : (
        <Counter isFancy={false} />
      )}
      <button onClick={() => setIsFancy(!isFancy)}>toggle</button>
    </div>
  );
}
```

`isFancy`를 바꿔도 두 분기 모두 같은 위치의 `Counter`다. 타입이 같으므로 React는 같은 인스턴스로 보고 내부 count state를 유지한다. prop만 `isFancy` true/false로 갱신된다.

### 2. 타입이 다르면 폐기 후 재마운트

```tsx
{isPaused ? <p>일시정지</p> : <Counter />}
```

`isPaused`가 토글될 때마다 `<p>`와 `<Counter>`는 타입이 다르다. `<Counter>` → `<p>` 전환에서 Counter는 unmount되어 count state가 사라지고, 다시 `<p>` → `<Counter>`로 돌아오면 count가 0부터 시작한다.

### 3. 리스트의 key

```tsx
{users.map((user) => (
  <li key={user.id}>{user.name}</li>
))}
```

key는 형제 항목들 사이에서 항목을 식별하는 ID다. 항목이 추가·삭제·재정렬돼도 React는 같은 key를 가진 엘리먼트를 같은 항목으로 매칭해, 해당 DOM 노드와 컴포넌트 state를 그대로 따라가게 한다. key는 전역이 아니라 같은 부모 안의 형제들 사이에서만 유일하면 된다.

### 4. key를 바꿔 의도적으로 state 초기화

```tsx
<Chat key={selectedUserId} contact={selectedUser} />
```

대화 상대가 바뀔 때 입력 중이던 메시지를 비우고 싶으면 `key`에 상대 id를 준다. id가 바뀌면 key가 바뀌고, React는 이전 `<Chat>`을 폐기하고 새로 마운트해 내부 state를 초기화한다.

## Pitfalls

### key에 배열 index 쓰기

```tsx
// 안티패턴: 순서가 바뀌는 리스트
{todos.map((todo, index) => (
  <TodoItem key={index} todo={todo} />
))}
```

index를 key로 쓰면 "key = 자리 번호"가 되어 위치 기반 매칭과 같아진다. 항목이 앞에 추가되거나 정렬·필터로 순서가 바뀌면 같은 index에 다른 데이터가 들어온다. React는 index가 같으니 같은 항목으로 보고 DOM 노드와 state를 재사용한다.

버그 재현:

```tsx
function List() {
  const [items, setItems] = useState(["A", "B", "C"]);
  return (
    <>
      <button onClick={() => setItems(["Z", ...items])}>맨 앞 추가</button>
      <ul>
        {items.map((label, index) => (
          // key={index} 이므로 각 input의 내부 state가 index에 묶인다
          <li key={index}>
            {label} <input defaultValue={`${label}의 메모`} />
          </li>
        ))}
      </ul>
    </>
  );
}
```

실행 순서:

1. 첫 렌더에서 index 0/1/2의 input에 각각 A/B/C의 메모를 적는다.
2. "맨 앞 추가"를 누르면 배열이 `["Z", "A", "B", "C"]`가 된다.
3. React는 index 0을 같은 항목으로 보고 기존 input(=A의 메모를 담은 DOM 노드)을 재사용한다. 화면 라벨은 "Z"로 바뀌지만 input 안에는 A에 적었던 메모가 그대로 남는다.
4. 결과적으로 메모가 한 칸씩 밀려 엉뚱한 항목에 붙는다.

`key={index}`를 `key={항목 고유 id}`로 바꾸면 React가 Z를 새 항목으로, A/B/C를 기존 항목으로 매칭해 input state가 올바른 항목을 따라간다.

### 렌더할 때마다 새 key 생성

```tsx
<li key={Math.random()}>{item.name}</li>
```

매 렌더마다 key가 달라지면 React는 모든 항목을 매번 다른 항목으로 보고 전부 unmount/remount한다. state가 매번 초기화되고 DOM이 통째로 다시 그려져 성능이 나빠진다.

### 안정적 key의 조건

- 데이터에서 나오는 고유 id(DB id, UUID 등)를 쓴다.
- 같은 항목은 렌더가 바뀌어도 같은 key를 유지한다.
- 같은 부모의 형제들 사이에서 유일하다.
- 렌더 중 즉석에서 만들지 않는다(`Math.random()`, 매번 새로 만드는 객체 참조 금지).
- 적당한 고유값이 없으면 데이터 생성 시점에 id를 부여해 데이터에 저장한다.

## 직접 확인

1. 위 `List` 컴포넌트를 그대로 만들고, input 3개에 서로 다른 글자를 적은 뒤 "맨 앞 추가"를 눌러 메모가 밀리는지 확인한다. 그다음 `key={index}`만 `key`를 항목 고유 id로 바꾸고 같은 조작을 반복해 메모가 제자리에 남는지 비교한다.
2. React DevTools의 Components 탭에서 항목을 선택하고 리스트를 재정렬해 본다. 안정적 key일 때는 선택된 컴포넌트가 같은 항목을 따라가고, `key={index}`일 때는 같은 자리(index)에 남아 다른 데이터로 바뀌는지 관찰한다.

## 스스로 답하기

1. 조건부로 같은 위치에 `<Counter />`와 `<p>`를 번갈아 렌더하면 Counter의 state는 유지되는가 초기화되는가, 그 이유는 무엇인가?
2. 리스트에서 `key={index}`가 정적 리스트에서는 문제없다가 정렬·앞쪽 삽입이 생기면 버그가 되는 이유를 동작 순서로 설명하라.
3. 대화 상대가 바뀔 때 입력창을 비우고 싶다. state를 수동으로 비우는 방법과 `key`를 바꾸는 방법은 각각 어떻게 동작하며 무엇이 다른가?

## 내 프로젝트 연결

- xAB 무한 스크롤 리스트에서 각 항목 key가 무엇인지 확인한다. index거나 페이지 안에서만 유일한 값이면, 다음 페이지를 이어 붙일 때 key 충돌이나 재마운트가 생길 수 있다. 항목별 서버 id 같은 전역 고유값을 key로 쓰는지 점검한다.
- chatGraph 라우팅에서 같은 컴포넌트가 경로만 바뀌어 렌더되는 자리를 찾는다. 같은 위치·같은 타입이면 React가 인스턴스를 재사용해 이전 화면의 state(스크롤·입력·선택)가 남는다. 라우트 파라미터가 바뀔 때 화면을 새로 시작해야 한다면 해당 컴포넌트에 `key={경로 파라미터}`를 줘 재마운트를 강제할지 판단한다.
- 두 리스트 모두 "같은 항목은 항상 같은 key, 다른 항목은 항상 다른 key"가 지켜지는지 데이터 흐름을 따라 확인한다.

## Related
- [[_MOC]]
- [[리렌더링-트리거]]
- [[lifecycle-useEffect]]
- [[../_roadmap/_MOC]]

## Sources
- react.dev: Preserving and Resetting State
- react.dev: Rendering Lists (keys)
