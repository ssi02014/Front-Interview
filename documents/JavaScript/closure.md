# 💻 클로저(Closure)

<br />

## 👨🏻‍💻 클로저(Closure)

- **클로저(closure)** 는 함수와 그 함수가 선언됐을 때의 `렉시컬 환경(Lexical environment)`과의 `조합`이라고 부르며, 내부 함수가 외부함수 변수에 액세스(접근) 할 수 있는 자바스크립트의 기능을 말한다.
- **클로저(closure)** 는 반환된 내부 함수가 자신이 `선언`되었을 때의 렉시컬 스코프 환경을 `기억`하여, 자신이 선언됐을 때의 환경(스코프) 밖에서 호출되어도 그 환경(스코프)에 접근할 수 있는 함수 **왜? 메모리가 여전히 기억하고 있기 때문**

<br />

### 🏃 렉시컬 스코프(Lexical scope) 예시

- 렉시컬 스코프는 함수를 `어디서 선언`하였는지에 따라 상위 스코프를 결정하는 방식이다.

```js
function init() {
  var name = "Mozilla"; // name은 init에 의해 생성된 지역 변수이다.

  function displayName() {
    // displayName() 은 내부 함수이며, 클로저다.
    alert(name); // 부모 함수에서 선언된 변수를 사용한다.
  }

  displayName();
}
init();
```

- init()은 `지역 변수 name`과 `함수 displayName()`을 생성한다.
- displayName()은 init() 안에 정의된 내부 함수이며 init() 함수 본문에서만 사용할 수 있다.
- 여기서 주의할 점은 displayName() 내부엔 자신만의 지역 변수가 없다는 점이다. 그런데 함수 내부에서 외부 함수의 변수에 접근할 수 있기 때문에 displayName() 역시 부모 함수 init()에서 선언된 변수 name에 접근할 수 있다.

<br />

- 위 예시를 통해 함수가 중첩된 상황에서 `파서`가 어떻게 변수를 처리하는지 알 수 있다. 이는 `어휘적 범위 지정(lexical scoping)`의 한 예이다.
- 중첩된 함수는 외부 범위(scope)에서 선언한 변수에도 접근할 수 있다.

<br />

### 🏃 클로저(Closure) 예시1

```js
function outer() {
  var a = 2;

  function inner() {
    console.log(a);
  }

  return inner;
}

var func = outer();
func(); // 2
```

- 여기서 `GC(Garbage Collector)`가 `outer()` 의 참조를 없앨 것 같지만 내부함수인 `inner()` 가 해당 스코프의 변수인 `a`를 참조하고 있기 때문에 없애지 않는다.
- 따라서 스코프 외부에서 `inner()`가 실행되도 해당 `스코프를 기억하기 때문에 2를 출력`하게 된다. 즉, 여기서 `클로저`는 inner()가 되며 func 에 담겨 밖에서도 실행되도 렉시컬 스코프를 기억한다.
- 한 눈에 봐서는 이 코드가 여전히 작동하는 것이 직관적으로 보이지 않을 수 있다. 몇몇 프로그래밍 언어에서, 함수 안의 지역 변수들은 그 함수가 처리되는 동안에만 존재한다. 즉, `outer()` 실행이 끝나면(inner함수가 리턴되고 나면) a변수에 더 이상 접근할 수 없게 될 것으로 예상하는 것이 일반적이다.
- 하지만 위의 예시와 자바스크립트의 경우는 다르다. 그 이유는 자바스크립트는 함수를 리턴하고, 리턴하는 함수가 `클로저`를 형성하기 때문이다. 클로저는 `함수와 함수가 선언된 어휘적 환경의 조합`이다. 이 환경은 클로저가 `생성된 시점의 유효 범위 내에 있는 모든 지역 변수`로 구성된다.

<br />

### 🏃 클로저(Closure) 예시2

```js
function func() {
  for (var i = 1; i < 5; i++) {
    setTimeout(() => {
      console.log(i);
    }, i * 500);
  }
}
func(); // 5 5 5 5
```

- 위 예시는 클로저를 사용하는 대표적인 예시이다.
- 코드의 의도한 바는 1부터 4까지 간격을 두고 출력하는 것이었지만 5가 4번 출력된다.
- 그 이유는? setTimeout() 을 반복문 안에서 돌리면 콜백함수가 계속해서 `task queue`에 쌓이게 되고 반복문이 끝나고 나서!! `call stack`으로 돌아와서 실행된다.
- 콜백 함수는 `클로저`이기 때문에 상위 스코프에게 i의 값을 물어보고 상위 스코프인 func 의 스코프에선 i가 5까지 증가했기 때문에 5가 4번 출력된다.

<br />

### 🏃 클로저(Closure) 예시2의 해결방안

- **블록 레벨 스코프로 해결하기**

```js
function func() {
  for (let i = 1; i < 5; i++) {
    setTimeout(() => {
      console.log(i);
    }, i * 500);
  }
}
func(); // 1 2 3 4
```

- 함수 레벨 스코프가 아닌 블록 레벨 스코프인 `let`을 사용한다.
- `let` 을 사용하면 for문 내의 새로운 스코프를 갖기 때문에 매 반복마다 새로운 i 가 선언되고, 반복이 끝난 이후의 값으로 초기화가 된다.
- 따라서, setTimeout()의 클로저인 콜백함수가 i를 참조하기 위해 상위 스코프를 검색할 때 `블록 레벨 스코프`에서 매 반복마다 선언 및 초기화 된 i를 참조하는 것이다.

<br />

## 참고

https://github.com/baeharam/Must-Know-About-Frontend/blob/master/Notes/javascript/closure.md <br />
https://developer.mozilla.org/ko/docs/Web/JavaScript/Closures <br />
https://jhleed.tistory.com/150 <br />
