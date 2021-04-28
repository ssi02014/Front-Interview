# 💻 Event Delegation(with. Event bubbling, Capturing)
<br />

## 👨🏻‍💻 이벤트 버블링과 캡쳐링
### 🏃 이벤트 버블링
- `이벤트 버블링`이란, 하위 엘리먼트에 이벤트가 발생할 때 그 엘리먼트로부터 시작해서 상위 요소까지 이벤트가 전달되는 방식을 말한다.
- 부연 설명을 하자면, 한 요소에 이벤트가 발생하면, 이 요소에 할당된 핸들러가 동작하고, 이어서 부모 요소의 핸들러가 동작한다. 가장 최상단의 조상 요소를 만날 때 까지 이 과정이 반복되면서 요소 각각에 할당된 핸들러가 동작한다.

<br />

```html
  <style>
    body * {
      margin: 10px;
      border: 1px solid blue;
    }
  </style>

  <form onclick="alert('form')">FORM
    <div onclick="alert('div')">DIV
      <p onclick="alert('p')">P</p>
    </div>
  </form>
```

<br />

- 가장 안쪽의 `<p>`를 클릭하면 순서대로 다음과 같은 일이 벌어진다.
1. `<p>`에 할당된 onclick 핸들러가 동작
2. 바로 바깥의 `<div>`에 할당된 onclick 핸들러가 동작
3. 그 바깥의 `<form>`에 할당된 핸들러가 동작
4. document 객체를 만날 때까지, 각 요소에 할당된 onclick 핸들러가 동작한다.

![event-bubling](https://user-images.githubusercontent.com/64779472/116424794-c5085200-a87c-11eb-9872-070dc8d98efb.PNG)

<br />

### 🏃 이벤트 캡처링
- `이벤트 캡처링`이란, 하위 엘리먼트에 이벤트 핸들러가 있을 때, 상위 엘리먼트로부터 이벤트가 발생하기 시작해서 하위 엘리먼트까지 이벤트가 전달되는 방식을 말한다.
- 실제 코드에서 기본 동작은 `이벤트 버블링`이다. 이벤트 캡처링은 실제 코드에서 자주 쓰이지는 않는다. 혹시나 이벤트 캡처링 동작 방식으로 코드를 실행시키려면 `addEventListener()`의 마지막 인자로 `{ capture: true }`를 전달해주면 된다.

<br />

```js
document.querySelector('ul').addEventListener('click', () => console.log('ul 클릭'), { capture: true });
```

<br />

### 🏃 DOM 이벤트 흐름 3가지 단계
1. 캡처린 단계 - 이벤트가 하위 요소로 전파되는 단계
2. 타킷 단계 - 이벤트가 실제 타깃 요소에 전달되는 단계
3. 버블링 단계 - 이벤트가 상위 요소로 전파되는 단계

![event-flow](https://user-images.githubusercontent.com/64779472/116426324-fa616f80-a87d-11eb-99a2-5ba206961c1d.PNG)

<br />

## 👨🏻‍💻 이벤트 위임
- 이벤트 위임은 비슷한 방식으로 여러 요소를 다뤄야 할 때 주로 사용된다. 하위 엘리먼트들이 여러개 있을 때, 하위 엘리먼트들에 각각 이벤트 핸들러를 달지 않고 상위 엘리먼트에 이벤트 핸들러를 달아 하위 엘리먼트들을 제어하는 방식이다.
- 공통 조상에 할당한 핸들러에서 `event.target`을 이용하면 실제 어디서 이벤트가 발생했는지 알 수 있다.
- 이 패턴으로 얻는 장점은 다음과 같다.
  1. 동적으로 엘리먼트를 추가할 때마다 핸들러를 고려할 필요가 없다.
  2. 상위 엘리먼트에 하나의 이벤트 핸들러만 추가하면 되기 때문에 코드가 훨씬 깔끔하다.
  3. 메모리에 있게되는 이벤트 핸들러가 적어지기 때문에 퍼포먼스 측면에 이점이 있다.

  ```html
    <ul onclick="alert('ul')">
      <li>첫번째</li>
      <li>두번째</li>
      <li>세번째</li>
    </ul>
  ```

<br />

- `li`에 각각 핸들러를 달지 않고 상위 엘리먼트인 `ul`에만 달은 것을 확인 할 수 있다. 무조건 이벤트 위임이 좋은 것은 아니기 때문에 상황에 맞춰 사용하면 된다.

<br />

## 참고
https://ko.javascript.info/bubbling-and-capturing <br />
https://github.com/baeharam/Must-Know-About-Frontend/blob/master/Notes/javascript/event-delegation.md <br />
https://ko.javascript.info/event-delegation <br />