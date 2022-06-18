# 💻 Brower Rendering Process

<br />

## 👨🏻‍💻 브라우저의 주요 기능

- 브라우저의 주요 기능은 사용자가 선택한 자원을 서버에 요청하고 브라우저에 표시하는 것이다.
- 자원은 보통 HTML 문서지만 PDF나 IMAGE 또는 다른 형태일 수 있다.
- 자원의 주소는 URI(Uniform Resource Identifier)에 의해 정해진다.
- 브라우저는 HTML과 CSS 명세에 따라 HTML 파일을 해석해서 표시하는데 이 명세넌 웹 표준화 기구인 W3C(World Wide Web Consortium)에서 정한다.

<br />

## 👨🏻‍💻 브라우저의 기본 구조

- 사용자 인터페이스: 주소 표시줄, 이전/다음 버튼, 북마크 메뉴 등 요청한 페이지를 보여주는 창을 제외한 나머지 모든 부분
- 브라우저 엔진: 사용자 인터페이스와 렌더링 엔진 사이의 동작을 제어
- 렌더링 엔진: 요청한 콘텐츠를 표시. 예를 들어 HTML을 하면 HTML과 CSS를 파싱하여 화면에 표시함
- 통신: HTTP 요청과 같은 네트워크 호출에 사용됨. 이것은 플랫폼 독립적인 인터페이스이고 각 플랫폼 하부에 실행 됨.
- UI 백엔드: 콤보 박스와 창 같은 기본적인 장치를 그림. 플랫폼에서 명시하지 않은 일반적인 인터페이스로서, OS 사용자 인터페이스 체계를 사용.
- 자바스크립트 해석기: 자바스크립트 코드를 해석하고 실행
- 자료 저장소: 자료를 저장하는 계층이다. 쿠키를 저장하는 것과 같이 모든 종류의 자원을 하드 디스크에 저장할 필요가 있다. HTML5 명세에는 브라우저가 지원하는 '웹 데이터 베이스'가 정의되어 있다.

<br />

![browser-element](https://user-images.githubusercontent.com/64779472/116430413-c6884900-a881-11eb-8a36-964a9818829d.PNG)

<br />

## 👨🏻‍💻 렌더링이란?

- HTML, CSS, JS 등 개발자가 작성한 문서를 브라우저에서 출력하는 과정을 말한다.

<br />

## 👨🏻‍💻 브라우저의 렌더링 과정

![스크린샷 2022-06-18 오후 11 37 01](https://user-images.githubusercontent.com/64779472/174443258-cac89e0b-9ca5-485e-b4de-b37aa27e289f.png)

1. 브라우저는 HTML, CSS, JS 등 렌더링에 필요한 리소스를 요청하고 서버로부터 응답을 받는다.

<br />

![dom](https://user-images.githubusercontent.com/64779472/116430954-431b2780-a882-11eb-85c9-c077f48670bc.PNG)

2. 브라우저 렌더링 엔진은 응답된 HTML을 파싱 후, `DOM(Document Object Model) 트리` 구축

<br />

![cssom](https://user-images.githubusercontent.com/64779472/116431082-65ad4080-a882-11eb-95b4-a8277b373594.PNG)

3. CSS도 파싱 후, `CSSOM(CSS Object Model) 트리` 구축

<br />

![render-tree](https://user-images.githubusercontent.com/64779472/116431313-a311ce00-a882-11eb-8ab1-f794fc3e7c66.PNG)

4. DOM과 CSSOM을 조합해 `렌더 트리(Render Tree)` 구축

<br />

5. Layout 단계: `뷰 포트(Viewport)` 내에서 각 노드들의 정확한 위치와 크기를 계산 (즉, 브라우저 화면의 어떤 위치에 어떤 크기로 출력될지 계산 하는 단계)

<br />

6. Paint 단계: Layout단계에서 계산한 위치/크기를 기반으로 화면에 그리는 단계이다.

<br />

7. Composite 단계: 렌더링 과정의 마지막 단계로 각 `레이어를 합성하는 단계`이다. 브라우저가 화면을 그릴 때(Layout, Paint) 각 레이어로 쪼개져서 진행된다. 그리고 이렇게 여러 개로 쪼개진 레이어들을 하나로 합치는 최종적으로 하나의 화면을 그려주는게 이 Composite단계이다.

## 👨🏻‍💻 렌더링에 관련된 추가적인 정보

### 🏃 CSS가 HTML 문서 상단에 배치되면 유리한 점

- 브라우저가 전달받는 HTML 문서는 위에어 아래로 처리되기 때문에 CSS를 HTML 문서 상단에 배치하면 렌더링 엔진이 CSS를 이용하여 렌더 트리를 구성하는 과정에서 조금이라도 빨리 스타일 정보를 제공받기 때문에 이 편이 조금 더 유리하다.
- 따라서, `body` 태그가 선언되기 전 `head` 태그에서 선언하는 것이 일반적이다.

<br />

### 🏃 JS를 HTML 하단에 배치하면 유리한 점

- CSS의 경우 HTML 문서 상단에 배치하는 것이 유리하지만 JS의 경우에는 문서 하단에 배치한느 것이 유리하다.
- JS 영역을 처리하는 과정에는 모든 작업이 정지하고 해석과 구현을 하는 데에 우선적으로 대응하기 때문이다.
- 따라서 DOM Tree 구성과 Render Tree 구성을 최대한 진행한 뒤 JS를 처리하는 것이 유리하다.

<br />

## 참고

https://d2.naver.com/helloworld/59361 <br />
https://github.com/baeharam/Must-Know-About-Frontend/blob/master/Notes/frontend/browser-rendering.md <br />
https://velog.io/@st2702/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EC%9D%98-%EB%A0%8C%EB%8D%94%EB%A7%81-%EA%B3%BC%EC%A0%95 <br />
