# 💻 TCP와 UDP

## 👨🏻‍💻 TCP(Transmission Control Protocol)

- TCP(Transmission Control Protocol)는 인터넷 상에서 데이터를 메시지의 형태로 보내기 위해 IP와 함께 사용하는 프로토콜이다.
- TCP는 `신뢰성`있는 데이터 전송을 지원하는 `연결지향형 프로토콜`이다.
- 3-way-handshaking과정을 통해 연결을 설정하고 4-way handshaking을 통해 해제한다.
- `흐름 제어`와 `혼잡 제어`를 지원하며 데이터의 순서를 보장한다.
- UDP보다는 속도가 느리다.
- 데이터 전송 단위: Segment

<br />

## 👨🏻‍💻 TCP(User Datagram Protocol)

- UDP(User Datagram Protocol)는 데이터를 `데이터그램 단위`로 처리하는 프로토콜이다.
- UDP는 TCP와 달리 `비연결형 프로토콜`이다.
- 연결을 위해 할당되는 논리적인 경로가 없다.
- 신뢰성이 낮다
- TCP보다 속도가 빠르다
- 데이터 전송 단위: Datagram

<br />

## 👨🏻‍💻 TCP, UDP 표 비교

![스크린샷 2022-06-10 오전 1 15 36](https://user-images.githubusercontent.com/64779472/172895138-fb1d119c-a6b5-4886-8711-5f7cf001aba4.png)

<br />

## 참고

https://www.notion.so/CS-54c9355e27e94a84800a5a42a5a63b72
