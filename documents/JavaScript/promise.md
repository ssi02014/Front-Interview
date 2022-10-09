# 💻 Promise

<br />

## 👨🏻‍💻 Promise란?

- 자바스크립트는 비동기 처리를 위한 하나의 패턴으로 `콜백 함수`를 사용한다.
- 전통적인 콜백 패턴은 `콜백 헬`로 인해 가독성이 나쁘고 버동기 처리 중 발생한 에러의 처리가 곤란하며 여러 개의 비동기 처리를 한번에 처리하는 데도 한계가 있다.
- ES6에서는 비동기 처리를 위한 또 다른 패턴으로 `프로미스(Promise)`를 도입했다.
- 프로미스는 전통적인 콜백 패턴이 가진 단점을 보완하여 비동기 처리 시점을 명확하게 표현할 수 있다는 장점이 있다.

<br />

## 👨🏻‍💻 콜백 패턴의 단점

### 🏃 동기식 처리모델(Synchronous processing model)과 비동기식 처리 모델(Asynchronous processing model)

- `동기식 처리 모델`은 직렬적으로 태스크를 수행한다. 즉, 태스크는 순차적으로 실행되며 어떤 작업이 수행중이면 다음 태스크는 대기한다.
- `비동기식 처리 모델`은 병렬적으로 태스크를 수행한다. 즉, 태스크가 종료되지 않은 상태라 하더라도 대기하지 않고 즉시 다음 태스크를 수행한다.
- 자바스크립트의 대부분의 DOM 이벤트와 Timer 함수(setTimeout, setInterval), Ajax 요청은 비동기식 처리 모델로 동작한다.

<br />

### 🏃 콜백 헬(Callback hell)

- 자바스크립트에서 비동기식 처리 모델은 요청을 병렬로 처리하여 다른 요청이 `블로킹(작업 중단)`되지 않는 장점이 있다.
- 하지만, 비동기 처리를 위해 콜백 패턴을 사용하면 처리 순서를 보장하기 위해 여러 개의 콜백 함수가 `네스팅(nesting, 중첩)`되어 복잡도가 높아지는 `콜백 헬(Callback hell`) 이 발생한다는 단점이 있다.
- 콜백 헬은 가독성을 나쁘게 하며 실수를 유발하는 원이이 된다.
- 밑에 코드는 콜백 헬의 예제이다.

```js
step1(function (value1) {
  step2(value1, function (value2) {
    step3(value2, function (value3) {
      step4(value3, function (value4) {
        step5(value4, function (value5) {
          // value5를 사용하는 처리
        });
      });
    });
  });
});
```

<br />

## 👨🏻‍💻 Promise의 생성

- 프로미스는 `Promise 생성자 함수`를 통해 `인스턴스화` 한다.
- Promise 생성자 함수는 비동기 작업을 수행할 콜백 함수를 인자로 전달받는데 이 콜백 함수는 `resolve`와 `reject` 함수를 인자로 전달받는다.

```js
  // Promise 객체의 생성
  const promise = new Promise((resolve, reject) => {
    // 비동기 작업을 수행한다.

    if (/* 비동기 작업 수행 성공 */) {
      resolve('result');
    }
    else { /* 비동기 작업 수행 실패 */
      reject('failure reason');
    }
  });
```

<br />

- Promise는 비동기 처리가 `성공(fullfilled)`하였는지, 또는 `실패(rejected)`하였는지 등의 `상태(state)`정보를 갖는다.
- Promise 상태 정보
  ![promise상태](https://user-images.githubusercontent.com/64779472/120832507-b3ad1680-c59b-11eb-8c1b-b6e53b7d7771.PNG)

<br />

- Promise 생성자 함수가 인자로 전달 받은 콜백 함수는 내부에서 비동기 처리 작업을 수행한다.
- 비동기 처리가 성공하면 콜백 함수의 인자로 전달받은 `resolve` 함수를 호출한다. 이때 Promise는 `fullfilled` 상태가 된다.
- 비동기 처리가 실패하면 `reject` 함수를 호출한다. 이때 Promise는 `rejected`상태가 된다.

<br />

```js
const promiseAjax = (method, url, payload) => {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();

    xhr.open(method, url);
    xhr.setRequestHeader("Content-type", "application/json");
    xhr.send(JSON.stringify(payload));

    xhr.onreadystatechange = function () {
      // 서버 응답 완료가 아니면 무시
      if (xhr.readyState !== XMLHttpRequest.DONE) return;

      if (xhr.status >= 200 && xhr.status < 400) {
        // resolve 메소드를 호출하면서 처리 결과를 전달
        resolve(xhr.response); // Success!
      } else {
        // reject 메소드를 호출하면서 에러 메시지를 전달
        reject(new Error(xhr.status)); // Failed...
      }
    };
  });
};
```

- 위의 예제는 비동기 함수 내에서 Promise 객체를 생성하고 그 내부에서 비동기 처리를 구현하였다.
- 비동기 처리에 성공하면 `resolve` 메서드를 호출한다. 이때 resolve 메서드의 인자로 `비동기 처리 결과`를 전달한다.
- 비동기 처리에 실패하면 `reject` 메서드를 호출한다. 이때 reject 메서드의 인자로 `에러 메시지`를 전달한다.
- 추가적으로 위의 예제에서 XMLHttpRequest의 속성과 메서드를 간단하게 알아보면

```
  - .open(method, url, async, username, passowrd): HTTP 요청에 대한 속성을 지정한다.
    1. method: 파라미터 전송 방법을 지정, "GET" 또는 "POST"로 지정할 수 있다.
    2. url: HTTP 요청을 보낼 원격 페이지의 주소.
    3. async: 요청을 동기, 비동기 처리할지의 여부 true이면 비동기처리, false면 동기로 처리(생략 가능)
    4. username, password: http 요청에 대한 인증이 필요할 경우 지정할 수 있는 계정 정보(생략 가능)

  - .send(content): open에 지정한 속성을 이용하여 HTTP 요청을 전송한다.
    1. content: HTTP 요청과 함께 전송할 파라미터 또는 콘텐츠이다.

  - .setRequestHeader(key,value) : key/value 쌍의 HTTP 헤더를 전송 목록에 더합니다.

  - .onreadystatechange: HTTP요청의 상태 변화에 따라 호출되는 이벤트 핸들러입니다.
    1. 0 (UNSENT) : XMLHttpRequest 객체가 생성됨.
    2. 1 (OPENED) : open() 메소드가 성공적으로 실행됨.
    3. 2 (HEADERS_RECEIVED) : HTTP 요청을 보내어 처리하고 있는 중. 헤더는 읽을 수 있는 상태.
    4. 3 (LOADING) : 요청한 데이터를 처리 중임.
    5. 4 (DONE) : 요청한 데이터의 처리가 완료되어 응답할 준비가 완료됨. 비로소 responseText 와 responseXML 속성을 읽을 수 있는 상태.

  - .responseText : 요청에 대한 응답을 텍스트로 반환합니다.
  - .responseXML : 연결에 대한 응답을 XML DOM 으로 변환합니다. XML 문자열이 아니라 XML DOM으로 반환한다는 것을 염두해 두세요.
  - .status : HTTP 상태 코드를 숫자로 반환합니다. 예를 들면 OK에 대해서 200을, 페이지를 찾을수 없었을 때는 404를 반환합니다.
  - .statusText : HTTP 상태 코드에 대한 문자열을 반환합니다. 예를 들면 "OK", "Not Found" 등이 될수 있습니다.
```

<br />

## 👨🏻‍💻 Promise의 후속 처리 메서드

![promise프로세스](https://user-images.githubusercontent.com/64779472/120838625-fc1c0280-c5a2-11eb-936f-d6f2658a012f.PNG)

- Promise로 구현된 비동기 함수는 `Promise 객체`를 반환하여야 한다.
- Promise로 구현된 `비동기 함수를 호출하는 측(Promise consumer)`에서는 Promise 객체의 `후속 처리 메서드(then, catch)`를 통해 비동기 처리 결과 또는 에러 메시지를 전달받아 처리한다.
- Promise 객체는 상태를 갖는 다고 하였다.`(fullfilled, rejected 등)` 이 상태에 따라 후속 처리 메소드를 `체이닝 방식`으로 호출한다.

<br />

### 🏃 then

- then 메서드는 두 개의 콜백 함수를 인자로 받는다.
- 첫 번째 콜백 함수는 `성공(fullfilled, resolve 함수가 호출된 상태)` 시 호출된다.
- 두 번째 콜백 함수는 `실패(rejected, reject 함수가 호출된 상태)`시 호출된다.

<br />

### 🏃 catch

- `예외(비동기 처리에서 발생한 에러와 then 메서드에서 발생한 에러)`가 발생하면 호출된다.
- catch 메서드는 Promise를 반환한다.

<br />

```js
promiseAjax("GET", "http://jsonplaceholder.typicode.com/posts/1")
  .then(JSON.parse)
  .then(
    // 첫 번째 콜백 함수는 성공(fulfilled, resolve 함수가 호출된 상태) 시 호출된다.
    render,
    // 두 번째 함수는 실패(rejected, reject 함수가 호출된 상태) 시 호출된다.
    console.error
  );
```

- 위의 예제에서 promiseAjax은 `Promise 객체`를 반환한다.
- Promise 객체의 `후속 메서드(then, catch)`를 사용하여 비동기 처리 결과에 대한 후속 처리를 수행한다.

<br />

## 👨🏻‍💻 Promise 에러 처리

- 비동기 처리 결과에 대한 후속 처리는 Promise 객체가 제공하는 `후속 처리 메서드(then, catch, finally)`를 사용하여 수행한다고 말했다.
- 비동기 처리 시에 발생한 에러는 `then 메서드`의 `두 번째 콜백 함수`로 처리할 수 있다.

```js
const wrongUrl = "https://jsonplaceholder.typicode.com/XXX/1";

// 두 번째 콜백 함수는 첫 번째 콜백 함수에서 발생한 에러를 캐치하지 못한다.
promiseAjax("https://jsonplaceholder.typicode.com/todos/1").then(
  (res) => console.xxx(res),
  (err) => console.error(err)
);
```

- 하지만, then의 두 번째 콜백 함수는 첫 번째 콜백 함수에서 발생한 에러를 캐치 못하고, 코드가 복잡해져서 가독성에 좋지 않다!

<br />

```js
promiseAjax("https://jsonplaceholder.typicode.com/todos/1")
  .then((res) => console.xxx(res))
  .catch((err) => console.error(err)); // TypeError: console.xxx is not a function
```

- catch 메서드를 `모든 then메서드를 호출한 이후`에 호출한다면, `비동기 처리에서 발생하는 에러(reject함수가 호출된 상태)`뿐만 아니라 `then 메서드 내부에서 발생한 에러`까지 모두 캐치할 수 있다.
- 또한, catch 메서드를 사용하는 것이 가독성이 좋고 명확하다. 따라서 에러 처리는 then 메서드에서 하지 말고 `catch 메서드`를 사용하는 것을 권장한다.

<br />

## 👨🏻‍💻 프로미스 체이닝

- 비동기 함수의 처리 결과를 가지고 다른 비동기 함수를 호출해야 하는 경우, 함수의 호출이 `중첩(네스팅, nesting)`되어 복잡도가 높아지는 `콜백 헬`이 발생한다.
- 프로미스는 후속 처리 메서드를 `체이닝(chainning)`하여 여러 개의 프로미스를 연결하여 사용할 수 있다. 이를 통해 콜백 헬을 해결한다.
- Promise 객체를 반환한 비동기 함수는 프로미스 후속 처리 메서드인 `then`이나 `catch` 메서드를 사용할 수 있다.
- 따라서, then 메서드가 Promise 객체를 반환하도록 하면(then 메서드는 기본적으로 Promise를 반환한다.) `여러 개의 프로미스를 연결`하여 사용할 수 있다.

```js
const url = "http://jsonplaceholder.typicode.com/posts";

// 포스트 id가 1인 포스트를 검색하고 프로미스를 반환한다.
promiseAjax("GET", `${url}/1`)
  // 포스트 id가 1인 포스트를 작성한 사용자의 아이디로 작성된 모든 포스트를 검색하고 프로미스를 반환한다.
  .then((res) => promiseAjax("GET", `${url}?userId=${JSON.parse(res).userId}`))
  .then(JSON.parse)
  .then(render)
  .catch(console.error);
```

<br />

## 👨🏻‍💻 Promise.all

- 여러개의 비동기 작업들이 존재하고 이들이 모두 완료되었을 때, 작업을 진행하고 싶다면 `Promise.all`을 활용하면 된다.
- `Promise.all`메서드는 Promise가 담겨 있는 배열 등의 `이터러블`을 인자로 전달 받는다.
- 전달받은 모든 프로미스를 병렬로 처리하고 그 처리 결과를 resolve하는 새로운 프로미스를 반환한다.

```js
Promise.all([
  new Promise((resolve) => setTimeout(() => resolve(1), 3000)), // 1
  new Promise((resolve) => setTimeout(() => resolve(2), 2000)), // 2
  new Promise((resolve) => setTimeout(() => resolve(3), 1000)), // 3
])
  .then(console.log) // [ 1, 2, 3 ]
  .catch(console.log);
```

- 위의 코드를 살펴보면 `모든 Promise의 처리가 성공`하면 각각의 프로미스가 resolve한 처리 결과를 `배열`에 담아 resolve하는 `새로운 프로미스를 반환`한다.
- 이때, 첫번째 프로미스가 가장 나중에 처리되더라도 Promise.all 메서드가 반환하는 프로미스는 첫번째 프로미스가 resolve한 처리 결과부터 차례대로 배열에 담는다. 그리고 그 배열을 resolve하는 새로운 프로미스를 반환한다. 즉, `처리 순서가 보장된다.`

<br />

## 참고

https://babtingdev.tistory.com/45
https://poiemaweb.com/es6-promise
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise
https://ko.javascript.info/promise-basics
