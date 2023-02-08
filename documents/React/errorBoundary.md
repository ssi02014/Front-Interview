# 💻 ErrorBoundary

## 👨🏻‍💻 ErrorBoundary?

- UI의 일부분에 존재하는 `자바스크립트 에러가 전체 애플리케이션을 중단시켜서는 안된다.` 리액트는 이 문제를 해결하기 위해 React 16에서 `에러 경계(ErrorBoundary)`를 도입했다.
- ErrorBoundary는 하위 컴포넌트 트리의 어디에서든 자바스크립트 에러를 기록하며, 깨진 컴포넌트 대신 `Fallback UI`를 보여주는 리액트 컴포넌트이다.
- ErrorBoundary는 렌더링 도중 라이프 사이클 메서드 및 그 아래에 있는 전체 트리에서 에러를 잡아낸다.

<br />

### ErrorBoundary 사용 이유

- `선언적`으로 에러 제어
- 에러가 발생하더라도 전체 애플리케이션을 중단하지 않고, 대체 UI(Fallback)를 보여주기 위함
- 오류 경계는 try-catch 블록을 사용할 수 없는 상황에서 꽤나 유용하다.

```
선언형이란? 어떻게(How)보다 무엇을(What)에 집중
즉, 결과물에만 집중하고, 복잡한 과정은 추상화합니다.
명령형의 경우 한 줄씩 읽어 나가면서 다음에 어떤 일이 발생할지 추측해야 한다.
반면에 선언형의 경우 자세한 방법을 모르더라도 코드만 보고도 어떤 일이 발생할지 예측이 단숨에 가능하다.
```

<br />

### ErrorBoundary가 잡아내지 못하는 에러

- 이벤트 핸들러 내에서 발생하는 오류
- 비동기 코드 내에서 발생하는 오류
- 서버 측 렌더링 중에 발생하는 오류
- 하위 컴포넌트가 아닌 ErrorBoundary(에러 경계) 자체에서 발생하는 에러

<br />

### ErrorBoundary의 위치

- 최상위 컴포넌트에 감싸서 에러를 제어할 수도 있지만, 각 위젯을 독립적으로 ErrorBoundary로 감싸서 애플리케이션의 나머지 부분이 충돌하지 않도록 보호할 수 도 있다.
- ErrorBoundary의 세분화된 부분은 개발자에게 달려있다.

<br />

### ErrorBoundary 기본 예시

```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // 다음 렌더링에서 폴백 UI가 보이도록 상태를 업데이트 합니다.
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    // 에러 리포팅 서비스에 에러를 기록할 수도 있습니다.
    logErrorToMyService(error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      // 폴백 UI를 커스텀하여 렌더링할 수 있습니다.
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children;
  }
}
```

- 리액트 공식문서에서 제공해주는 클래스형으로 구현한 ErrorBoundary이며, 생명주기 메서드인 static getDerivedStateFromError와 componentDidCatch를 사용한다.
- 에러 발생한 뒤에 폴백 UI 렌더링을 하려면 `static getDerivedStateFromError`를 사용
  - 해당 생명주기 메서드는 `하위의 자손 컴포넌트`에서 오류가 발생했을 때 호출됩니다. 이 메서드는 매개변수로 오류를 전달받고, `갱신된 state 값을 반드시 반환`해야 합니다.
- 에러 정보를 기록하려면 `componentDidCatch`를 사용, componentDidCatch는 자손 컴포넌트에서 오류가 발생했을 때에 호출되며, 2개의 매개변수를 전달받습니다.
  - error: 발생한 오류
  - info: 어떤 컴포넌트가 오류를 발생시켰는지에 대한 정보를 포함한 componentStack 키를 갖고있는 객체

<br />

```jsx
<ErrorBoundary>
  <MyComponent />
</ErrorBoundary>
```

- 그리고 위와 같이 일반 컴포넌트로서 사용할 수 있다.

<br />

### react-error-boundary

- 참고로 이런 에러바운더리를 직접 클래스형으로 작성해서 사용해도 좋지만, `react-error-boundary`라는 라이브러리를 통해서도 해당 기능을 구현할 수 있다.
- [react-error-boundary](https://github.com/bvaughn/react-error-boundary)
