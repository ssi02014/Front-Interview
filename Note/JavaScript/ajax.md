# 💻 Ajax
<br />

## 👨🏻‍💻 Ajax
- `AJAX(Asynchronous JavaScript And XML)`란, 자바스크립트 라이브러리중 하나이다. 브라우저가 갖고있는 `XMLHttpRequest` 객체를 이용해서 전체 페이지를 새로 고치지 않고도 페이지의 일부만을 위한 데이터를 로드하는 기법이다.
- 자바스크립트를 사용한 비동기 통신, 클라이언트와 서버간에 `XML 데이터`를 주고받는 기술이다.
- 여기서 `XML`이 있는 이유는 과거에는 데이터 포맷으로 XML을 많이 사용했기 때문이다. 요즘에는 `JSON`을 더 많이 사용한다.

<br />

## 👨🏻‍💻 Ajax왜 사용하는가?
- 기본적으로 `HTTP 프로토콜`은 클라이언트쪽에서 req를 보내고 서버로부터 res를 받으면 이어졌던 연결이 끊기게 되어 있다. 그래서 화면의 내용을 갱신하기 위해서는 다시 req를 보내고 res를 받으면서 페이지 전체를 갱신 한다.
- 이럴 경우, 페이지의 일부분만 갱신하는 경우에도 페이지 전체를 다시 로드해야하는데, 엄청난 `자원 낭비`와 `시간 낭비`를 초래한다. 
- 하지만 `Ajax`는 html 페이지 전체가아닌 일부분만 갱신할 수 있도록 `XMLHttpRequest`객체를 통해 서버에 request를 한다. 이 경우 JSON이나 XML 형태로 필요한 데이터만 받아 갱신하기 때문에 그만큼의 자원과 시간을 아낄 수 있다.

<br />

## 👨🏻‍💻 Ajax 장, 단점
### 🏃 장점
- 웹페이지의 속도 향상
- 페이지를 전환하지 않고 빠르게 화면 일부분만 업데이트 할 수 있다.
- 서버의 처리가 완료 될때까지 기다지리 않고 처리 가능(비동기 처리)
- 서버에서 Data만 전송하면 되므로 전체적인 코딩의 양이 줄어듦

<br />

### 🏃 단점
- History 관리가 안된다. 즉, 보안에 좀 더 신경을 써야 한다.
- 연속으로 데이터를 요청하면 서버 부하가 증가할 수 있다.
- XMLHttpRequest를 통해 통신하는 경우 사용자에게 아무런 진행 정보가 주어지지 않는다. 그래서 요청이 완료되지 않았는데 사용자가 페이지를 떠나거나 오작동할 우려가 있다.
- 지원하지 않는 브라우저가 있다.

<br />

## 👨🏻‍💻 Ajax 동작 방식
![ajax동작방식](https://user-images.githubusercontent.com/64779472/117575711-0a027300-b11e-11eb-976b-79fa06eec84f.PNG)

<br />

1. 사용자에 의한 요청 이벤트 발생
2. 요청 이벤트가 발생하면 이벤트 핸드러에 의해 자바스크립트가 호출
3. 자바스크립트는 XMLHttpRequest 객체를 사용하여 서버로 요청을 보냄. 이때, 브라우저는 요청을 보내고 나서, 서버의 응답을 기다릴 필요 없이 다른 작업을 처리(`비동기 처리`)
4. 서버는 전달받은 XMLHttpRequest 객체를 가지고 Ajax 요청을 처리
5. 와 6. 서버는 처리한 결과를 HTML, XML 또는 JSON 형태의 데이터로 웹 브라우저에 전달.
7. 서버로부터 전달받은 데이터를 가지고 웹 페이지의 일부분만을 갱신하는 자바스크립트를 호출
8. 결과적으로 웹 페이지의 일부분만이 다시 로딩되어 표시된다.

<br />

## 👨🏻‍💻 Ajax 어떻게 사용하는가?
### 🏃 XMLHttpRequest
- 일반적으로 `XMLHttpRequest` 객체를 사용하여 인스턴스를 만들어 인스턴스의 `open()`, `send()` 메서드를 이용한다.
```js
  let ourRequest = new XMLHttpRequest();

  ourRequest.open(
    "GET",
    "https://learnwebcode.github.io/json-example/animals-1.json"
  );

  ourRequest.onload = () => {
    let ourData = JSON.parse(ourRequest.responseText);
    console.log(ourData[0]);
  };

  ourRequest.send();
```

<br />

### 🏃 Fetch
- ES6부터 새로 도입 된 `fetch`를 사용해서 요청을 할 수도 있다. IE를 지원하지 않는 다는 점을 제외하고는 `XMLHttpRequest`보다 훨씬 직관적이다.
- ES6에서 표준이 되었고, `Promise`를 리턴한다.
- 응답 객체는 json(), blob()과 같은 내장 메서드로 body를 추출해내고 이는 다시 `Promise`를 리턴한다.

```js
  fetch("https://learnwebcode.github.io/json-example/animals-1.json")
    .then(res => res.json())
    .then(resJson => console.log(resJson));
```

<br />

## 참고
https://github.com/baeharam/Must-Know-About-Frontend/blob/master/Notes/javascript/ajax.md <br />
http://tcpschool.com/ajax/ajax_intro_works <br />
https://coding-factory.tistory.com/143 <br />