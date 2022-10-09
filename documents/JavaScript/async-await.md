# 💻 async/await

<br />

## 👨🏻‍💻 async/await 이란?

- async/await는 `ES8(ECMAScript2017)`의 공식 스펙으로 비교적 최근에 정의된 문법이다.
- async/await를 사용하면 비동기 코드를 작성할 때 비교적 쉽고 명확하게 코드를 작성할 수 있다.
- 자바스크립트는 `싱글 스레드 프로그래밍 언어`이기 때문에 비동기처리가 필수적이다.
- 비동기 처리는 그 결과가 언제 반환될지 알 수 없기 때문에 이를 동기식으로 처리하는 기법들이 사용되어야 한다. 대표적으로 `setTimeout`,`Callback`,`Promise`이다.
- 위 3가지 기법들도 훌륭하지만 문제점이 존재한다. async/await는 이를 해결함과 동시에 사용법이 간단해졌다.

<br />

## 👨🏻‍💻 async 키워드

- async 키워드는 항상 function 앞에 위치합니다.

```js
async function f() {
  return 1;
}

console.log(f()); // Promise { 1 }
console.log(f().then()); // Promise { <pending> }
f().then((res) => console.log(res)); //1
```

- 🌟 function 앞에 async를 붙이면 해당 함수는 항상 Promise를 반환한다.
- 🌟 Promise가 아닌 값을 반환하더라도 `이행 상태의 프라미스(resolved promise)`로 값을 감싸 이행된 Promise가 반환되도록 한다.

<br />

```js
async function f() {
  return Promise.resolve(1);
}

console.log(f()); // Promise { <pending> }
console.log(f().then()); // Promise { <pending> }
f().then((res) => console.log(res)); // 1
```

- 위 코드와 같이 명시적으로 Promise를 반환하는 것도 가능한데, 결과는 거의 동일하다.

<br />

## 👨🏻‍💻 await 키워드

- 자바스크립트는 await 키워드를 만나면 Promise가 `처리(Settled)`될 때까지 기다린다. 결과는 그 이후 반환된다.

```js
async function f() {
  let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("완료!"), 1000);
  });
  let result = await promise; // 프라미스가 이행될 때까지 기다림 (*)

  console.log(result); // "완료!"
}

f();
```

- 위 코드에서 함수를 호출하고, 함수 본문이 실행되는 도중에 `(*)`로 표시한 줄에서 실행이 잠시 `중단`되었다가 Promise가 처리되면 실행이 재개된다.
- 이때 프라미스 객체의 결과 값이 변수 result에 할당 된다. 따라서 위 코드를 실행하면 1초 뒤에 `완료!`가 출력된다.

<br />

- 🌟 `await(기다리다라는 뜻을 가진 영단어)`는 말 그대로 Promise가 처리될 때까지 함수 실행을 기다리게 만든다.
- Promise가 처리 되면 그 결과와 함께 실행이 재개된다. Promise가 처리되길 기다리는 동안엔 `엔진이 다른 일(다른 스크립트 실행, 이벤트 처리 등)`을 할 수 있기 때문에 CPU 리소스가 낭비되지 않는다.
- await은 `promise.then()`보다 좀 더 세련되게 프로미스의 결과 값을 얻을 수 있다.

<br />

## 👨🏻‍💻 async/await 기본 예제

```js
function fetchItems() {
  return new Promise(function (resolve, reject) {
    let items = [1, 2, 3];
    resolve(items);
  });
}

async function logItems() {
  var resultItems = await fetchItems();
  console.log(resultItems); // [1,2,3]
}

logItems();
```

- fetchItems() 함수는 Promise 객체를 반환하는 함수이다. (Promise는 `자바스크립트 비동기 처리를 위한 객체`)
- fetchItems() 함수를 실행하면 Promise가 이행(Resolved)되며 결과 값은 `items`배열이다.
- logItems() 함수를 실행하면 fetchItems() 함수의 결과 값인 `items`배열이 `resultItems` 변수에 담긴다.
- 여기서 await을 사용하지 않았다면 밑에 코드 처럼 데이터를 받아온 시점에 콘솔을 출력할 수 있게 `콜백 함수`나 `.then()` 등을 사용해야 한다.

```js
function fetchItems() {
  return new Promise(function (resolve, reject) {
    let items = [1, 2, 3];
    resolve(items);
  });
}

function logItems() {
  var resultItems = fetchItems();
  resultItems.then((res) => console.log(res)); // [1,2,3]
}

logItems();
```

<br />

## 👨🏻‍💻 async/await 예외 처리

- async/await에서 예외를 처리하는 방법은 `try/catch`이다.
- Promise에서 에러 처리를 위해 `.catch()`를 사용했던 것처럼 async에서 `catch () { ... }`를 사용한다.

```js
async function logTodoTitle() {
  try {
    const user = await fetchUser();
    if (user.id === 1) {
      const todo = await fetchTodo();
      console.log(todo.title); // delectus aut autem
    }
  } catch (error) {
    console.log(error);
  }
}
```

<br />

## 참고

https://joshua1988.github.io/web-development/javascript/js-async-await/
https://ko.javascript.info/async-await
https://blueshw.github.io/2018/02/27/async-await/
