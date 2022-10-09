# 💻 DOM(Document Object Model)

## 👨🏻‍💻 문서 객체 모델(Document Object Model: DOM)

- DOM은 `XML`이나 `HTML` 문서에 접근하기 위한 일종의 `인터페이스`이다. DOM은 웹페이지 내의 모든 요소를 정의하고 객체로 나타내준다. 또한, 각각의 `요소에 접근하는 방법`을 제공한다.
- HTML 을 지탱하는 것은 `태그(tag)`이다.
- DOM에 따르면, `모든 HTML 태그는 객체이다.` 태그 하나가 감싸고 있는 자식 태그는 `중첩 태그(nested tag)`라고 부른다. `태그 내의 문자(text)역시 객체이다.`
- 위에 언급된 모든 객체는 `자바스크립트를 통해 접근`할 수 있고, 페이지를 조작할 때 이 객체를 사용한다. 예로, document.body는 `<body>`태그를 객체로 나타낸 것이다.
- document 객체는 페이지의 `기본 진입점 역할`을 한다.

<br />

```js
document.body.style.background = "red";
setTimeout(() => {
  document.body.style.background = "";
}, 3000);
```

<br />

- 위 예제는 document.body의 배경색을 바꾸기 위해 `style.background`를 사용했는데, 이외에도 다양한 프로퍼티가 존재한다. 예로 들어, `innerHTML`(해당 노드의 HTML 콘텐츠), `offsetWidth`(해당 노드의 너비[픽셀]) 등이 있다.

<br />

### DOM 예제

```html
<!DOCTYPE html>
<html>
  <head>
    <title>사슴에 관하여</title>
  </head>
  <body>
    사슴에 관한 진실.
  </body>
</html>
```

- 위와 같은 html 문서가 있다고 가정하면 DOM 구조는 아래와 같다.

<br />

![스크린샷 2022-07-16 오후 11 14 43](https://user-images.githubusercontent.com/64779472/179358534-93747534-7eac-4431-81c8-9573cf970371.png)

<br />

- DOM은 HTML을 위와 같이 `태그 트리 구조`로 표현한다. 위에서 언급했듯이 트리에 있는 `노드는 모두 객체`이다.
- 태그는 요소 노드 (element node)이고, 트리 구조를 구성한다. `<html>`은 루트 노드가 되고, `<head>`와 `<body>`는 루트 노드의 자식 노드가 된다.
- 요소 내의 문자는 `텍스트(text)노드`가 된다. 위 그림에서 `#text`로 확인할 수 있듯이, 텍스트 노드는 `문자열`만 담는다. 또한, 자식 노드를 가질 수 없고, 트리의 끝에서 `잎 노드(leaf node)`가 된다.

![스크린샷 2022-07-16 오후 11 16 41](https://user-images.githubusercontent.com/64779472/179358616-c4f7d1a4-e9b1-4503-a277-9fce66a1f2d5.png)

- 텍스트 노드에 있는 `특수 문자`는 다음과 같은 의미를 가진다.
  - 새 줄(newline) : `↵` (자바스크립트에선 \n로 표시)
  - 공백(space) : `␣`
- 새 줄과 공백은 글자나 숫자처럼 유효한 문자로 취급된다. 따라서 이 두 특수문자는 텍스트 노드가 되고, DOM의 일부가 된다.

<br />

```html
<head>
  <title>사슴에 관하여</title>
</head>
```

<br />

- 위 HTML 문서에서 `<head>`와 `<title>` 사이에 새 줄과 약간의 공백이 있는 걸 볼 수 있는데, 이런 특수문자 역시 `#text` 노드가 된다.

<br />

![스크린샷 2022-07-16 오후 11 19 45](https://user-images.githubusercontent.com/64779472/179358743-1eeef23d-efd0-4c1a-a3a9-cf326292ff14.png)

<br />

### 텍스트 예외 2가지

- 역사으로, `<head>` 태그 이전의 공백과 새 줄은 무시된다.
- HTML 명세서에서 모든 콘텐츠는 `body` 안쪽에 있어야 한다고 했으므로, `</body>`뒤에 무언가를 넣더라도 그 콘텐츠는 자동으로 body 안쪽으로 옮겨진다. 따라서 `</body>` 뒤에는 공백이 있을 수 없다.
- 공백이 없는 텍스트 노드만으로 HTML문서를 구성하려면 아래 예제 처럼 만들어야 한다.

<br />

![스크린샷 2022-07-16 오후 11 23 12](https://user-images.githubusercontent.com/64779472/179358847-908cae33-21d0-4ac5-a818-4fbc6ad4815f.png)

![스크린샷 2022-07-16 오후 11 23 29](https://user-images.githubusercontent.com/64779472/179358856-22e95e7d-50d9-4345-a7ab-883a776f7407.png)

<br />

### 자동 교정

- 기형적인 HTML을 만나면 브라우저는 DOM 생성 과정에서 HTML을 자동으로 교정한다.
- 예를 들어 가장 최상위 태그는 항상 `<html>` 이어야 하는데 문서에 `<html>` 태그가 없는 경우, 문서 최상위에 이를 자동으로 넣어준다. 따라서 DOM에는 `<html>`에 대응하는 노드가 항상있다. `<body>` 도 마찬가지로 적용된다.

<br />

```html
<!DOCTYPE html> 안녕하세요
```

<br />

- 위 예제처럼 HTML 파일에 `안녕하세요`라는 문장 하나만 저장된 상황이라도, 브라우저가 자동으로 `<html>`과 `<body>`로 감싸준다. 또한, `<head>`도 더해준다.

![스크린샷 2022-07-16 오후 11 26 57](https://user-images.githubusercontent.com/64779472/179358975-43c92283-7b78-45ea-badc-c21a8068955d.png)

<br />

- DOM 생성과정에서 브라우저는 문서에 있는 에러 등, 닫는 태그가 없는 에러 등을 `자동으로 처리`한다.
- 아래 예제처럼 정상적인 HTML 형식이 아니고, 태그 짝이 안맞아도 브라우저는 정상적으로 `교정`시켜준다.

<br />

![스크린샷 2022-07-16 오후 11 28 35](https://user-images.githubusercontent.com/64779472/179359037-a3516d15-a5b2-4b11-b6b9-bf143f819dfc.png)

![스크린샷 2022-07-16 오후 11 29 35](https://user-images.githubusercontent.com/64779472/179359073-70059413-ed34-42f3-8991-78fc4fb86f97.png)

<br />

- 추가적으로, 테이블에는 언제나 `<tbody>`가 있다.
- DOM 명세서에선 테이블에는 반드시 `<tbody>`가 있어야 한다고 못 박아 놨지만, HTML에선 `<tbody>`를 생략하곤 한다. 이때 브라우저는 아래와 같이 자동으로 DOM에 `<tbody>`를 만들어준다.

<br />

![스크린샷 2022-07-16 오후 11 31 36](https://user-images.githubusercontent.com/64779472/179359162-8856f4fe-ff10-4575-a7fd-c346318483aa.png)

![스크린샷 2022-07-16 오후 11 31 49](https://user-images.githubusercontent.com/64779472/179359173-b7b90b27-b9a2-4491-98cc-c2d6dc6989b5.png)

<br />

### 기타 노드 타입

- 요소 노드와 텍스트 노드 외에도 다양한 노드 타입이 있다. 예를 들어, `주석도 노드가 된다.`

<br />

```html
<!DOCTYPE html>
<html>
  <head>
    <title>사슴에 관하여</title>
  </head>
  <body>
    사슴에 관한 진실.
    <ol>
      <li>사슴은 똑똑합니다.</li>
      <!-- comment -->
      <li>그리고 잔꾀를 잘 부리죠!</li>
    </ol>
  </body>
</html>
```

<br />

- 위 예제처럼 작성된 HTML 문서가 있다고 가정해보자. 그러면 아래와 같이 DOM 트리가 구성될 것이다.

<br />

![스크린샷 2022-07-16 오후 11 35 34](https://user-images.githubusercontent.com/64779472/179359327-79c9747e-1968-424c-a77c-073e82085450.png)

- 트리에 `주석 노드(comment node)`라는 새로운 노드 타입이 등장했다. 현재`#comment`로 표현되는 주석 노드는 두 텍스트 노드 사이에 존재한다.
- 여기서, 주석은 화면 출력물에 영향을 주지 않는데, 왜 DOM에 추가되는지 의아해할 수 있다. 주석 노드는 HTML에 있다면 반드시 DOM 트리에 추가되어야 한다는 규칙때문에 DOM에 추가 된 것이다.
- 아래 문구를 기억하자.

<br />

```
HTML 안의 모든 것은 (심지어 주석이더라도) DOM을 구성한다.
```

<br />

- HTML 문서 최상단에 있는 `<!DOCTYPE>` 지시자 또한 DOM 노드가 된다. 이 노드는 DOM 트리의 `<html>` 바로 위에 위치한다. (지금까지 예제들에는 표시되지는 않았지만 실제로는 존재하는 노드이다)
- 문서 전체를 나타내는 `document` 객체 또한 DOM 노드이다.
- 참고로 노드 타입은 `총 12가지`인데, 실무에선 주로 `4가지` 노드를 다룬다.
- 실무에서 자주 사용하는 4가지 노드는 다음과 같다.
  - DOM의 진입점이 되는 `문서(document)` 노드
  - HTML 태그에서 만들어지며, DOM 트리를 구성하는 블록인 `요소 노드(element node)`
  - 텍스트를 포함하는 `텍스트 노드(text node)`
  - 화면에 보이지는 않지만, 정보를 기록하고 자바스크립트를 이용해 이 정보를 DOM으로부터 읽을 수 있는 `주석(comment) 노드`

<br />

### 참고

- https://ko.javascript.info/dom-nodes
