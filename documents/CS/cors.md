# 💻 CORS

- 도메인이나 서브 도메인, 프로토콜, 포트가 다른 곳에 요청을 보내는 것을 `Cross-Origin Request(크로스 오리진 요청)`이라고 부른다.
- 크로스 오리진 요청을 보내려면 remote origin에서 전송받은 특별한 헤더가 필요하다. 이러한 정책을 `CORS(Cross-Origin Resource Sharing)`라고 부른다.
- 한번 아래처럼 `http://example.com` 사이트에 요청을 보내보자. 요청이 실패하는 것을 확인할 수 있을 것이다.

```js
try {
  await fetch("http://example.com");
} catch (err) {
  alert(err); // TypeError: Failed to fetch
}
```

<br />

## 왜 CORS가 필요할까?

- CORS는 악의를 가진 `해커로부터 인터넷을 보호`하기 위해 만들어 졌다.
- 과거 수 년 동안, 한 사이트의 스크립트에서 다른 사이트에 있는 콘텐츠에 접근 할 수 없다는 제약이 있었다. 이런 간단하지만 강력한 규칙은 인터넷 보안을 위한 근간이었다.
  - 이러한 규칙 덕분에 `hacker.com`에서 `gmail.com`에 있는 메일 박스에 접근할 수 없는 것이다.
- 그런데 이 당시에는 자바스크립트는 네트워크 요청을 보낼 수 있는 메서드를 지원하지 않았고, 정말 웹페이지를 꾸미기 위해 사용하는 그정도 수준이였다. 하지만 웹 개발자들은 다른 사이트 컨텐츠에 접근하고 싶다는 니즈가 생겼고, 위와 같은 보안 제약을 피해 다른 웹 사이트에 요청을 보내기 위한 트릭을 만들었다.
  - 트릭에 대해서는 디테일하게 설명하지는 않겠다. 간단하게, `<form>`안에 `<iframe>` 을 넣어 전송하던가, `<script>` 를 사용하던가 이런 제약을 피하기 위한 방법이 존재했다.
  - 이러한 트릭은 보안 제약을 어기면서 양방향으로 데이터를 전달할 수 있었다.
- 시간이 지나 브라우저측 자바스크립트에도 `네트워크 관련 메서드(GET, POST, DELETE, PUT 등)`가 추가됐다. 처음 네트워크 요청 메서드가 등장했을 때엔 크로스 오리진 요청이 불가능했다. 하지만 긴 논의 끝에 크로스 오리진 요청을 허용하기로 결정한다. 단, 크로스 오리진 요청은 서버에서 명시적으로 크로스 오리진 요청을 `허가`한다는 `특별한 헤더`를 전송했을 때만 가능하도록 제약을 걸게 된다.

<br />

## 크로스 오리진 요청 종류

- 크리스 오리진 요청은 정말 단순하게 2가지로 구분 된다.
  - 안전한 요청(safe request)
  - 그 외의 요청(안전하지 않은 요청)

<br />

## 안전한 요청

- 안전한 요청은 안전하지 않은 요청 대비 만들기 쉽다.
- 안전한 요청은 다음과 같은 2가지 조건을 모두 충족하며, 말 그대로 안전한 요청이다.
  - 안전한 메서드(safe method) - `GET`, `POST`, `HEAD`를 사용한 요청
  - 안전한 헤더(safe header)
    - `Accept` 헤더
    - `Accept-Language` 헤더
    - `Content-Language` 헤더
    - 값이 `application/x-www-form-urlencoded`이나 `multipart/form-data`, `text/plain`인 `Content-Type`헤더
- 표준이 아닌 헤더(API-Key가 명시된 특수한 헤더 등)가 들어있거나 안전하지 않은 메서드(PUT, DELETE 등)을 사용한 요청은 안전한 요청이 될 수 없다.
- 아주 오래전에는 자바스크립트를 사용해 이런 요청을 보내는 것이 불가능 했다. 하지만 시간이 지나고 개발자가 자바스크립트를 사용해 `안전하지 않은 요청`을 보낼 수 있게되자, 브라우저는 안전하지 않은 요청을 서버에 보내기 전에 `preflight`요청을 먼저 전송해 서버가 `크로스 오리진 요청을 받을 준비`가 되어있는지를 확인한다.
  - 이때, 서버에서 크로스 오리진 요청은 허용하지 않는다는 정보를 담은 헤더를 브라우저에 응답하면 안전하지 않은 요청은 서버로 전송되지 않는다.

<br />

## CORS와 안전한 요청

<img width="718" alt="스크린샷 2023-06-28 오후 6 57 19" src="https://github.com/ssi02014/Front-Interview/assets/64779472/6fb11c6f-e3c8-4560-b7c1-99d7e03b46c5">

- 크로스 오리진 요청(Cross-Origin Request)을 보낼 경우 브라우저는 항상 `Origin`이라는 헤더를 요청 헤더에 추가한다.
  - Origin 헤더에는 요청은 위 사진처럼 `도메인 + 프로토콜 + 포트 정보`가 담긴다.
- 서버는 `요청 헤더에 있는 Origin을 검사`하고, 요청을 받아들이기로 동의한 상태라면 특별한 헤더 `Access-Control-Allow-Origin`을 응답해 추가한다. 이 헤더에는 `허가된 Origin에 대한 정보`나 `와일드카드(*)`가 명시된다.
- Access-Control-Allow-Origin 헤더에 `Origin 정보`나 `*`이 있으면 응답은 성공하고, 그렇지 않으면 응답이 실패하게 된다.
- 이러한 과정에서 브라우저는 `중재인` 역할을 한다. 아래 그림을 참고하자.

<img width="675" alt="스크린샷 2023-06-28 오후 7 02 35" src="https://github.com/ssi02014/Front-Interview/assets/64779472/40945f67-6c95-4d5c-8dc7-7504085282f4">

1. 브라우저는 크로스 오리진 요청 시 Origin에 값이 제대로 설정, 전송되었는지 확인한다.
2. 브라우저는 서버로부터 받은 응답에 Access-Control-Allow-Origin이 있는지를 확인해서 서버가 크로스 오리진 요청을 허용하는지, 거부하는지 확인한다.
3. Access-Control-Allow-Origin이 있다면 자바스크립트를 이용해 응답에 접근할 수 있고, 아니면 에러가 발생한다.
4. 요청이 허용된 경우, preflight 요청에 대한 응답은 다음과 같은 형태를 띈다.

```
200 OK
Content-Type: text/html; charset=UTF-8
Access-Control-Allow-Origin: https://javascript.info // (*)
...
```

<br />

## 응답 헤더

- 크로스 오리진 요청이 이뤄진 경우, 자바스크립트는 기본적으로 안전한 응답 헤더로 분류되는 헤더에만 접속할 수 있다. 이외에 응답 헤더에 접근하면 에러가 발생한다.
  - `Cache-Control`
  - `Content-Language`
  - `Content-Type`
  - `Expires`
  - `Last-Modified`
  - `Pragma`
- 자바스크립트를 사용해 안전하지 않은 응답 헤더에 접근하려면 서버에서 `Access-Control-Expose-Headers`라는 헤더를 보내줘야 한다.
- Access-Control-Expose-Headers에는 자바스크립트 접근을 허용하는 안전하지 않은 헤더 목록이 담겨있다. (`콤마(,)`로 구분)

```
200 OK
Content-Type:text/html; charset=UTF-8
Content-Length: 12345
API-Key: 2c9de507f2c54aa1
Access-Control-Allow-Origin: https://example.com
Access-Control-Expose-Headers: Content-Length,API-Key // (*)
```

<br />

## 안전하지 않은 요청

- 현대에는 GET, POST 뿐만 아니라 PATCH, DELETE 등 어떤 메서드도 사용할 수 있다.
- 하지만, 과거에는 GET, POST만 요청 메서드로 사용할 수 있었고, 아직도 이런 메서드만 다루는 웹서버도 꽤 있다. 이런 웹서버들은 GET, POST 이외의 메서드를 이용한 요청이 오면 `브라우저가 보낸 요청이 아니라고 판단`하고 `접근 권한을 확인`한다.
- 위와 같은 혼란스러운 상황을 피하고자 브라우저는 안전하지 않은 요청이 이뤄지는 경우, 서버에 바로 요청을 보내지 않고 `preflight 요청`이라는 사전 요청을 서버에 보내 `권한을 확인`한다.
  - 참고로, 안전한 요청이라면 preflight 요청을 하지 않고, 실제 본 요청을 서버로 보낸다
- preflight 요청은 `OPTIONS 메서드`를 사용하고 두 헤더가 함께 들어가며, 본문은 비어있다.
  - `Access-Control-Request-Method`: 안전하지 않은 요청에서 사용하는 메서드 정보
  - `Access-Control-Request-Header`: 안전하지 않은 요청에서 사용하는 헤더 목록(쉼표로 구분)
- 안전하지 않은 요청을 허용하기로 합의하면 서버는 본문이 비어있고, 상태 코드가 200인 응답을 다음과 같은 헤더와 함께 브라우저로 보낸다.
  - `Access-Control-Allow-Origin`: `*`이나 요청을 보낸 Origin 이어야 합니다(예: https://example.com)
  - `Access-Control-Allow-Methods`: 허용된 메서드 정보
  - `Access-Control-Allow-Headers`: 허용된 헤더 목록
  - `Access-Control-Max-Age`: permission 체크 여부를 몇 초간 `캐싱`해 놓을지를 명시한다. 이렇게 permission 정보를 캐싱해 놓으면 `브라우저는 일정 기간 동안 preflight 요청을 생략하고, 안전하지 않은 요청을 보낼 수 있다.`

<br />

## 크로스 오리진 요청 과정

<img width="661" alt="스크린샷 2023-06-28 오후 7 14 53" src="https://github.com/ssi02014/Front-Interview/assets/64779472/8d14203a-3125-4469-b0c9-5acd552917b7">

- 아래와 같은 요청이 있다고 가정해보자.
- 아래 요청은 안전하지 않은 요청이다. 그 이유는 PATCH 메서드를 사용하고 있고, Content-Type 헤더의 정보가 application/json이며, 비표준 헤더 API-Key를 사용한다.

```js
let response = await fetch("https://site.com/service.json", {
  method: "PATCH",
  headers: {
    "Content-Type": "application/json",
    "API-Key": "secret",
  },
});
```

<br />

### 1단계 - preflight 요청

- 본 요청을 보내기 전에 브라우저는 자체적으로 preflight 요청을 보낸다.

```
OPTIONS /service.json
Host: site.com
Origin: https://javascript.info
Access-Control-Request-Method: PATCH
Access-Control-Request-Headers: Content-Type,API-Key
```

<br />

### 2단계 - preflight 응답

- 서버는 해당 요청을 허용하기로 한다면 상태코드 200과 함께 다음 같은 응답을 전송한다.

```
200 OK
Access-Control-Allow-Origin: https://javascript.info
Access-Control-Allow-Methods: PUT,PATCH,DELETE
Access-Control-Allow-Headers: API-Key,Content-Type,If-Modified-Since,Cache-Control
Access-Control-Max-Age: 86400
```

- 이렇게 서버에서 preflight 응답이 오면 브라우저는 Access-Control-Allow-Methods를 PATCH가 있는 것을 확인하고, 이어서 Access-Control-Allow-Headers에 API-Key,Content-Type가 있는 것을 확인한다.
- 둘 다 모두 정상이므로 이제 브라우저는 본 요청을 서버에 보낸다.
- 참고로 위에서도 언급했지만 Access-Control-Max-Age 헤더가 응답으로 오면 preflight 허용 여부가 헤더와 함께 캐싱되기 때문에 브라우저는 해당 헤더에 명시된 시간만큼 preflight 요청을 보내지 않아도 된다.

<br />

### 3단계 실제 요청

- preflight 요청이 성공적으로 이뤄진 후에야 브라우저는 본 요청을 보낸다. 지금부터의 프로세스는 안전한 요청이 이뤄질때의 절차와 동일하다.
- 본 요청은 크로스 오리진 요청이기 때문에 `Origin` 헤더가 붙는다.

```
PATCH /service.json
Host: site.com
Content-Type: application/json
API-Key: secret
Origin: https://javascript.info
```

<br />

### 4단계 실제 응답

- 서버에서 preflight 요청이 성공했더라도 본 응답에 `Access-Control-Allow-Origin` 헤더는 반드시 붙여줘야 한다.

```
Access-Control-Allow-Origin: https://javascript.info
```

- 이 모든 과정이 끝나야 자바스크립트를 사용해 실제 응답을 읽을 수 있다.

<br />

## 자격 증명

- 자바스크립트로 크로스 오리진 요청을 보낼 경우, 기본적으로 `쿠키`나 `HTTP 인증` 같은 `자격 증명(credential)`이 함께 전송되지 않는다.
- HTTP 요청의 경우 대개 쿠키가 함께 전송되는데, 크로스 오리진 요청은 예외이다.
- 이런 예외가 생긴 이유는 자격 증명과 함께 전송되는 요청의 경우 영향력이 강하기 때문이다. 크로스 오리진 요청 시 자격 증명을 함께 전송 할 수 있으면 사용자 동의 없이 자바스크립트로 민감한 정보에 접근할 수 있게 된다.
- 그럼에도 불구하고 서버에서 이를 허용하고 싶다면, 자격 증명이 담긴 헤더를 명시적으로 허용하겠다는 세팅을 해줘야 한다.

### fetch

- fetch를 이용해 자격 증명 정보를 함께 전송하려면 `credential` 옵션을 추가하면 된다.
- 옵션은 3가지가 있다.
  - omit : 절대로 cookie 들을 전송하거나 받지 않는다.
  - same-origin : 동일 출처(Same-Origin)이라면, user credentials (cookies, basic http auth 등..)을 전송한다. (`default`)
  - include : Cross-Origin 호출이라 할지라도 언제나 user credentials (cookies, basic http auth 등..)을 전송한다.

```js
fetch("주소", {
  credentials: "include", // 모든 요청에 인증 정보 포함
});
```

<br />

### axios

- axios의 경우에는 `withCredentials` 설정을 `true`로 넣어주면 된다.

```js
axios.post(주소, 데이터, { withCredentials: true });

// 또는 공통으로 추가
axios.defaults.withCredentials = true;
```

<br />
