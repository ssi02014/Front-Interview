# 💻 viewport

## 👨🏻‍💻 반응형 웹(responsive web)

- `반응형 웹(responsive web)이란`, 하나의 웹사이트로 데스크탑PC, 스마트폰, 태블릿 등 접속하는 `디스플레이 종류에 따라 화면의 크기가 자동`으로 변하도록 만든 웹페이지를 말한다.
- 이러한 반응형 웹을 구현할 때 `미디어 쿼리(@media)`를 이용하는데, 미디어 쿼리는 CSS3부터 지원이되는 CSS 기술로 미디어 타입, 화면 크기 등을 기준으로 다른 스타일 시트를 적용할 수 있도록 한다. 이러한 미디어 쿼리를 이용해서 화면 크기가 변할 때 스타일을 바꾸도록 해서 반응형 웹을 구현할 수 있다.
- 보통 모바일 웹을 구현하게 되면 `viewport`라는 것을 고려하게 된다. viewport란 쉽게 말하면 웹페이지가 사용자에게 보여지는 영역을 말한다. 보통 데스크탑에서는 브라우저의 크기를 바꿔서 viewport의 크기를 바꿀 수 있다.
- 하지만 그에 반해, `휴대폰이나 테블릿 같은 경우는 브라우저의 크기를 변경할 수가 없다.` Double Tab이나, Zoom In/Out 으로 viewport의 배율은 변경할 수 있어도 viewport 자체는 바꿀 수가 없다.
- 현대에는 워낙 다양한 휴대폰, 테블릿 기기들이 나오면서 viewport 크기의 종류도 굉장히 다양하다. 따라서 이런 다양한 viewport 크기에 대응하기 위해서는 HTML5에서 제공하는 meta 태그를 이용해 viewport의 크기, Zoom in/out 도 조정할 수 있게 설정해줘야 한다.

<br />

## 👨🏻‍💻 viewport

![스크린샷 2022-05-22 오전 12 21 50](https://user-images.githubusercontent.com/64779472/169658189-006fb99b-3a6a-450c-956d-86352537a3ac.png)

<br />

- `viewport란?` 위에서도 설명했지만 사용자에게 보여지는 영역 즉, `display 상의 표시 영역이다.`
- 이 viewport를 모바일에서 보느냐, 데스크탑 PC에서 보느냐에 따라 해당 디바이스 최적의 화면을 보여주기 위해서는 웹 사이트 설계 시 meta 태그에 viewport 설정이 반드시 필요하다.
- 설정을 해주지 않으면 아래 예제와 같은 차이가 있다.

<br />

![스크린샷 2022-05-22 오전 12 22 32](https://user-images.githubusercontent.com/64779472/169658219-fe53f688-79af-4bd2-a41f-130dc7efc09f.png)

<br />

## 👨🏻‍💻 viewport 설정 값

- meta 태그의 content 값에 따라 다양한 설정 값을 추가해서 모바일 기기에서 실제 렌더링 되는 영역과 viewport의 크기, 줌 레벨을 조절할 수 있다.

### width

- viewport의 `가로 크기`를 조정한다. 일반적인 숫자값이 들어 갈 수도 있고, device-width, device-height와 같은 특정한 값을 사용할 수도 있다. device-width는 100% 스케일에서 CSS 픽셀들로 계산된 화면의 폭을 의미한다.
- 추천 설정 값은 device-width이다.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

<br />

### height

- viewport의 `세로 크기를` 조정한다. 보통 height 값은 넣지 않는게 보편적이다.

```html
<meta name="viewport" content="height=device-height" />
```

<br />

### initial-scale

- 페이지가 처음 로딩될 때 `줌 레벨`을 조정한다. 값이 1.0 일때는 CSS 픽셀과 기기종속적인 픽셀 간의 1:1 관계를 형성한다. 추천 설정 값은 1.0이다.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

<br />

### minimum-scale, maximum-scale

- 각각 줄일 수 있는 최소 크기와 늘릴 수 있는 최대 크기를 의미한다.
- minimum-scale의 default 값은 0.25이며, maximum-scale의 default 값은 1.6이다.
- 사용자가 극단적으로 화면을 줄이거나 늘리는 것을 방지하려면 위의 값들을 설정해주면 된다.

```html
<meta
  name="viewport"
  content="width=device-width, initial-scale=1.0 minimum-scale=1.0"
/>
<meta
  name="viewport"
  content="width=device-width, initial-scale=1.0 maximum-scale=1.0"
/>
```

<br />

### shrink-to-fit

- yes와 no 값을 가지며, 애플 사파리 11 버전에서는 viewport 크기가 보여줘야할 내용보다 작으면 보여줘야 할 내용을 줄여서 보여준다고 한다 그래서 no라는 값을 넣어 줄여주는 것을 방지할 수 있다. default는 yes 이다.

```html
<meta
  name="viewport"
  content="width=device-width, initial-scale=1.0 shrink-to-fit=1.0"
/>
```

<br />

### user-scaleable

- yes 와 no 값을 가지며, 사용자가 `확대/축소` 할 수 있는지를 설정한다. default는 yes 이다.

```html
<meta
  name="viewport"
  content="width=device-width, initial-scale=1.0 user-scalable=no"
/>
```

<br />

### 참고

- https://webty.tistory.com/102
- https://blog.naver.com/ssi02014/222737069169
