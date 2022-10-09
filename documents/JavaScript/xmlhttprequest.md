# 💻 XMLHttpRequest와 Fetch

<br />

## 👨🏻‍💻 XMLHttpRequest

- `XMLHttpRequest(XHR)` 객체는 서버와 상호작용하기 위해 사용됩니다.
- 전체 페이지 새로고침 없이도 `URL`로부터 데이터를 받아올 수 있습니다.
- 이는 웹페이지가 사용자가 하고있는 것을 방해하지 않으면서 페이지의 일부를 업데이트 할 수 있도록 해줍니다.
- `XMLHttpRequest`는 `Ajax`프로그래밍이 자주 사용됩니다.

<br />

```js
var xhr = new XMLHttpRequest();
xhr.onreadystatechange = function () {
  if (xhr.readyState === xhr.DONE) {
    if (xhr.status === 200 || xhr.status === 201) {
      console.log(xhr.responseText);
    } else {
      console.error(xhr.responseText);
    }
  }
};
xhr.open("GET", "http://localhost:3000/single-json");
xhr.send();
```

- 위의 코드는 XHR의 기본 예제이다.

<br />

## 👨🏻‍💻 XMLHttpRequest 메서드

- new XMLHttpRequest( ): 새로운 XMLHttpRequest 객체 생성
- abort( ): 현재 요청을 취소.
- getAllResponseHeaders( ): `헤더 정보`를 반환.
- getResponseHeader( ): `특정 헤더 정보`를 반환.
- open (method, url, async, user, psw): `HTTP 요청에 대한 속성`을 지정한다.
  - method : 파라미터 전송 방법을 지정, `GET` 또는 `POST`로 지정할 수 있다.
  - url : HTTP 요청을 보낼 원격 페이지의 주소.
  - async : 요청을 `동기`, `비동기` 처리할지의 여부 `true`이면 비동기처리, `false`면 동기로 처리(생략 가능)
  - user, pwd: http 요청에 대한 인증이 필요할 경우 지정할 수 있는 계정 정보(생략 가능)
- send( ): 서버에 요청 보내기. `GET 방식` 요청일 때 사용.
- send(string): 서버에 요청 보냄. `POST 방식` 요청일 때 사용.
- setRequestHeader( ): `key/value`쌍의 HTTP 헤더를 전송 목록에 더한다.

<br />

## 👨🏻‍💻 XMLHttpRequest 속성

- .onreadystatechange: HTTP요청의 `상태 변화`에 따라 호출되는 `이벤트 핸들러`입니다. 즉 이 함수는 서버에서 응답이 도착할 때까지 `readyState` 프로퍼티 값의 변화에 따라 총 5번 호출된다.
  - 0 (UNSENT) : XMLHttpRequest 객체가 생성됨.
  - 1 (OPENED) : open() 메소드가 성공적으로 실행됨.
  - 2 (HEADERS_RECEIVED) : HTTP 요청을 보내어 처리하고 있는 중. 헤더는 읽을 수 있는 상태.
  - 3 (LOADING) : 요청한 데이터를 처리 중임.
  - 4 (DONE) : 요청한 데이터의 처리가 완료되어 응답할 준비가 완료됨. 비로소 responseText 와 responseXML 속성을 읽을 수 있는 상태.

```js
switch (httpRequest.readyState) {
  case XMLHttpRequest.UNSET:
    currentState += "현재 XMLHttpRequest 객체의 상태는 UNSET 입니다.<br>";
    break;

  case XMLHttpRequest.OPENED:
    currentState += "현재 XMLHttpRequest 객체의 상태는 OPENED 입니다.<br>";
    break;

  case XMLHttpRequest.HEADERS_RECIEVED:
    currentState +=
      "현재 XMLHttpRequest 객체의 상태는 HEADERS_RECEIVED 입니다.<br>";
    break;

  case XMLHttpRequest.LOADING:
    currentState += "현재 XMLHttpRequest 객체의 상태는 LOADING 입니다.<br>";
    break;

  case XMLHttpRequest.DONE:
    currentState += "현재 XMLHttpRequest 객체의 상태는 DONE 입니다.<br>";
    break;
}
```

<br />

- .responseText : 요청에 대한 응답을 `텍스트`로 반환합니다.
- .responseXML : 연결에 대한 응답을 `XML DOM`으로 변환합니다. XML 문자열이 아니라 XML DOM으로 반환한다는 것을 염두해 두세요.
- .status : `HTTP 상태 코드`를 `숫자`로 반환합니다. 예를 들면 OK에 대해서 200을, 페이지를 찾을수 없었을 때는 404를 반환합니다.
- .statusText : `HTTP 상태 코드`에 대한 `문자열`을 반환합니다. 예를 들면 "OK", "Not Found" 등이 될수 있습니다.

<br />

## 👨🏻‍💻 Fetch

- 자바스크립트를 사용하여 `Ajax 비동기 통신`을 위해 별도의 `라이브러리`를 많이 사용하고 있습니다. 예를들면 jQuery의 `ajax()`, 아니면 `axios` 등을 Ajax 구현을 위한 목적으로 추가해 사용해왔습니다.
- 왜냐하면 순수 자바스크립트는 비동기 통신이 어렵고 비효율적이기 때문이다. 특히 XMLHttpRequest는 원하는 기능을 구현하기 위해서는 너무 복잡하고 `Promise`객체를 사용하는 것도 어렵기 때문이다.
- 이후, `fecth API`가 ES6표준으로 등장하면서 `fetch` 사용이 일반적이게 되었다.
- `fetch`는 ES6의 비동기 통신 방법으로, 자체적으로 `Promise`객체를 반환하기에 `Promise`와 함께 사용하기도 편리하다.

<br />

## 👨🏻‍💻 Fetch(Promise 기반)사용법

### 🏃 GET

```js
fetch("https://jsonplaceholder.typicode.com/posts/1").then((response) =>
  console.log(response)
);
```

- `fetch()`는 디폴트로 GET 방식으로 작동하고 GET 방식은 요청 전문을 받지 않기 때문에 옵션 인자가 필요가 없습니다.
- 출력 결과는 다음과 같다.

```
  Response {status: 200, ok: true, redirected: false, type: "cors", url: "https://jsonplaceholder.typicode.com/posts/1", …}
```

- 대부분의 `REST API`들은 `JSON` 형태의 데이터를 응답하기 때문에, `응답(response) 객체`는 `json()` 메서드를 제공한다.

<br />

```js
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then((response) => response.json())
  .then((data) => console.log(data));
```

- `json()`를 호출하면, `응답(response) 객체`로 부터 JSON 포멧의 응답 전문을 자바스크립트 객체로 변환하여 얻을 수 있습니다.

```js
  {
    "userId": 1,
    "id": 1,
    "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
    "body": "quia et suscipit↵suscipit recusandae consequuntur …strum rerum est autem sunt rem eveniet architecto"
  }
```

<br />

### 🏃 POST

- `원격 API`에서 관리하고 있는 데이터를 생성해야 한다면 `요청 전문`을 포함할 수 있는 `POST 방식`의 HTTP 통신이 필요하다.

```js
let body = {
  title: "Test",
  body: "I am testing!",
  userId: 1,
};

fetch("https://jsonplaceholder.typicode.com/posts", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(body),
}).then((response) => console.log(response));
```

- method 옵션을 POST로 지정해주고
- headers 옵션을 통해 JSON 포멧을 사용한다고 알려준다.
- 요청 전문을 JSON 포멧으로 `직렬화(JSON.stringify(body))`화여 가장 중요한 body 옵션에 설정해줍니다.
- `JSON.stringify()` 메서드는 JavaScript 값이나 객체를 `JSON 문자열`로 `변환`합니다.

```
  Response {type: "cors", url: "https://jsonplaceholder.typicode.com/posts", redirected: false, status: 201, ok: true, …}
```

<br />

```js
let body = {
  title: "Test",
  body: "I am testing!",
  userId: 1,
};

fetch("https://jsonplaceholder.typicode.com/posts", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(body),
})
  .then((response) => response.json())
  .then((data) => console.log(data));
```

- 마찬가지 방법으로 응답 객체의 `json() 메서드`를 호출하면 응답 전문을 `객체 형태`로 얻을 수 있습니다.

```js
  {
    title: "Test",
    body: "I am testing!",
    userId: 1,
    id: 101
  }
```

<br />

### 🏃 PUT

```js
let body = {
  title: "Edit",
  body: "I am Edit Testing!",
  userId: 2,
};

fetch("https://jsonplaceholder.typicode.com/posts/1", {
  method: "PUT",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(body),
})
  .then((response) => response.json())
  .then((data) => console.log(data));
```

- `PUT`은 `method`의 옵션을 제외하고 `POST`와 거의 유사하다.

<br />

### 🏃 DELETE

```js
fetch("https://jsonplaceholder.typicode.com/posts/1", {
  method: "DELETE",
})
  .then((response) => response.json())
  .then((data) => console.log(data));
```

- `DELETE` 방식에서는 보낼 데이터가 없기 때문에, `headers와 body 옵션이 필요가 없다.`

<br />

## 참고

https://babtingdev.tistory.com/45
https://www.daleseo.com/js-window-fetch/
https://velog.io/@khw970421/Fetch-%EC%82%AC%EC%9A%A9%EB%B2%95
https://uhou.tistory.com/102
https://meetup.toast.com/posts/92
