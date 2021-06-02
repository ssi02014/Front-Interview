# 💻 동기(Synchronous)와 비동기(Asynchronous)

<br />

## 👨🏻‍💻 동기(Synchronous)란?
![동기](https://user-images.githubusercontent.com/64779472/120514223-01911580-c408-11eb-8a3d-1d176e9c7420.PNG)

- 말 그대로 `동시에 일어난다`는 의미이다.
- 요청을 보낸 후 해당 요청의 응답(=결과)을 받아야 다음 동작을 실행하는 방식이다.
- 설계가 간단하고 직관적이지만 결과를 볼때까지 아무것도 못하고 대기해야 된다.
- 즉, 요청이 들어온 순서에 맞게 하나씩 처리하는 방식이다. 순서에 맞춰 진행된다는 장점은 있지만, 여러가지 요청을 동시에 처리할 수 없다.
- 실제 cpu가 느려지는 것은 아니지만, 시스템의 전체적인 `효율이 저하`된다고 할 수 있다.

<br />

```js
  function func1() { 
    console.log('func1'); 
    func2(); 
  } 

  function func2() { 
    console.log('func2');
    func3(); 
  } 

  function func3() { 
    console.log('func3');
  } 

  func1(); //출력: func1 func2 func3
  
```
- 위에 예시는 동기식으로 동작하는 코드로, 순차적으로 실행된다.

<br />

## 👨🏻‍💻 비동기(Asynchronous)란?
![비동기](https://user-images.githubusercontent.com/64779472/120514853-af042900-c408-11eb-8dd8-fbf46cf6e5fc.PNG)

- 말그대로 `동시에 일어나지 않는다`는 의미이다.
- 요청을 보낸 후 응답과 관계없이 다음 동작을 실행하는 방식이다.
- 결과과 주어지는데 시간이 걸리더라도 그 시간동안 다른 작업이 가능해 `자원의 효율적인 사용이 가능`하지만, 설계가 동기적 방식보다 복잡하다.

<br />

```js
function func1() { 
  console.log('func1'); 
  func2(); 
} 

function func2() { 
  setTimeout(function() { 
    console.log('func2'); 
  }, 0); 
  func3(); 
} 

function func3() { 
  console.log('func3'); 
} 

func1(); //출력: func1 func3 func2
```

<br />

- 위의 예제는 비동기식으로 처리하는 코드이다. `setTimeout 메서드`가 대표적인 `비동기 함수`이다.

```
  1. 함수 func1 호출되면 함수 func1은 Call Stack에 쌓인다.
  2. 함수 func1은 함수 func2을 호출하므로 함수 func2가 Call Stack에 쌓이고 setTimeout메서드가 호출된다.
  3. setTimeout의 콜백 함수는 즉시 실행되지 않고, 지정 대기 시간만큼 기다리다가 'tick' 이벤트가 발생하면 이벤트 큐로 이동한다.
  4. Call Stack이 비어졌을 때 Call Stack으로 이동되어 실행된다.
```

![비동기처리과정](https://user-images.githubusercontent.com/64779472/120515983-d90a1b00-c409-11eb-9bff-459d55a682f6.gif)

<br />

## 참고
https://sinsomi.tistory.com/entry/%EC%8B%A0%EC%9E%85-%EA%B0%9C%EB%B0%9C%EC%9E%90-%EB%A9%B4%EC%A0%91-%EB%8F%99%EA%B8%B0%EC%99%80-%EB%B9%84%EB%8F%99%EA%B8%B0-%EA%B0%9C%EB%85%90-%EC%B4%88%EC%BD%94%EB%8D%94 <br />
https://velog.io/@dolarge/cs-%EB%8F%99%EA%B8%B0%EC%99%80-%EB%B9%84%EB%8F%99%EA%B8%B0 <br />
https://seunghyun90.tistory.com/51 <br />
https://webclub.tistory.com/605 <br />
https://private.tistory.com/24 <br />