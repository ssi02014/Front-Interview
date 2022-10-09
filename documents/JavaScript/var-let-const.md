# 💻 var vs let vs const

<br />

## 👨🏻‍💻 var, let, const 차이점

### 🏃 스코프(Scope)

- var는 `함수 레벨 스코프(Function Level Scope)`
- 함수 레벨 스코프는 함수 내에서 선언된 변수는 함수 내에서만 유효하며 함수 외부에서는 참조할 수 없다. 즉, `함수 내부에서 선언한 변수는 지역 변수`이며 `함수 외부에서 선언한 변수는 모두 전역 변수`이다.
- let과 const는 `블럭 레벨 스코프(Block Level Scope)`
- 블록 레벨 스코프는 모든 코드 블록({ ... })(즉, 함수, if문, for문, while문, try/catch문 등)내에서 선언된 변수는 코드 블록 내에서만 유효하며 코드 블록 외부에서는 참조할 수 없다. 즉, `코드 블록 내부에서 선언한 변수는 지역 변수`이며, `코드 블록 외부에서 선언한 변수는 전역 변수`이다.

```js
var foo = "Foo";
let bar = "Bar";

console.log(foo, bar); //Foo, Bar

{
  let bazz = "Bazz";
  console.log(bazz); //Bazz
}

console.log(bazz); // ReferenceError
```

<br />

### 🏃 호이스팅(Hoisting)

- `호이스팅`은 코드에 선언된 변수 및 함수를 코드 `최상단`으로 끌어올리는 것을 말한다.
- 함수 내에 선언 된 함수 범위의 변수는 해당 함수 최상단으로 끌어올려지고, 함수 외부에 선언한 전역 범위의 변수는 스크립트의 최상단으로 끌어올려진다.
- var는 함수 스코프의 최상단으로 `호이스팅` 되고 선언과 동시에 `undefined 로 초기화` 된다.
- let과 const는 블록 스코프의 최상단으로 호이스팅 되어 선언만 되고, `값이 할당되기 전까지 어떤 값으로도 초기화되지 않는다.` 따라서 var로 선언한 변수는 선언 전에 사용해도 에러가 나지 않지만 let, const는 `ReferenceError`가 발생합니다.

```js
function run() {
  console.log(foo); // undefined

  var foo = "Foo";

  console.log(foo); // Foo
}

run();
```

<br />

```js
function checkHoisting() {
  console.log(foo); // ReferenceError

  let foo = "Foo";

  console.log(foo); // Foo
}

checkHoisting();
```

<br />

- var, let은 변수 선언시 초기 값을 주지 않아도 되지만 const는 `반드시 초기값을 할당`해야 합니다.
- var, let은 `재할당이 가능`하다.

```js
    const foo;
    foo = "Foo"; //Error

    let foo;
    foo = "Foo" //정상 작동
```

<br />

### 🏃 글로벌 객체 바인딩

- strict mode가 아니라는 가정 하에 var는 글로벌 스코프에서 선언되었을 경우 `글로벌 객체에 바인딩된다.`
- strict mode가 아니라는 가정 하에, let과 const는 글로벌 스코프에서 선언되었을 경우 `글로벌 객체에 바인딩되지 않는다.`

```js
var foo = "Foo"; // global scope
let bar = "Bar"; // global scope

console.log(window.foo); // Foo
console.log(window.bar); // undefined
```

<br />

### 🏃 재선언(Redeclaration)

- var는 `재선언이 가능`하다.
- let과 const는 `재선언이 불가능하다.`

```js
var foo = "foo1";
var foo = "foo2"; // 문제없음

let bar = "bar1";
let bar = "bar2"; // SyntaxError: Identifier 'bar' has already been declared
```

<br />

## 참고

https://stackoverflow.com/questions/762011/whats-the-difference-between-using-let-and-var
https://github.com/baeharam/Must-Know-About-Frontend/blob/master/Notes/javascript/var-let-const.md
https://medium.com/@yeon22/javascript-var-let-const%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90-9fab5c264c9c
