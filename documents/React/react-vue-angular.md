# 💻 React vs Vue vs Angular

![리뷰앵](https://user-images.githubusercontent.com/64779472/118085582-9900db00-b3fd-11eb-822c-25fb79399bda.PNG)

<br />

## 👨🏻‍💻 리액트(React)

### 🏃 리액트(React) 특징

- 리액트는 페이스북에서 관리하는, 리액트는 웹 페이지의 컴포넌트를 렌더링하고 빌드하는데 초점을 둔, 가장 인기 있는 `자바스크립트 라이브러리`이다.
- UI 라이브러리이기 때문에 리액트 자체만으로 전역 상태 관리, 라우팅, 빌드 시스템 등을 지원하지 않는다. 따라서, 리액트에서 앞선 기능들을 사용하려면 Redux, Mobx, react-router 등을 `추가해서 사용`해야 한다.
- `크로스 플랫폼(Cross-Platform)` 애플리케이션이나 싱글 페이지 어플리케이션(SPA)을 개발할 때 사용된다.
- `Virtual Dom` 사용
- JS로 모든 것을 구현할 수 있다. JSX와 styled-components와 같은 외부 라이브러리를 이용해 js로 마크업과 스타일을 구현한다.

<br />

### 🏃 Data Flow

- React는 데이터 흐름이 한 방향으로 흐르는 `단방향 데이터 흐름`을 가진다.

<br />

### 🏃 Component 기반 구조

- 리액트는 UI(View)를 `여러 컴포넌트`로 쪼개서 만든다.
- 한 페이지 내에서도 여러 각 부분을 독립된 컴포넌트로 만들고, 이 컴포넌트를 조합해 화면을 구성한다.
- 컴포넌트 단위로 쪼개져 있기 때문에 전체 코드를 파악하기가 상대적으로 쉽다.
- 기능 단위, UI 단위로 캡슐화시켜 코드를 관리하기 때문에 재사용성이 높다.
- 코드를 반복 사용할 필요 없이 import해 사용하면 된다는 간편함이 있으며, 애플리케이션이 복잡하더라도 코드의 유지보수, 관리가 용이하다.

<br />

### 🏃 Virtual DOM

![vdom](https://user-images.githubusercontent.com/64779472/118092148-ab334700-b406-11eb-9de1-cff2f32cfc02.PNG)

<br />

- `DOM`은 Document Object Model의 약자이다. DOM은 HTML, CSS, XML 등을 트리 구조로 인식하고, 데이터를 객체로 간주하고 관리한다.
- 리액트는 이 DOM Tree 구조와 같은 구조체를 Virtual DOM으로 가지고 있는다.
- Virtual DOM은 가상의 Doucment Object Model을 말한다.
- 이벤트가 발생할 때마다 Virtual DOM을 만들고, 다시 그릴 때마다 실제 DOM과 비교하고 전후 상태를 비교해, 변경이 필요한 최소한의 변경사항만 실제 DOM에 반영해, 앱의 효율성고 속도를 개선한다.

<br />

### 🏃 Props and State

- Props란 부모 컴포넌트에서 자식 컴포넌트로 전달해 주는 데이터를 말한다.
- 읽기 전용 데이터이며, 자식 컴포넌트에서 전달받은 props는 변경이 불가능하고 props 를 전달해준 최상위 부모 컴포넌트만 props를 변경할 수 있다.

<br />

## 👨🏻‍💻 뷰(Vue)

### 🏃 뷰(Vue) 특징

- Evan You가 만들었으며, 2014년 릴리즈를 시작으로 꾸준히 발전하고 있는 `자바스크립트 프레임워크`이다.
- 컨트롤러 대신 뷰 모델을 가지는 `MVVM(Model-View-ViewModel)` 패턴을 기반으로 디자인되었으며, 재사용이 가능한 UI들을 묶어서 사용할 수 있다.
- `Vitual DOM`을 사용한다.
- Angular와 React에 비해 매우 작고 가벼우며 복잡도가 낮습니다.
- Template와 Component를 사용하여 재사용이 가능한 사용자 인터페이스를 묶고 View Layer를 정리하여 사용한다.

<br />

### 🏃 MVVM(Model-View-ViewModel)

![MVVM](https://user-images.githubusercontent.com/64779472/118091383-b9cd2e80-b405-11eb-843d-ea142976e23c.PNG)

<br />

- `Model - View - ViewModel`의 줄임말로 로직과 UI의 분리를 위해 설계된 패턴이다.
- 웹페이지는 DOM과 JS로 만들어지게 되는데 DOM이 View의 역할을 하고, 자바스크립트가 Model의 역할을 한다.
- ViewModel이 없는 경우에는 직접 Model과 View를 연결해야 한다. 그러나 ViewModel이 중간에서 연결해주는 것이 MVVM 모델이다.

<br />

### 🏃 Component

![component-vue](https://user-images.githubusercontent.com/64779472/118091322-a0c47d80-b405-11eb-9bfd-85e4216d1cf4.PNG)

<br />

- 화면에 비춰지는 뷰의 단위를 쪼개어 재활용이 가능한 형태로 관리하는 것이 `컴포넌트` 입니다.
- Vue에서, 컴포넌트는 미리 정의된 옵션으 가진 `Vue 인스턴스 `입니다.
- 전역 등록과 지역 등록이 존재합니다.
- Vue는 재사용이 가능한 컴포넌트로 웹 페이지를 구성할 수 있습니다.
- 확장자가 .vue인 단일 파일에 HTML, JS, CSS 코드로 구성하여 사용합니다.

<br />

### 🏃 Vue 인스턴스

- `new Vue`로 선언하여 만들어진 객체를 `Vue 인스턴스`라고 한다.
- el: 태그에 지정한 ID, 클래스명, 태그명으로 해당 태그와 vue 인스턴스를 연결하는 옵션
- data: key와 value를 지정하는 JSON 형식으로 데이터 입력 옵션
- computed: getter/setter를 지정하는 옵션이다.

```
<div id = “app”
    {{message}}
</div>

<script>
  let model = {
      message : “뷰 생성”
  }

  new Vue({
      el : ‘#app’,
      data : model
  })
</script>
```

<br />

## 👨🏻‍💻 앵귤러(Angular)

### 🏃 앵귤러(Angular) 특징

- `Google`에서 만든 SPA(Single Page Application)방식의 프론트엔드 개발을 위한 `자바스크립트 프레임워크` 이다.
- 웹 애플리케이션은 물론 모바일 웹, 네이티브 모바일과 데스크탑 애플리케이션까지 프론트엔드 개발에 필요한 `대부분의 기능을 갖추고 있다.`
- 사용언어는 TypeScript 혹은 JS의 ES6을 사용할 수 있지만, 개발 그룹측에서는 `TypeScript를 사용할 것을 권장`하고 있다.
- 리액트와 뷰와 마찬가지로 `컴포넌트 기반 개발`을 한다.
- 단방향 또는 양방향의 선택적 `데이터 바인딩` 지원
- 디렉티브(Directive)와 서비스, 의존성 주입(DI, Dependency Injection)의 간소화
- `Angular CLI(Command Line Interface)` 제공한다. 즉, 개발 도구 통합 및 개발 환경 구축 자동화. 명령어를 통해 프로젝트 생성, 빌드, 테스트, 구성요소 추가 등을 간편하게 이용

<br />

## 참고

https://ryublock.tistory.com/41
https://wikidocs.net/17701
https://kjwsx23.tistory.com/526
https://brunch.co.kr/@skykamja24/573
