# 💻 JSX(JavaScript XML)

## 👨🏻‍💻 JSX

- JSX(JavaScript XML)는 `Javascript에 XML을 추가한 확장한 문법이다.`
- JSX는 리액트로 프로젝트를 개발할 때 사용되므로 공식적인 자바스크립트 문법은 아니다.
- 브라우저에서 실행하기 전에 `바벨`을 사용하여 일반 자바스크립트 형태의 코드로 변환된다.
- 자바스크립트에서 HTML 작성하듯이 하기 때문에 가독성이 높고 작성하기 쉽다.
- 개발자가 JSX를 작성하면 리액트 엔진은 JSX를 기존 자바스크립트로 해석한다. 이를 `선언형 화면 기술`이라고 한다.

<br />

## 👨🏻‍💻 JSX 문법

- 반드시 부모 요소 하나가 감싸 있는 형태여야 한다.

```jsx
// 정상 코드 1(<div></div>)
function App() {
  return (
    <div>
      <div>Hello</div>
      <div>GodDaeHee!</div>
    </div>
  );
}

// 정상 코드 2(<React.Fragment></React.Fragment>)
function App() {
  return (
    <React.Fragment>
      <div>Hello</div>
      <div>GodDaeHee!</div>
    </React.Fragment>
  );
}

// 정상 코드(<></>)
function App() {
  return (
    <>
      <div>Hello</div>
      <div>GodDaeHee!</div>
    </>
  );
}
```

<br />

- JSX 안에서도 `{}` 를 사용해 자바스크립트 표현식을 작성할 수 있다.

```jsx
function App() {
  const name = "JeonMinjae";

  return (
    <div>
      <div>Hello</div>
      <div>{name}!</div>
    </div>
  );
}
```

<br />

- if문과 for문 대신 `삼항 연산자`나 `&& 연산자`를 이용한 조건부 렌더링

```jsx
function App() {
  const name = "react";

  return (
    <div>
      <div>Hello</div>
      <div>{name === "react" ? <h1>True</h1> : <h1>False</h1>}</div>
    </div>
  );
}
```

<br />

- JSX에서 자바스크립트 문법을 쓰려면 `{}`를 사용해야 되기 때문에, 스타일을 적용할 때에도 객체 형태로 넣어주어야 한다. 또한 camelCase 프로퍼티 명명 규칙을 사용한다.

```jsx
function App() {
  const name = "JeonMinjae";

  return (
    <div>
      <div>Hello</div>
      <div style={{ fontSize: "12px" }} className="name">
        {name}
      </div>
    </div>
  );
}
```

<br />

## 참고

- https://www.notion.so/a42647e064864e469b66acacfe69652b
