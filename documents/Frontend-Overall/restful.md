# 💻 REST와 REST API

<br />

## 👨🏻‍💻 REST

### 🏃 REST의 정의

- REST는 `Representational State Transfer`의 약자이다.
- 자원의 이름(자원의 표현)으로 구분하여 해당 자원의 상태(정보)를 주고 받는 모든 것을 의미한다.
- 즉, 자원(resource)의 표현(representation)에 의한 상태 전달이다.

<br />

- 자원(resource)의 표현(representation)
  - 자원: 해당 소프트웨어가 관리하는 모든 것 ex) 문서, 그림, 데이터, 해당 소프트웨어 자체 등
  - 표현: 그 자원을 표현하기 위한 이름 ex) DB의 학생 정보가 자원일 때, student를 자원의 표현으로 정한다.
- 상태(정보) 전달
  - 데이터가 요청되어지는 시점에서 `자원의 상태(정보)`를 전달한다.
  - `JSON` 혹은 `XML`를 통해 데이터를 주고 받는 것이 일반적이다.
- 월드 와이드 웹(www)과 같은 `분산 하이퍼미디어 시스템`을 위한 소프트웨어 개발 아키텍처의 한 형식이다.
  - REST는 기본적으로 `웹의 기존 기술`과 `HTTP 프로토콜`을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일이다.

<br />

### 🏃 REST의 구체적인 개념

- HTTP URI(Uniform Resource Identifier)를 통해 `자원(Resource)`을 명시하고, `HTTP Method(POST, GET, PUT, DELETE)`를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미한다.
- 즉, REST는 `자원 기반의 구조(ROA, Resource Oriented Architecture)`설계의 중심에 Resource가 있고 HTTP Method를 통해 Resource를 처리하도록 설계된 아키텍처를 의미한다.
- 웹 사이트의 이미지, 텍스트, DB 내용 등의 모든 자원에 고유한 ID인 HTTP URL을 부여한다.
- CRUD Operation
  - Create: 생성(POST)
  - Read : 조회(GET)
  - Update : 수정(PUT)
  - Delete : 삭제(DELETE)
  - HEAD: header 정보 조회(HEAD)

<br />

### 🏃 REST 구성 요소

- **자원(Resource): URI**
  - 모든 자원에 고유한 ID가 존재하고, 이 자원은 Server에 존재한다.
  - 자원을 구별하는 ID는 `/groups/:group_id`와 같은 `HTTP URI`이다.
  - Client는 URI를 이용해서 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 Server에 요청한다.
- **행위(Verv): HTTP Method**
  - `HTTP 프로토콜의 Method`를 사용한다.
  - HTTP 프로토콜은 GET, POST, PUT, DELETE와 같은 메서드를 제공한다.
- **표현(Representation of Resource)**
  - Client가 자원의 상태(정보)에 대한 `조작을 요청`하면 Server는 이에 적절한 `응답(Representation)`을 보낸다.
  - REST에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태의 Representation으로 나타내어 질 수 있다.
  - `JSON` 혹은 `XML`을 통해 데이터를 주고 받는 것이 일반적이다.

<br />

### 🏃 REST의 특징

- **Uniform Interface(인터페이스 일관성)**
  - Uniform Interface는 URI로 지정한 `리소스에 대한 조작을 통일`되고 `한정적인 인터페이스`로 수행하는 아키텍처 스타일을 말한다.

<br />

- **Stateless (무상태성)**
  - REST는 무상태성 성격을 갖는다. 다시 말해 작업을 위한 상태정보를 따로 저장하고 관리하지 않는다. 세션 정보나 쿠키정보를 별도로 저장하고 관리하지 않기 때문에 API 서버는 들어오는 요청만을 단순히 처리하면 된다. 그렇기 때문에 서비스의 자유도가 높아지고 서버에서 불필요한 정보를 관리하지 않음으로써 구현이 단순해진다.

<br />

- **Cacheable (캐시 처리 가능)**
  - REST의 가장 큰 특징 중 하나는 HTTP라는 기존 웹표준을 그대로 사용하기 때문에, 웹에서 사용하는 기존 인프라를 그대로 활용이 가능하다. 따라서 HTTP가 가진 `캐싱 기능`이 적용 가능하고 HTTP 프로토콜 표준에서 사용하는 Last-Modified태그나 E-Tag를 이용하면 캐싱 구현이 가능하다.

<br />

- **Self-descriptiveness (자체 표현 구조)**
  - REST의 또 다른 큰 특징 중 하나는 REST API 메시지만 보고도 이를 쉽게 이해 할 수 있는 자체 표현 구조로 되어 있다는 것이다.

<br />

- **Client-Server 구조**
  - REST 서버는 `API 제공`, 클라이언트는 사용자 인증이나 컨텍스트(세션, 로그인 정보)등을 `직접 관리`하는 구조로 각각의 역할이 확실히 구분되기 때문에 클라이언트와 서버에서 개발해야 할 내용이 명확해지고 서로간 의존성이 줄어들게 됩니다.

<br />

- **Layered System (계층형 구조)**
  - REST 서버는 `다중 계층`으로 구성될 수 있으며 `보안`, `로드 밸런싱`, `암호화 계층`을 추가해 구조상의 유연성을 둘 수 있고 `PROXY`, `게이트웨이` 같은 네트워크 기반의 중간매체를 사용할 수 있게 합니다.

<br />

## 👨🏻‍💻 REST API

- API(Application Programming Interface)란, `데이터와 기능의 집합`을 제공하여 컴퓨터 프로그램간 상호작용을 촉진하며, 서로 정보를 교환 가능 하도록 하는 것
- REST API란, REST 기반으로 서비스 API를 구현한 것
- 최근 OpenAPI(누구나 사용할 수 있도록 공개된 API), 마이크로 서비스(하나의 큰 애플리케이션을 여러 개의 작은 애플리케이션으로 쪼개어 변경과 조합이 가능하도록 만든 아키텍처) 등을 제공하는 업체 대부분 REST API를 제공한다.

<br />

### 🏃 REST API의 특징

- 사내 시스템들도 REST 기반으로 시스템을 분산해 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 할 수 있다.
- REST는 HTTP 표준을 기반으로 구현하며, HTTP를 지원하는 프로그래밍 언어로 클라이언트, 서버를 구현할 수 있다.
- 즉, REST API를 제작하면 델파이 클라이언트 뿐만 아니라, 자바, C#, 웹 등을 이용해 클라이언트를 제작할 수 있다.

<br />

## 👨🏻‍💻 REST API

- REST API 설계 시 가장 중요한 항목은 다음의 2가지다.

```
  1. URI는 정보의 자원을 표현해야 한다.
  2. 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현한다.
```

<br />

### 🏃 REST API 중심 규칙

1. URI는 정보의 자원을 표현해야 한다.
   - resource는 동사보다는 명사를, 대문자보다는 소문자를 사용한다.
   - resource의 Document 이름은 단수 명사를 사용한다. (밑에 설명 참고)
   - resource의 Collection은 복수 명사를 사용한다. (밑에 설명 참고)
   - resource의 Store 이름은 복수 명사를 사용한다.

```
  👎
  GET /members/delete/1
```

- 위에서 BAD는 REST를 제대로 적용하지 않은 URI이다. URI는 `자원을 표현하는데 중점`을 두어야 한다. delete와 같은 행위에 대한 `표현이 들어가서는 안된다.`

<br />

2. 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE 등)로 표현
   - URI에 HTTP Method가 들어가면 안된다.
   - URI에 행위에 대한 동사 표현이 들어가면 안된다. (즉, CRUD 기능을 나타내는 것은 URI에 사용하지 않는다.)
   - 경로 부분 중 변하는 부분은 유일한 값으로 대체한다.

```
  👍
  DELETE /members/1
```

- 회원 정보를 가져올 때는 GET, 회원 추가 시의 행위를 표현하고자 할 때는 POST Method를 사용하여 표현한다.

```
  👎
  GET /members/show/1

  👍
  GET /members/1
```

```
  👎
  GET /members/insert/2 - (GET 메서드는 리소스 생성에 맞지 않습니다.)

  👍
  POST /members/2
```

```
  👍
  POST /students - (student를 생성)
  DELETE /students/12 - (id=12인 student를 삭제)
```

<br />

- 즉, `URI`는 `자원을 표현`하는데에 집중하고 `행위에 대한 정의`는 `HTTP Method`를 통해 하는 것이 REST API를 설계하는 중심 규칙이다.

<br />

### 🏃 URI 설계 시 주의할 점

1. 슬래시 구분자(/)는 `계층 관계`를 나타내는 내용이다.

```
  👍
  http://restapi.example.com/houses/apartments
  http://restapi.example.com/animals/mammals/whales
```

<br />

2. URI 마지막 문자로 슬래시(/)를 포함하지 않는다.
   - URI에 포함되는 모든 글자는 리소스의 `유일한 식별자`로 사용되어야 하며 URI가 다르다는 것은 리소스가 다르다는 것이고, 역으로 리소스가 다르면 URI도 달라져야 한다.
   - REST API는 `분명한 URI`를 만들어 통신을 해야 하기 때문에 혼동을 주지 않도록 URI 경로의 마지막에는 슬래시(/)를 사용하지 않는다.

```
  👎
  http://restapi.example.com/houses/apartments/

  👍
  http://restapi.example.com/houses/apartments
```

<br />

3. `하이픈(-)`은 URI 가독성을 높이는데 사용한다.
   - URI를 쉽게 읽고 해석하기 위해, 불가피하게 긴 URI경로를 사용하게 된다면 하이픈(-)을 사용해 가독성을 높일 수 있다.

<br />

4. `밑줄(_)`은 URI에 사용하지 않는다.
   - 글꼴에 따라 다르지만 밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도 한다. 이런 문제를 피하기 위해 밑줄 대신 `하이픈(-)`을 사용한다.(가독성)

<br />

5. `파일 확장자`는 URI에 포함시키지 않는다.
   - REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI안에 포함시키지 않는다.
   - 대신, `Accept header`를 사용한다.

```
  👎
  http://restapi.example.com/members/soccer/345/photo.jpg

  👍
  GET : /members/soccer/345/photo HTTP/1.1 Host: restapi.example.com Accept: image/jpg
```

<br />

### 🏃 리소스 간의 관계를 표현하는 방법

- REST 리소스 간에 연관 관계가 있을 수 있고, 이런 경우 다음과 같은 표현 방법으로 사용한다.

```
    /리소스명/리소스 ID/관계가 있는 다른 리소스명

    GET : /users/{userid}/devices   (일반적으로 소유 ‘has’의 관계를 표현할 때)
```

- 만약에 관계명이 복잡하다면 이를 서브 리소스에 명시적으로 표현하는 방법이 있다. 예를 들어 사용자가 '좋아하는' 디바이스 목록을 표현해야 할 경우이다.

```
  GET : /users/{userid}/likes/devices (관계명이 애매하거나 구체적 표현이 필요할 때)
```

<br />

### 🏃 자원을 표현하는 Collection과 Document

- Collection과 Document에 대해 알면 URI 설계가 한 층 더 쉬워진다.
- Document는 단순히 `문서`로 이해해도 되고, 한 `객체`라고 이해해도 된다.
- Collection은 `문서들의 집합`, `객체들의 집합`이라고 생각하면 이해하는데 도움이 된다.
- Collection과 Document는 모두 `리소스`라고 표현할 수 있으며 `URI에 표현`된다.

```
  http:// restapi.example.com/sports/soccer
```

- 위의 예제를 보면 sports라는 Collection과 soccer라는 Document로 표현되어 있다.

<br />

```
  http:// restapi.example.com/sports/soccer/players/13
```

- 위의 예제는 sports, players라는 2개의 Collection과 soccer, 13(13번 선수)를 의미하는 Document로 URI가 이뤄져 있다.
- 여기서 중요한 점은 Collection은 `복수`로 사용한다. 좀 더 직관적인 REST API를 위해서는 Collection과 Document를 사용할 때 단수, 복수도 지켜준다면 이해하기 쉬운 URI를 설계 할 수 있다.
- 물론, Document는 단수 명사를 사용한다.

<br />

## 👨🏻‍💻 RESTful API

- 일반적으로 REST라는 아키텍처를 구현하는 웹 서비스를 나타내기 위해사용되는 용어
  - 즉, `REST API`를 제공하는 웹 서비스를 `RESTful`하다고 할 수 있다.
- RESTful은 REST를 REST답게 쓰기 위한 방법으로, 누군가가 공식적으로 발표한 것이 아니다.
  - 즉, REST 원리를 따르는 시스템은 RESTful이란 용어로 지칭 된다.

<br />

### 🏃 RESTful API의 목적

- 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것
- RESTful한 API를 구현하는 근본적인 목적이 성능 향상에 있는 것이 아니라 `일관적인 컨벤션`을 통한 API의 `이해도` 및 `호환성`을 높이는 것이 주 동기이다.
- 이는 결국, 성능이 중요한 상황에서는 굳이 RESTful 한 API를 구현할 필요는 없다는 의미이다.

<br />
<br />
<br />

### 🔍 참고) HTTP Method의 역할

- GET, POST, PUT, DELETE 이 4가지의 Method를 가지고 CRUD를 할 수 있다.

![restful](https://user-images.githubusercontent.com/64779472/121723265-3fd1b780-cb21-11eb-85be-5079e1f9f804.PNG)

<br />

### 🔍 참고) HTTP 응답 상태 코드

- 잘 설계된 REST API는 URI만 잘 설계된 것이 아닌 그 리소스에 대한 응답을 잘 내어주는 것 까지 포함된다.
- 정확한 응답의 상태 코드만으로도 많은 정보를 전달할 수가 있기 때문에 응답의 상태코드 값을 명확히 보내주는 것도 중요한 일이 될 수 있다.

<br />

![200](https://user-images.githubusercontent.com/64779472/121725048-b4a5f100-cb23-11eb-99c4-ecab3c83f0b9.PNG)

<br />

![400](https://user-images.githubusercontent.com/64779472/121725050-b5d71e00-cb23-11eb-8d29-ca6f744a9a2e.PNG)

<br />

![300500](https://user-images.githubusercontent.com/64779472/121725054-b7a0e180-cb23-11eb-85b2-fa1a17c6753c.PNG)

<br />

## 참고

https://meetup.toast.com/posts/92 <br />
https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html <br />
