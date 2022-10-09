# 💻 React Hooks

## 👨🏻‍💻 React Hook?

- 리액트 훅은 `React 16.8 버전`에서 새롭게 도입된 기능이다. 기존에 클래스 컴포넌트에는 상태 관리나 라이프사이클의 기능이 있었지만, 함수형 컴포넌트에는 그런 기능들이 존재하지 않았다. 하지만 Hook이 도입되면서 함수형 컴포넌트에서도 `상태 관리`할 수 있는 useState나 `렌더링 직후 작업`을 설정할 수 있는 useEffect 등의 기능들을 사용할 수 있게 됬다.
- 리액트 훅이 도입되서 클래스 기반 컴포넌트, 라이프 사이클 메서드, this의 필요성이 사라졌다. 또한, 공통 기능을 커스텀 hook으로 만들어서 로직을 재사용하기 쉬워졌다. 마지막으로 컴포넌트 자체에서 로직을 분리할 수 있어서 읽기 쉽고 테스트하기 쉬운 코드를 작성할 수 있다.

<br />

## 👨🏻‍💻 React Hook 종류

### useState

```jsx
import React, { useState } from "react";

const [data, setData] = useState("");
```

- 대표적인 Hook이다. 함수형 컴포넌트에서도 `가변적인 상태`를 지닐 수 있게 해주며, 함수형 컴포넌트에서 `상태를 관리`해야 할 때 사용한다.
- useState()라는 함수는 `배열`을 리턴하도록 되어있다. 따라서 구조분해 할당 방식으로 할당 할 수 있으며, 첫 번째는 `State의 값`, 두 번째는 `State 변경 함수`이다.

```
상태관리란?
일반적으로 상태관리라 함은변화하는 데이터들을 관리하는 것인데, 상태의 초기 값을 저장하거나,
현재 상태의 값을 읽거나, 새로운 데이터로 상태를 업데이트 하는 등의 행위를 뜻한다.
```

<br />

### useEffect

```jsx
import React, { useEffect } from "react";

useEffect(() => {
  // ...
}, []);
```

- useEffect는 라이플 사이클 메서드와 관려이 있다. 기존 클래스형 컴포넌트의 라이플 사이클 메서드 중 `componentDidMount`와 `componentDidUpdate`, `componentWillUnmount` 를 합친 형태라고 생각하면 된다.
- 처음 컴포넌트가 `마운트` 될 때 한 번 동작한다. → `componentDidMount`
- useEffect의 두번째 인자인 `의존성 배열`로 지정한 state의 값이 변화할 때마다 동작한다. → `componentDidUpdate`
- useEffect 내부에서 return을 통해 `componentWillUnmount` 메서드도 사용할 수 있다. 이를 `뒷정리 함수`라고도 한다.
- 만약, useEffect의 두번째 인자인 의존성 배열을 아에 입력하지 않으면 state가 바뀔 때마다 동작하기 때문에 비효율적이다.
- 또한, 의존성 배열을 `빈 배열`로 넣는 경우에는 마운트가 된 후 `딱! 한번만` 작동한다.

<br />

### useLayoutEffect

```jsx
import React, { useEffect } from "react";

useLayoutEffect(() => {
  // ...
}, []);
```

- useLayoutEffect는 useEffect와 비교해서 이해하면 편리하다.
- useEffect는 컴포넌트들이 render되고, paint 후에 즉, `Mount(마운트)`될 때 `비동기적으로 실행`된다. paint된 후에 실행되기 때문에 useEffect에서 DOM에 영향을 주는 코드가 있으면 사용자 입장에서는 `깜빡이는 현상`을 경험한다.
- 그에 반해, useLayoutEffect는 컴포넌트들이 render된 후에 실행되고 그 후에 paint한다. 또한 이런 과정이 `동기적`으로 실행된다. 따라서 paint 되기전에 실행되기 때문에 dom 을 조작하는 코드가 존재하더라도 사용자는 깜빡임을 경험하지 않습니다.
- 이렇게만보면 useLayoutEffect가 useEffect보다 더 좋게 느껴질 수 있겠지만, 반대로 useLayoutEffect의 내부 로직이 복잡하면 사용자 입장에서는 화면을 보는데까지 시간이 오래걸린다는 단점이 있다.
- 결론은, 기본적으로는 useEffect를 사용하는 것을 권장하고, 화면이 깜빡이는 상황일 때 이를 방지하기위해서는 useLayoutEffect를 사용하면 좋을 것 같다.

<br />

### useRef

```jsx
import React, { useRef } from "react";

const ref = useRef(null);
```

- 리액트로 작업하다 보면 `DOM 요소에 직접 접근`해야 할 때가 있다. 예를 들어 특정 DOM 요소에 focus를 주거나 DOM 요소의 크기나 스크롤 위치를 알고 싶은 경우이다. 이때 ref 속성을 이용하면 DOM 요소에 직접 접근할 수 있다.
- ref.current 속성을 통해서 직접 접근이 가능하다.
- 이외에도, `값이 변해도 리렌더링하지 않는 변수`를 관리하는 용도로도 사용할 수 있다.

<br />

### useCallback

```jsx
import React, { useCallback } from "react";

const func = useCallback(() => {
  //...
}, []);
```

- 컴포넌트가 렌더링 될 때마다 `함수`를 새로 생성하지 않고 `재사용`하고, 두 번째 인자인 `의존성 배열에 State 값`이 변경되었을 때만 새로 생성하도록 해서 최적화할 수 있는 Hook이다.
- `메모이제이션 훅`이다. `메모이제이션`이란 계산 된 값을 자료 구조에 저장하고 이후 같은 계산을 반복하지 않고 자료 구조에서 꺼내 재사용하는 것을 말한다.

<br />

### useMemo

```jsx
import React, { useMemo } from "react";

const value = useMemo(() => {
  //...
}, []);
```

- `특정 결과 값`을 재사용할 때 사용하는 Hook이다. 두 번째 인자인 의존성 배열에 State 값이 변경되었을 때만 연산하므로 최적화가 개선된다.
- useCallback과 마찬가지로 `메모이제이션 훅`이다. 둘의 차이는 `특정 결과의 값`을 재사용하냐, `함수`를 재사용하냐 차이가 있다.

<br />

### useContext

- 기존의 React에 존재하는 Context API를 편하게 사용할 수 있게 해주는 Hook이다.

<br />

### useReducer

- 컴포넌트의 상태값을 리덕스의 `리듀서`처럼 관리할 수 있게 해주는 Hook이다.
- useReducer를 사용하면 컴포넌트의 `상태 업데이트 로직`을 컴포넌트에서 `분리`시킬 수 있다. 상태 업데이트 로직을 `컴포넌트 바깥`에 작성할 수도 있고, 심지어 다른 파일에 작성 후 불러와서 사용할 수도 있다.

<br />

## 참고

https://www.notion.so/a42647e064864e469b66acacfe69652b
