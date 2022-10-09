# 💻 DNS(Domain Name System)

## 👨🏻‍💻 DNS(Domain Name System)란?

![image](https://user-images.githubusercontent.com/64779472/141728326-565e160d-d2bf-4585-8b72-0de4484c2ccb.png)

- `DNS(Domain Name System, 도메인 네임 시스템, 네임서버)`는 인터넷에서 사용되는 주소 체계로 `.com` 또는 `.net`과 같은 특정 최상위 도메인(TLD)의 모든 도메인 네임 및 해당하는 IP주소, 및 관련 값들을 저장, 관리하는 분산 형 데이터베이스 또는 그에 해당하는 기능을 갖는 물리적인 서버 장치를 지칭한다.
- 쉽게 말하면, 네트워크에서 도메인이나 호스트 이름을 숫자로 된 IP주소로 해석해주는 TCP/IP 네트워크 서비스이다.
- 계층 구조를 가지는 분산데이터베이스 구조이다.
- DNS를 운영하는 서버를 `네임서버(Name Server)`라고 한다.
- 예를 들어, 웹 주소 또는 URL을 입력하면 DNS가 입력된 이름과 해당 위치의 IP 주소를 일치시키고 사용자를 해당 사이트에 연결시켜 주는 데이터베이스 서버인 것이다. DNS는 "www.codns.com의 IP주소는 121.125.74.99" 라는 주소 정보를 저장하고 관리하는 `전화번호부`와 비슷하다.


<br />

## 👨🏻‍💻 DNS(Domain Name System)의 과거와 현재
### 🏃 과거

![image](https://user-images.githubusercontent.com/64779472/141728365-2b74fad3-0a7e-462c-a11e-07f4797e9306.png)

- 예전에는 컴퓨터마다 `hosts.txt` 파일을 갖고 있었다.
- 파일 위치: C:\Windows\System32\drivers\etc\hosts
- hosts.txt 파일에는 모든 컴퓨터의 Hostname과 IP Address 정보가 저장되어있다.
- Client는 FTP를 이용해 접근해서 hosts 파일을 다운로드 및 적용하였다. 90년대 초반 Web 서비스 사용자가 폭발적으로 증가하면서 Internet에 연결된 Host 숫자가 크게 늘어났고, 호스트의 수정 및 업데이트가 늦어지고 네트워크 트레픽이 증가하고 호스트 이름을 짓기가 어려워졌다.(이름중복)

<br />

### 🏃 현재
- 분산된 데이터베이스 이용한다. 
- 도메인이 워낙 많기 때문에 전 세계 모든 조직의 도메인정보를 갖고 있는 DNS 서버는 존재하지 않는다.
- 각 조직은 자신들의 도메인 정보를 관리하는 DNS서버를 자체적으로 운영하고, 이러한 수 많은 도메인의 DNS 서버들이 상호 연동되어 있는 Domain Name Space를 구성하게 된다. (DNS란? 섹션 사진)

<br />

## 👨🏻‍💻 DNS 동작과정
- 1. Local(hosts) -> DNS Cashe Table -> DNS Server
- 2. 위 과정에서 없다면 최상위(루트 도메인) -> Top Level Domain -> Second Level Domain -> SubDomain 순으로 IP를 찾음.

<br />

![image](https://user-images.githubusercontent.com/64779472/141729167-f68a66d3-3ce9-4c30-b8c9-77a0db2f1477.png)

- ① ~ ③ Root DNS 서버는 전체 `FQDN` 정보는 알지 못하기 때문에 자신의 하위 Domain인 `COM DNS 서버`에게 주소를 알려준다.
- ④ ~ ⑤ 이를 수신한 Local DNS 서버는 다시 Iterative Query를 사용하여 com DNS 서버에게 정보를 요청하고, com DNS 서버도 자신의 하위 레벨 Domain인 naver.com의 DNS서버 주소를 알려준다.
- ⑥ ~ ⑦ 이를 수신한 Local DNS 서버는 다시 Iterative Query를 사용하여 naver.com DNS 서버에게 www 호스트에 대한 정보를 요청하고, naver.com DNS 서버는 www.naver.com에 대한 IP서버 주소를 알려준다.
- ⑧ Local DNS 서버는 위와 같이 www.naver.com 에 대한 IP주소를 수신 후 자신의 DNS Cache에 등록하고 해당 정보를 요청했던 Client에게 응답메세지로 답변한다.
- 해당 Client는 수신한 www.naver.com의 의 IP주소를 사용하여 실제 해당 서버에 패킷을 전송하게 된다. 그 후 Local DNS 서버는 다른 Client에게 동일한 FQDN에 대한 DNS Query를 수신할 경우 DNS서버 Cache에 등록된 정보로 답변하는 것이 가능하다.

```
  ※ FQDN은 '절대 도메인 네임' 또는 '전체 도메인 네임' 이라고도 불리는 도메인 전체 이름을 표기하는 방식을 의미한다.
  - 웹 사이트 주소를 예로 들어보자.
    1. www.tistory.com 
    2. onlywis.tistory.com

  - 위의 두 주소 중 www 와 onlywis 부분이 '호스트'이고, tistory.com 부분이 '도메인'이다.
  - 호스트와 도메인을 함께 명시하여 전체 경로를 모두 표기하는 것을 FQDN 이라 한다.
```
```
  ※ Iterative Query(반복절 질의)는 local DNS 서버가 다른 DNS 서버에게 쿼리를 보내어 답을 요청하는 작업이다.
  - 자신이 직접 관리하지 않는 질의 요청이 있을 경우 질의에 응답 가능한 NS 목록을 응답한다.
  - 예를들어, 컴퓨터가 질의 한 것이 www.naver.com이라 하면 자신은 com 도메인이고, 자신의 하위 도메인에 naver.com이 있을 때, 컴퓨터에 naver.com을 관리하는 DNS를 알려주는 것
```

## 참고
https://hihighlinux.tistory.com/47 <br />
https://peemangit.tistory.com/52 <br />
http://www.codns.com/b/B05-162 <br />

<br />