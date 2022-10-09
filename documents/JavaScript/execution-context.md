# 💻 Execution Context

<br />

## 👨🏻‍💻 실행 컨텍스트(Execution Context)

- 실행 컨텍스트는 `코드의 실행 환경`에 대한 여러가지 정보(Scope, Hoisting, this, function, closure 등)를 담고있는 개념이다.
- 간단히 말하면 `자바스크립트 엔진`에 의해 만들어지고 사용되는 코드 정보를 담은 `객체의 집합`이라고 할 수 있다.
- 실행 컨텍스트를 바로 이해하지 못하면 코드 독해가 어려워지며 디버깅도 매우 곤란해 질 것이다.

### 🏃 종류

- 자바스크립트에서 실행 가능한 코드는 3가지로 이루어져 있다.
- 전역 코드, 함수 코드가 일반적으로 실행 가능한 코드이다.

<br />

```
1. 전역 코드: 전역 영역에 존재하는 코드
2. 함수 코드: 함수 내에 존재하는 코드
3. Eval 코드: eval()로 실행되는 코드
```

<br />

- 자바스크립트 엔진은 코드를 실행하기 위하여 실행에 필요한 여러가지 정보를 알고 있어야 한다.
- 이러한 `실행에 필요한 정보`들을 형상화하고 구분하기 위해 자바스크립트 엔진은 실행 컨텍스트를 `객체`의 형태로 관리한다.

<br />

```
1. 변수: 전역 변수, 지역 변수, 매개 변수, 객체의 프로퍼티
2. 함수 선언
3. 변수의 유효범위 (Scope)
4. this
```

<br />

- 1. 자바스크립트 엔진이 파일을 실행하기 전에 `글로벌 실행 컨텍스트(Global Execution Context, GEC)`가 생성된다.
- 2. 그리고 함수를 호출할 때마다 `함수 실행 컨텍스트(Function Execution Context, FEC)`가 생성된다.
- 이때 주의할 점은, 글로벌의 경우 `실행 이전`에 생성되지만, 함수의 경우 `호출할 때` 생성된다는 것이다.

<br />

## 👨🏻‍💻 실행 컨텍스트 스택(Exectuion Context Stack)

- 실행 컨텍스트가 생성되면 흔히 `콜 스택(Call Stack)`이라고 불리는 `실행 컨텍스트 스택`에 쌓이게 된다.
- `GEC`는 코드를 실행하기 전에 쌓이고, 모든 코드를 실행하면 제거된다.
- `FEC`는 함수를 호출할 때 쌓이고 호출이 끝나면 제거된다.

```js
var x = "xxx";

function foo() {
  var y = "yyy";

  function bar() {
    var z = "zzz";
    console.log(x + y + z);
  }
  bar();
}
foo();
```

- 위 코드를 실행하면 아래와 같이 실행 컨텍스트 스택이 생성되고 소멸한다.
- 현재 실행 중인 컨텍스트에서 해당 컨텍스트와 관련 없는 코드(ex. 다른 함수)들은 실행되면 새로운 컨텍스트가 생성 된다.
- 이 컨텍스트는 스택에 쌓이게 되고 컨트롤(제어권)이 이동한다.

![실행컨텍스트스택](https://user-images.githubusercontent.com/64779472/120208197-25b5f080-c268-11eb-9e5a-eb3da3b96eed.PNG)

<br />

## 👨🏻‍💻 실행 컨텍스트 구성 요소

- 실행 컨텍스트는 `Lexical Environment`, `Variable Environment`, `this 바인딩` 3개의 구성요소를 갖는다.

<br />

### 🏃 Lexical Environment

- Lexical Environment는 `변수 및 함수 등의 식별자(Identifier) 및 외부 참조`에 관한 정보를 갖고 있는 컴포넌트이다. 이 컴포넌트는 `Environment Record`, `outer 참조` 2개의 구성요수를 갖는다.
- Environment Record가 식별자에 관한 정보를 갖고 있으며, outer 참조는 외부 Lexical Environment를 참조하는 포인터인다.
- 좀 더 풀어쓰자면 Environment Record는 `최초의 변수`, `Arguments`, `함수 선언`들을 저장한다.
- outer는 `부모 Environment(reference)`를 저장한다.
- 실행 컨텍스트는 생성 될 때, Lexical Environment와 Variable Environment의 구성 요소는 동일한 값을 가지나, 컨텍스트 내에서 코드를 실행하는 동안 Variable Environment와 달리 Lexical Environment의 구성요소의 값은 변경될 수 있다.

```js
var x = 10;

function foo() {
  var y = 20;
  console.log(x);
}
```

- 위와 같은 코드가 있을 때는 아래와 같이 Lexical Environment가 형성된다.

<br />

```js
  globalEnvironment = {
    environmentRecord = { x: 10 },
    outer: null
  }

  fooEnvironment = {
    environmentRecord = { y: 20 },
    outer: globalEnvironment
  }
```

- 따라서, `foo()` 에서 `x`를 참조할 때는 fooEnvironment의 Environment Record를 찾아보고, 없기 때문에 outer 참조를 사용하여 외부의 Lexical Environment에 속해 있는 Environment Record를 찾아보는 방식이다.

<br />

### 🏃 Variable Environment

- Variable Environment는 Lexical Environment와 동일한 성격을 갖지만 `var`로 선언된 변수만 저장한다는 점에서 다르다.
- 즉, Lexical Environment는 `var`를 제외한, `let`, `함수 선언문`, `함수 매개 변수`들을 저장한다.
- 코드에 의해 새로운 변수/함수가 추가되더라도 절대 값이 변하지 않는다.
- [코드 참고](https://stackoverflow.com/questions/23948198/variable-environment-vs-lexical-environment/45788048#45788048)

<br />

### 🏃 this 바인딩

- this의 바인딩은 실행 컨텍스트가 생성될 때마다 this 객체에 `어떻게 바인딩이 되는지`를 나타낸다. 즉, 실행 컨텍스트의 `this 키워드의 반환 값`을 저장한다.
- this의 키워드는 `현재 컨텍스트가 참조하고 있는 객체`를 가리키며, 함수 호출 패턴에의해 결정 된다.
- ES6부터는 this의 바인딩이 Lexical Environment 안에 있는 Environment Record 안에서 일어난다는 것을 기억하자.(그렇게 중요하지는 않다.)
- GEC의 경우
  - Strict Mode라면 `undefined`로 바인딩 된다.
  - Strict Mode가 아니라면 글로벌 객체로 바인딩 된다.(브라우저에선 Window, 노드에선 Global)
- FEC의 경우
  - 해당 함수가 어떻게 호출되었는지에 따라 바인딩 된다.

<br />

## 👨🏻‍💻 과정

- Execution Context는 2가지 과정을 거친다.
- Creation Phase(생성 단계), Execution Phase(실행 단계)

### 🏃 생성 단계

- 생성 단계는 다시 3단계로 이루어진다.
- Lexical Environment 생성, Variable Environment 생성, this 바인딩
- 주의할 점은 값이 변수에 매핑되지 않는다는 것이다. `var`의 경우 `undefined`로 초기화되고, `let`이나 `const`는 아무 값도 가지지 않는다.

<br />

### 🏃 실행 단계

- 코드를 실행하면서 변수에 값을 매핑시킨다. 예시를 보자

```js
var a = 3;
let b = 4;

function func(num) {
  var t = 9;
  console.log(a + b + num + t);
}

var r = func(4);
```

<br />

- GEC의 생성 단계, 여기서 생성이 될 때 실행 컨텍스트 스택에 쌓인다.

```js
  GEC {
    ThisBinding: window,
    LexicalEnvironment: {
      EnvironmentRecord: {
        b: <uninitialized>,
        func: func(){...}
      },
      outer: null
    },
    VariableEnvironment: {
      EnvironmentRecord: {
        a: undefined,
        r: undefined
      },
      outer: null
    }
  }
```

<br />

- GEC의 실행 단계

```js
  GEC {
    ThisBinding: window,
    LexicalEnvironment: {
      EnvironmentRecord: {
        b: 4,
        func: func(){...}
      },
      outer: null
    },
    VariableEnvironment: {
      EnvironmentRecord: {
        a: 3,
        r: undefined
      },
      outer: null
    }
  }
```

- 이후에 `func()`을 호출하고 FEC를 생성한다.

<br />

- FEC의 생성 단계

```js
  FEC {
    ThisBinding: window,
    LexicalEnvironment: {
      EnvironmentRecord: {
        arguments: { num: 4, length: 1 },
      },
      outer: GEC의 LexicalEnvironment
    },
    VariableEnvironment: {
      EnvironmentRecord: {
        t: undefined
      },
      outer: GEC의 LexicalEnvironment
    }
  }
```

<br />

- FEC의 실행 단계

```js
  FEC {
    ThisBinding: window,
    LexicalEnvironment: {
      EnvironmentRecord: {
        arguments: { num: 4, length: 1 },
      },
      outer: GEC의 LexicalEnvironment
    },
    VariableEnvironment: {
      EnvironmentRecord: {
        t: 9
      },
      outer: GEC의 LexicalEnvironment
    }
  }
```

- FEC가 스택에서 제거 되고 GEC의 `r`이 20으로 초기화 된다.

<br />

```js
  GEC {
    ThisBinding: window,
    LexicalEnvironment: {
      EnvironmentRecord: {
        b: 4,
        func: func(){...}
      },
      outer 참조: null
    },
    VariableEnvironment: {
      EnvironmentRecord: {
        a: 3,
        r: 20
      },
      outer 참조: null
    }
  }
```

- 모든 코드를 실행하고 GEC가 스택에서 제거된 뒤 프로그램이 종료된다.
- [코드 참고](https://miro.medium.com/max/1100/1*SBP65hdVDW5j0LuVryTiXw.gif)를 참고하면 더 확실히 이해할 수 있다.

<br />

## 참고

https://github.com/baeharam/Must-Know-About-Frontend/blob/master/Notes/javascript/execution-context.md
https://minjung-jeon.github.io/Execution-Context/
https://velog.io/@imacoolgirlyo/JS-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%9D%98-Hoisting-The-Execution-Context-%ED%98%B8%EC%9D%B4%EC%8A%A4%ED%8C%85-%EC%8B%A4%ED%96%89-%EC%BB%A8%ED%85%8D%EC%8A%A4%ED%8A%B8-6bjsmmlmgy
https://poiemaweb.com/js-execution-context
