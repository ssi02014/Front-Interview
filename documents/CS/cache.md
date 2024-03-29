# 💻 캐시(Cache)

## 👨🏻‍💻 캐시 메모리(Cache Memory)

![image](https://user-images.githubusercontent.com/64779472/142031761-048384b6-2a1f-4d2b-8ca6-355ae866876b.png)

- 캐시 메모리란, 메인 메모리와 CPU간의 데이터 속도 향상을 위한 중간 버퍼 역할을 하는 CPU내, 외에 존재하는 메모리이다. 전체 시스템의 성능의 개선을 시킬 수 있는 메모리이다.
- 쉽게 말하면, 메인 메모리와 CPU 사이에서 빠르게 전달을 위해서 미리 데이터들을 저장해두는 좀더 빠른 메모리이다.
- 보통 CPU는 데이터를 가져오기 위해 캐시 메모리 -> 메모리 -> 보조기억장치 순으로 접근한다.
- 캐시 메모리는 저장 공간이 작고 비용이 비싼 대신 빠른 성능을 제공한다.
- 원하는 데이터가 캐시 메모리에 존재할 경우 해당 데이터를 반환하며, 이러한 상황을 `Cache Hit`라고 한다.
- 원하는 데이터가 캐시 메모리에 존재하지 않을 경우 DBMS 또는 서버에 요청을 해야하며 이를 `Cache Miss`라고 한다.
- 캐시는 반복적으로 데이터를 사용하는 경우에, 지속적으로 DBMS 혹은 서버에 요청하는 것이 아니라 캐시 메모리에 데이터를 저장하였다가 불러다 쓰는 것이다.

<br />

- 캐시는 다음과 같은 경우에 고려하면 좋다.
```
  1. 접근 시간에 비해 원래 데이터를 접근하는 시간이 오래 걸리는 경우(서버의 균일한 API 데이터)
  2. 반복적으로 동일한 결과를 돌려주는 경우(이미지, 썸네일 등)
```

<br />

### 🏃 캐시의 필요성

![image](https://user-images.githubusercontent.com/64779472/142032614-8505d42b-7634-496a-94bc-fc254e3590b5.png)

- 위의 그래프는 `Long Tail`법칙의 그래프이다. Long Tail 법칙은 `20%의 요구가 시스템 리소스의 대부분을 사용한다.`는 법칙이다. 
- 그렇기 때문에 20%의 기능에 Cache를 이용함으로써 리소스 사용량은 대폭 줄이고, 성능은 대폭 향상시킬 수 있다.

<br />

## 👨🏻‍💻 캐시(Cache)의 종류
### 🏃 Local Cache
- Local 장비 내에서만 사용되는 캐시로, Local 장비의 리소스를 이용한다.
- Local에서만 작동하기 때문에 속도가 빠르다.
- Local에서만 작동하기 때문에 다른 서버와 데이터 공유가 어렵다.

<br />

### 🏃 Global Cache
- 여러 서버에서 Cache Server에 접근하여 사용하는 캐시로 분산된 서버에서 데이터를 저장하고 조회할 수 있다.
- 네트워크를 통해 데이터를 가져오므로, Local Cache에 비해 상대적으로 느리다.
- 별도의 Cache서버를 이용하기 때문에 서버 간의 데이터 공유가 쉽다.

<br />

## 👨🏻‍💻 웹 캐시(Web Cache)
- 웹 캐시란 사용자가 웹 사이트(Server)에 접속할 때, 정적 컨텐츠(Image, HTML, CSS 등)를 특정 위치에 저장하여, 웹 사이트 서버에 해당 컨텐츠를 매번 요청하여 받는 것이 아니라, 특정 위치에서 불러옴으로써 사이트 응답시간을 줄이고, 서버 트래픽 감소 효과를 보는 것이다.
- 서버를 통해서 내려 받는 양이 적어지니 응답 시간이 감소하고, 네트워크 트래픽이 감소되니 Server와 Client 모두 win-wind 할 수 있는 최고의 TradeOff이다.

<br />

## 👨🏻‍💻 웹 캐시(Web Cache)의 종류
### 🏃 Browser Caches
- 브라우저 또는 HTTP요청을 하는 Client Application에 의해 내부 디스크에 캐쉬
- Cache된 Resource를 공유하지 않는 한 개인에 한정된 Cache
- 브라우저의 Back버튼 또는 이미 방문한 페이지를 재 방문하는 경우 극대화

<br />

### 🏃 Proxy Caches
- Browser Cache와 동일한 원리로 동작하며 Client나 Server가아닌 네트워크 상에서 동작.
- 큰회사나 IPS의 방화벽에 설치 되며 대기시간 & 트래픽 감소, 접근정책 & 제한 우회, 사용률 기록등 수행
- 한정된 수의 클라이언트을 위하여 무한대의 웹서버의 컨텐츠를 캐쉬

<br />

### 🏃 Gateway Caches
- 서버 앞 단에 설치되어 요청에 대한 캐쉬 및 효율적인 분배를 통해 가용성, 신뢰성, 성능등을 향상
- Encryption / SSL acceleration, Load balancing, Serve/cache static content, Compression등을 수행
- 무한대의 클라이언트들에게 한정된 수(또는 하나)의 웹서버 컨텐츠를 제공

<br />

## 참고
https://mangkyu.tistory.com/69 <br />
https://hahahoho5915.tistory.com/33 <br />
https://wikidocs.net/65523 <br />