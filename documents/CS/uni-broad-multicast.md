# 💻 유니캐스트, 브로드캐스트, 멀티캐스트

## 👨🏻‍💻 유니캐스트, 브로드캐스트, 멀티캐스트

### 유니캐스트(Unicast)

![스크린샷 2022-06-20 오후 10 30 43](https://user-images.githubusercontent.com/64779472/174612654-e7d99140-5f67-491e-bb7a-da391624f2f2.png)

- 유니캐스트는 1:1 통신을 말하며 LAN 통신에서 송신자의 MAC과 수신자의 MAC 주소를 알 때 메시지를 전달한다.
- 출발지와 목적지가 정확해야 하는 `일대일 통신`이다.
- 송신 노드 하나가 수신 노드 하나에 데이터를 전송하는 일대일 방식
- MAC <-> MAC에서 수신하는 입장에서 자신의 MAC과 비교하여 동일하지 않으면 해당 통신을 받지 않기 때문에 `CPU 성능을 저하시키지 않는다.`

<br />

### 브로드캐스트(Broadcast)

![스크린샷 2022-06-20 오후 10 31 36](https://user-images.githubusercontent.com/64779472/174612787-d83623f3-05cd-4f7d-9f00-9e306ba64b7d.png)

- 정보의 전달 과정에서 `송신자는 누군지 확실히 아나 수신자를 특정하지 않을 때`, `네트워크에 있는 모든 서버에게 정보를 알려야할 때`, `라우터끼리 정보를 교환하거나 새로운 라우터를 찾을 때`, 브로드 캐스팅 방식을 사용한다.
- 즉, 같은 네트워크에 있는 `모든 장비들에게 보내는 통신`이다.
- 송신 노드 하나가 네트워크에 연결된 수신 가능한 모든 노드에 데이터를 전송
- 모든 장비들에게 데이터를 전송하기 때문에 나에게 필요한 정보인지 확인하는 과정에서 CPU가 사용되기 때문에 `과도한 브로드캐스트는 네트워크 및 PC 성능을 떨어뜨릴 수 있다.`

<br />

### 멀티캐스트(Multicast)

![스크린샷 2022-06-20 오후 10 32 50](https://user-images.githubusercontent.com/64779472/174613014-96873e6b-b600-4d37-8240-c34f27826bc6.png)

- 한번의 송신으로 메시지나 정보를 목표한 여러 컴퓨터에 전송하는 것을 말한다. `일대다 전송 방법`이다.
- 여러 명에게 보내야 할 경우에 사용하는 방식으로 `유니캐스트`와 `브로드캐스트`를 합쳐놓은 듯한 개념이다.
- 송신 노드 하나가 네트워크에 연결된 `하나 이상의 수신노드에 데이터를 전송`한다.
- 유니 캐스트는 MAC을 전부 확인해서 같은걸 100번 보내야 하니, 보내야 하는 PC가 많을수록 네트워크 부하가 커지고, 브로드캐스트는 해당 네트워크 전체에 보내게 되니 관련없은 PC에서 CPU 사용량이 증가하게 되는 단점이 있다.
- 멀티 캐스트는 특정 그룹을 지정해서 해당 그룹원에게만 보내는 방식을 사용한다.

<br />
