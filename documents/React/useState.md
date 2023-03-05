# 💻 useState 비동기 동작

- 리액트로 개발을 할 때 useState 훅을 이용하면 컴포넌트에 상탯값을 쉽게 관리 할 수 있다.
- useState 훅이 반환하는 배열의 두 번째 요소는 `상태값 변경 함수`다.

```js
const [state, setState] = useState(0);
```

- 리액트는 상탯값 변경 함수가 호출되면 해당 컴포넌트를 리렌더링한다. 아래는 리액트 컴포넌트가 리렌더링되는 조건이다.

```
1. state가 변경되었을 때
2. props가 변경되었을 때
3. 부모 컴포넌트가 렌더링 될 때
4. forceUpdate()를 실행할 때
```

- 리렌더링 과정에서 자식 컴포넌트도 같이 렌더링된다. 그래서 리액트는 렌더링 최적화를 위해 상탯값 변경을 비동기, 배치로 처리한다.

<br />

### 배치란?

- 배칭은 React가 더 나은 성능을 위해 여러 개의 state 업데이트를 하나의 리렌더링 (re-render)로 묶는 것을 의미한다.
- 아래와 예시를 보자.

```jsx
const App = () => {
  const [number, setNumber] = useState(0);

  const onClick = (e) => {
    setNumber(number + 1); // 아직 업데이트 X
    setNumber(number + 1); // 아직 업데이트 X
  };

  // 리액트는 onClick 함수가 완전히 종료되야 리렌더링 함

  console.log("render");
  return (
    <>
      <p>{number}</p>
      <button onClick={onClick}>더하기</button>
    </>
  );
};
```

- 위 코드를 보면 onClick 함수를 호출하면 number 상탯값을 두 번 증가시키려고 했다. 하지만 우리의 의도와 달리 number의 값은 1만 증가한다.

  - 이는 상탯값 변경 함수가 비동기, 배치로 동작하기 때문이다. 리액트는 효율적으로 렌더링하기 위해 여러 개의 상탯값 변경 요청을 배치로 묶어서 처리한다.
  - 따라서 onClick 함수가 호출되어도 console.log("render")도 1번만 출력된다.

- 리액트가 상탯값 변경 함수를 동기로 처리하면 하나의 상탯값 변경 함수가 호출될 때마다 화면을 다시 그리기 때문에 성능 이슈가 생길 수 있다.
  - 상탯값 변경 함수가 동기로 동작하지만 매번 화면을 다시 그리지 않는다면, UI데이터와 화면 간의 불일치가 발생해서 혼란스러울 수 있다.

<br />

### 해결책

- 이러한 상태 변화가 1번만 일어나는 것을 방지하고, 비동기로 동작하지만 상탯값 변경 함수가 호출 될 때마다 해당 상태를 변경하고 싶으면 상탯값 변경 함수로 `콜백 함수`를 넣는 방식이 있다.

```jsx
const App = () => {
  const [number, setNumber] = useState(0);

  const onClick = (e) => {
    setNumber((prev) => prev + 1);
    setNumber((prev) => prev + 1);
  };

  console.log("render");
  return (
    <>
      <p>{number}</p>
      <button onClick={onClick}>더하기</button>
    </>
  );
};
```

- 위와 같이 작성하면 배치 처리되서 1회만 리렌더링 되는 것은 맞는데, 기존과 다르게 onClick이 1회 호출하면, 상태값은 1만 증가하는 것이 아닌 2가 증가한다.
- 이유는 상탯값 변경 함수로 입력된 함수는 `자신이 호출되기 직전의 상탯값을 매개변수`로 받는다. 이 코드에서는 첫 번째 호출에서 변경된 상탯값이 두 번째 호출의 콜백함수 prev 인수로 사용된다. 따라서 이렇게 작성하면 number는 2가 증가한다.

<br />

### 근본적으로 왜 1만 증가하는 걸까?

```js
function useState(initialState) {
  var dispatcher = resolveDispatcher();
  return dispatcher.useState(initialState);
}
```

- React의 useState 함수이다. 이 함수는 `resolveDispatcher`라는 함수가 반환하는 객체의 useState라는 메서드를 실행하여 반환되는 값을 리턴한다.

```js
function resolveDispatcher() {
  var dispatcher = ReactCurrentDispatcher.current;

  {
    if (dispatcher === null) {
      error("Invalid hook call...");
    }
  }

  return dispatcher;
}
```

- resolveDispatcher 함수는 다시 `ReactCurrentDispatcher`라는 객체의 `current` 속성을 반환한다.

```js
var ReactCurrentDispatcher = {
  /**
   * @internal
   * @type {ReactComponent}
   */
  current: null,
};
```

- 이때 주목할 점은 `ReactCurrentDispatcher`가 객체라는 점이다.
- 객체이기 때문에 동일한 key 값에 대하여 이전의 값을 계속해서 덮어쓴다. 결국에는 마지막 명령어만 수행되는 셈이다. 아래처럼.

```js
const num = 1;
const obj1 = { num: 1 };
const obj2 = Object.assign(
  {},
  { num: num + 1 },
  { num: num + 1 },
  { num: num + 1 }
);

console.log(obj); // { num: 1 }
console.log(obj2); // { num: 2 }
```
