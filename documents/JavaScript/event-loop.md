# 💻 Event Loop

![event-loop](https://user-images.githubusercontent.com/64779472/116123381-e7c02c80-a6fd-11eb-859b-f5375b051f01.PNG)

<br />

## 👨🏻‍💻 JS Engine(상단 그림의 왼쪽)

- 자바스크립트 엔진은 `Memory Heap`과 `Call Stack`으로 구성되어 있다.(ex. 구글의 V8 Engine)
- 자바스크립트는 `단일 스레드(Single Thread) 기반 프로그래밍 언어`인데, 이 의미는 Call Stack이 하나라는 이야기이다.
  - Memory Heap: 메모리 할당이 일어나는 곳(ex. 우리가 프로그램에 선언한 변수, 함수 등이 담겨져 있음)
  - Call Stack: 코드가 실행될 때 쌓이는 곳 Stack 형태로 쌓인다. (Stack은 자료구조 중 하나로, 후입선출(LIFO) 방식이다.)
- 단일 콜 스택을 갖는 다는 의미는, 요청이 `동기적으로 처리`된다는 것을 의미한다.
- 비동기 요청을 처리하기 위해서는 자바스크립트를 실행하는 환경인 `브라우저`나 `Node.js`가 담당한다.

<br />

## 👨🏻‍💻 Web API

- Web API는 JS Engine이 아니다.
- Web API는 브라우저에서 제공하는 API로, DOM, AJAX, Timeout 등이 있다.
- Call Stack에서 실행된 비동기 함수는 Web API를 호출하고, Web API는 콜백 함수를 Callback Queue에 넣는다.

<br />

## 👨🏻‍💻 Event Loop

- Event Loop는 Call Stack과 Callback Queue의 상태를 체크하여, Call Stack이 빈 상태가 되면, Callback Queue의 첫번째 콜백 함수를 Call Stack에 넣는다.
- 위와 같은 반복적인 행동일 틱(Tick)이라고 부른다.
- **과정 정리)**
  1. V8 엔진에서 코드가 실행되면, Call Stack에 쌓인다.
  2. Stack의 후입선출의 룰에 따라 제일 마지막에 들어온 함수가 먼저 실행되며, Stack에 쌓여진 함수가 모두 실행된다.
  3. 비동기 함수가 실행된다면, Web API가 호출된다.
  4. Web API는 비동기 함수의 콜백 함수를 CallBack Queue에 넣는다.
  5. Event Loop는 Call Stack이 빈 상태가 되면 Callback Queue에 있는 첫번째 콜백은 Call Stack으로 이동시킨다.

<br />

## 👨🏻‍💻 Callback Queue

- Callback Queue에는 `Task Queue`와 `Microtask Queue`가 있다.
- Task Queue는 setTimeout(), setInterval(), UI렌더링, requestAnimationFrame()이 담긴다.
- Microtask Queue는 Promise(then), MutaionObserver가 담긴다.
- Event Loop는 우선적으로 Microtask Queue를 확인한다. 만약, Microtask Queue에 콜백이 있다면, 이를 먼저 Call Stack에 담는다. 그리고 Microtask Queue에 처리해야 할 콜백 함수가 없다면, Task Queue에 확인 후 처리한다.

<br />

- **동작 예시 1)**

```js
console.log('script start');

setTimeout(function () {
  console.log('setTimeout');
}, 0);

Promise.resolve()
  .then(function () {
    console.log('promise1');
  })
  .then(function () {
    console.log('promise2');
  });

console.log('script end');
```

<br />

- **결과**

```
  script start
  script end
  promise1
  promise2
  setTimeout
```

<br />

- 위 결과의 이유는 Promise는 Microtask Queue에 담기고, setTimeout은 Task Queue에 담기기 때문에, 우선 순위가 높은 Promise의 콜백 함수가 먼저 실행되고, 그 다음 setTimeout의 콜백 함수가 실행된다.

<br />

## 👨🏻‍💻 그림으로 보는 동작 방식

```js
  console.log('콜 스택!');
  setTimeout(() => console.log('태스크 큐!'), 0);
  Promise.resolve().then(() => console.log('마이크로태스크 큐!'));

  //결과
  콜 스택!
  마이크로태스트 큐!
  태스트 큐!
```

<br />

![eventlooptask1](https://user-images.githubusercontent.com/64779472/116126402-92861a00-a701-11eb-9965-1695d35eda8a.png)

- 제일 먼저, '스크립트 실행' Task가 Task Queue에 들어간다.

![eventlooptask2](https://user-images.githubusercontent.com/64779472/116126407-93b74700-a701-11eb-80a1-78a2b7476d48.png)

- 이후, 이벤트 루프가 그 Task를 가져와서 로드 된 스크립트를 실행시킨다. 따라서 맨 처음에 **console.log**가 실행 된다.

![eventlooptask3](https://user-images.githubusercontent.com/64779472/116126408-93b74700-a701-11eb-9e8d-6dbc6b8f77d5.png)

- 그 다음, setTimeout() 이 Call Stack으로 가고 Web API가 이를 받아서 타이머를 동작시킨다.

![eventlooptask4](https://user-images.githubusercontent.com/64779472/116126412-944fdd80-a701-11eb-970c-5a147c91f2c2.png)

- 타이머가 끝나면, setTimeout()의 콜백 함수를 Task Queue에 넣는다.

![eventlooptask5](https://user-images.githubusercontent.com/64779472/116126414-944fdd80-a701-11eb-9ee2-9f639c9a126f.png)

- Promise가 Call Stack으로 가고 콜백 함수를 Microtask Queue에 넣는다.

![eventlooptask6](https://user-images.githubusercontent.com/64779472/116126415-94e87400-a701-11eb-81bb-6fa5592f8253.png)

- 이벤트 루프는 Microtask Queue에서 제일 오래된 Task인 Promise의 콜백 함수를 가져와 Call Stack에 넣는다.

![eventlooptask7](https://user-images.githubusercontent.com/64779472/116126417-95810a80-a701-11eb-9bb0-0b92e38603b6.png)

- Promise의 콜백 함수가 끝나고 Task Queue에서 제일 오래 된 Task인 setTimeout()의 콜백 함수를 가져와 Call Stack에 넣는다.

![eventlooptask8](https://user-images.githubusercontent.com/64779472/116126419-95810a80-a701-11eb-8de9-19ae91d34d07.png)

- setTimeout()의 콜백 함수가 끝나면 Call Stack이 비게 되고 프로그램이 종료된다.

<br />

## 참고

https://github.com/baeharam/Must-Know-About-Frontend/blob/master/Notes/javascript/event-loop.md <br /> https://velog.io/@thms200/Event-Loop-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84 <br />
