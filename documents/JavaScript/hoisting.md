# 💻 호이스팅(Hoisting)

<br />

## 👨🏻‍💻 호이스팅이란?

- 자바스크립트에서 호이스팅이란, 자바스크립트 엔진이 변수와 함수의 메모리 공간을 선언 전에 미리 할당하는 것을 의미한다. var로 선언한 변수의 경우 호이스팅 시에 `undefined`로 변수를 초기화한다. 반면 let, const로 선언한 변수의 경우 `호이스팅 시 변수를 초기화하지 않는다.`
- 현상적으로 접근하자면, 코드가 실행하기 전 변수/함수선언 이 해당 스코프의 최상단으로 끌어올려지는 것을 말한다.

<br />

## 👨🏻‍💻 호이스팅 특징

- 자바스크립트 엔진은 소스 코드를 한 줄씩 순차적으로 실행(런타임)하기에 앞서 먼저 소스 코드의 평가 과정을 거치면서 소스 코드를 실행하기 위한 준비(실행 컨텍스트를 위한 과정)를 한다.
- 위 과정에서 변수 선언을 포함한 `모든 선언문(변수, 함수 선언문)`을 소스 코드에서 찾아내 먼저 실행한다.
  - 이때 주의할 점은 `변수 선언`은 소스 코드가 순차적으로 실행되는 `런타임 이전`에 먼저 실행되지만 `변수 값의 할당(초기화)`는 소스 코드가 순차적으로 실행되는 시점인 `런타임`에 실행된다.
  - 따라서, 코드 실행 전에 이미 변수/함수 선언이 되어있기 때문에 선언문보다 참조/호출이 먼저 나와도 오류 없이 동작하는 것이다.
  - 오류 없이 동작하는건 정확히는 `var`와 `함수 선언문`만 해당
- 사실 `var`, `let`, `const`, `function`, `function*`, `class` 키워드를 사용해서 선언하는 모든 식별자는 호이스팅이 된다.
  - 왜? 모든 선언문은 런타임 이전 단계에서 먼저 실행되기 때문이다.
  - 하지만 위에서도 언급했듯이 let과 const는 블록 스코프의 최상단으로 호이스팅되어 선언은 되지만, 값이 할당 전까지 어떠한 값으로도 초기화되지 않는다. 따라서 var로 선언한 변수는 선언 전에 사용해서 에러가 발생하지 않지만 let, const는 `ReferenceError`가 발생한다.

<br />

## 👨🏻‍💻 호이스팅 예제

```js
// 예제1(var)
console.log(test1); // undefined

test1 = "gromit";

var test1;
console.log(test1); // gromit
```

<br />

```js
// 예제2.1(let)
console.log(test2); // ReferenceError
let test2;
```

```js
// 예제2.2(let)
let test3 = "test3";
console.log(test3); // test3
```

<br />

```js
// 예제3 function 선언문
func(); // Hello
function func() {
  console.log("Hello");
}
```

<br />

```js
// 예제4 function 표현식
func(); // TypeError: func is not a function
var func = function () {
  console.log("World");
};
```

<br />

```js
// 예제5 generator
console.log(genterator); // [GeneratorFunction: genterator]
function* genterator() {}
```

<br />
