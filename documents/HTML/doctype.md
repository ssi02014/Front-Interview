# 💻 HTML - DOCTYPE
<br />

## 👨🏻‍💻 DOCTYPE
- DOCTYPE은 Document Type의 약어이다.
- HTML은 `<html>`, `<head>`, `<body>`로 구성되어 있다. 그러나 중요한 또 하나 DOCTYPE이 있다. DOCTYPE은 `<html>` 태그 보다 먼저 선언하는 것이 일반적이며, `<!DOCTYPE html ...>` 형식으로 선언한다. 이때, 태그가 아니기 때문에 `</>`과 같이 닫아주지 않아도 된다.
- HTML은 한 개의 종류가 아니라 여러 종류가 있다. HTML 4.01 Strict, HTML 4.01 Transitional, XHTML 1.0 등이 있다. HTML 종류에 따라 같은 코드의 HTML 파일을 실행했을 때 다른 결과가 나타난다.
- 그렇기 때문에 `<!DOCTYPE html ...>`을 선언해서 어떤 HTML 표준을 따라 작성되었음을 브라우저에 알려준다. 만약 DOCTYPE을 선언하지 않으면 브라우저는 사용자가 HTML 4.01인지, XHTML 1.0인지, HTML5 인지 무엇을 기반으로 코드를 작성했는지 알 수가 없다.
- DOCTYPE을 선언할 경우 이를 `Standards Mode(표준 모드)`라 하고, 선언 하지 않는 경우를 `Quirks Mode(비표준 모드, 호환 모드)`라고 한다. 호환 모드의 경우 각 브라우저마다 문서를 나타내는 방식이 다르기 때문에 `크로스 브라우징 이슈`가 심각하다.

<br />

- 표준 모드 소스 코드(HTML 5)
```html
<!DOCTYPE html>
<html>
  <head>
  </head>
  <body>
  </body>
</html>
```

<br />

- 비표준 모드 소스 코드
```html
<html>
  <head>
  </head>
  <body>
  </body>
</html>
```

<br />

## 👨🏻‍💻 DTD
- `DTD(Document Type Definition)`란 문서 형식을 정의해놓은 것으로 DOCTYPE을 명시할 때 사용한다. 즉, HTML 문서가 어떤 문서 형식을 따르는지 DOCTYPE에서 DTD를 지정하는 것이다.
- 밑에 예시를 참고하고 더 자세하게 알고 싶다면 [W3C Recommended list of Doctype declarations](https://www.w3.org/QA/2002/04/valid-dtd-list.html) 를 확인한다.

<br />

- XHTML 1.1
- XHTML 1.0
  - Strict DTD
  - Transitional DTD
  - Frameset DTD 
- HTML 4.01
  - Strict DTD
  - Transitional DTD
  - Frameset DTD
- HTML 5

<br />

- 현 시점에선 `HTML5`의 DTD DOCTYPE을 명시하는 것이 제일 바람직하다.
```html
<!DOCTYPE html>
```

<br />

## 참고
https://github.com/baeharam/Must-Know-About-Frontend/blob/master/Notes/html/doctype.md <br />
https://developerjio.tistory.com/entry/HTML-DOCTYPE%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B4%EB%A9%B0-%EC%99%9C-%EC%82%AC%EC%9A%A9%ED%95%A0%EA%B9%8C <br />
https://theqoop.tistory.com/265 <br />
