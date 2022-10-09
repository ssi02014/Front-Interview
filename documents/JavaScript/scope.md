# 💻 Scope

<br />

## 👨🏻‍💻 스코프(Scope)

- `스코프(Scope, 유효범위)`는 자바스크립트를 포함한 모든 프로그래밍 언어의 기본적인 개념이다.
- 스코프는 참조 대상 식별자(identifier, 변수, 함수의 이름과 같이 어떤 대상을 다른 대상과 구분하여 식별할 수 있는 유일한 이름)를 찾아내기 위한 규칙이다.
- 즉, 어떤 변수를 사용하거나 함수를 호출하려고 할 때 해당하는 식별자로 사용하는데, 그 `식별자를 검색하는 메커니즘`이라고 이해하면 된다.

<br />

```js
let x = "global";

function foo() {
  let x = "function scope";
  console.log(x);
}

foo();
console.log(x);
```

<br />

- 위 예제에서 전역에 선언한 변수 x는 어디에든 참조할 수 있다. 하지만 함수 foo 내에서 선언된 변수 x는 함수 foo 내에서만 참조할 수 있따. 이러한 규칙을 `스코프`라고 한다.

<br />

## 👨🏻‍💻 스코프의 구분

### 🏃 자바스크립트에서 스코프

- 전역 스코프(Global Scope): 코드 어디에서든지 참조할 수 있다.
- 지역 스코프(Local Scopr or Function-level Scope): 함수 코드 블록이 만든 스코프로 함수 자신과 하위 함수에서만 참조할 수 있다.

<br />

### 🏃 변수 관점에서 스코프

- 전역 변수(Global variable): 전역에서 선언된 변수이며 어디에든 참조할 수 있다.
- 지역 변수(Local variable): 지역 내에서 선언된 변수이며 그 지역과 그 지역의 하부 지역에서만 참조할 수 잇다.

<br />

## 👨🏻‍💻 자바스크립트 스코프의 특징

- 대부분의 C-family language는 `블록 레벨 스코프(block-level-scope)`를 따른다.
- `블록 레벨 스코프`란, 코드 블록({ ... })내에서 유효한 스코프를 의미한다. 여기서 `유효하다` 라는 것은 `참조 할 수 있다`는 뜻이다.

<br />

```C++
  int main(void) {
    // block-level scope
    if (1) {
      int x = 5;
      printf("x = %d\n", x);
    }

    //if문 내에서 선언된 변수 x는 if문 코드 블록 내에서만 유효하다.
    printf("x = %d\n", x); // use of undeclared identifier 'x'

    return 0;
}
```

<br />

- 자바스크립트는 `함수 레벨 스코프(function-level-scope)`를 따른다.
- `함수 레벨 스코프`란, 함수 코드 블록 내에서 선언된 변수는 함수 코드 블록 내에서만 유효하고 함수 외부에서는 유효하지 않다.
- 단, ECMAScript6 에서 도입된 `let` keyword는 블록 레벨 스코프를 사용할 수 있다.

<br />

## 👨🏻‍💻 전역 스코프

- 전역에 변수를 선언하면 이 변수는 어디서든지 참조할 수 있는 전역 스코프를 갖는 전역 변수가 된다.
- `var` 키워드로 선언한 전역 변수는 `전역 객체(Global Object) window`의 프로퍼티 이다.
- 자바스크립트는 다른 C-family language와는 달리 특별한 시작점이 없으며 코드가 나타나는 즉시 해석되고 실행된다. 따라서 전역에 변수를 선언하기 쉬우며 이것은 전역 변수를 남발하게 하는 문제를 야기 시킨다.
- 전역 변수의 사용은 `변수 이름이 중복`될 수 있고, 의도치 않은 재할당에 의한 상태 변화로 `코드를 예측하기 어렵게` 만드므로 사용을 지양해야 한다.

<br />

```js
var global = "global";

function foo() {
  var local = "local";
  console.log(global);
  console.log(local);
}
foo();

console.log(global);
console.log(local); // Uncaught ReferenceError: local is not defined
```

<br />

## 👨🏻‍💻 함수 레벨 스코프

- 자바스크립트 ECAMScript6 이전에 사용하던 `var` keyword는 함수 스코프 변수를 선언할 때 사용한다.
- 함수 밖에서 선언한 함수 스코프 변수는 전역 범위를 가지고, 함수 안에서 사용하면 함수 밖을 제외한 내부 어디서든 접근이 가능한다.

```js
var a = "global";

function foo() {
  var b = "local1";
  console.log(a); //global - 전역변수. 출력가능.

  if (true) {
    var c = "local2";
    console.log(b); //local1 - 해당 함수 내 선언한 변수. 출력 가능.
  }

  console.log(c); //local2 - 해당 함수 내 선언한 변수. 출력 가능.
}

function bar() {
  var d = "local3";
  console.log(d); //local3 - 해당 함수 내 선언한 변수. 출력 가능.
  console.log(a); //global - 전역변수. 출력가능.
  console.log(b); //해당 함수 내 선언한 변수가 아님. Error
  console.log(c); //해당 함수 내 선언한 변수가 아님. Error
}

foo();
bar();
```

<br />

## 👨🏻‍💻 블록 레벨 스코프

- 블록은 0개 이상의 구분(statement)을 묶기위해 사용하고, `중괄호 { }로 경계를 구분`한다.
- ECMAScript6부터 도입된 `let` keyword는 블록 스코프 변수를 선언할 때 사용한다.
- 블록 스코프 변수는 함수 밖에서 선언하면 함수 스코프 변수처럼 전역 접근할 수 있다. 블록 안에서 선언하면 자신을 정의한 블록과 하위 블록에서만 접근이 가능하다.

<br />

```js
let foo = "I'm foo";
if (true) {
  let bar = "I'm bar";
  console.log(foo); //I'm foo
  console.log(bar); //I'm bar
}

console.log(foo); //I'm foo
console.log(bar); //Uncaught ReferenceError: bar is not defined.
```

<br />

## 👨🏻‍💻 렉시컬 스코프(Lexical Scope)

```js
var x = 1;

function foo() {
  var x = 10;
  bar();
}

function bar() {
  console.log(x);
}

foo(); // ?
bar(); // ?
```

<br />

- 위 예제의 실행 결과는 함수 bar의 상위 스코프가 무엇인지에 따라 결정된다. 두가지 패턴을 예측할 수 있다.
- 첫 번째, 함수를 `어디서 호출`하였는지에 따라 상위 스코프를 결정 -> 함수 bar의 상위 스코프는 함수 foo와 전역
- 두 번째, 함수를 `어디서 선언`하였는지에 따라 상위 스코프를 결정 -> 함수 bar의 상위 스코프는 전역
- 프로그래밍 언어는 이 두가지 방식 중 하나의 방식으로 함수의 상위 스코프를 결정한다. 첫번째 방식을 `동적 스코프(Dynamic Scope)`라 하고, 두 번째 방식을 `렉시컬 스코프(Lexcal Scope)`또는 `정적 스코프(Static Scope)`라 한다.
- 자바스크립트를 비롯한 대부분의 프로그래밍 언어는 렉시컬 스코프를 따른다.
- 정리하면 위 예제에서 함수 bar는 전역에 선언되어있다. 따라서 함수 bar의 상위 스코프는 전역 스코프이고 위 예제는 전역 변수 x의 값 1을 두번 출력한다.

<br />

## 참고

https://poiemaweb.com/js-scope
https://eblee-repo.tistory.com/37
https://github.com/baeharam/Must-Know-About-Frontend/blob/master/Notes/javascript/scope.md
