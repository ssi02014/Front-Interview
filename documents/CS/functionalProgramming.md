# 💻 함수형 프로그래밍(Functional Programming)
## 👨🏻‍💻 함수형 프로그래밍이란?
- 함수형 프로그래밍은 순수 함수(Pure Function)를 조합하고 상태 공유(Shared State), 변경 가능한 데이터(Mutable Data) 및 부수 효과(Side Effects)을 피하여 소프트웨어를 만드는 프로세스이다.
- 함수형 프로그래밍은 명령형(imperative)가 아닌 선언형(declarative)이며 애플리케이션의 상태는 순수 함수를 통해 전달된다.
- 함수형 프로그래밍은 위에서 정의된 기본 원칙들을 기반으로 소프트웨어를 구성하는 프로그래밍 패러다임이다.

<br />

## 👨🏻‍💻 함수형 프로그래밍의 특징
### 🏃 부수 효과(Side Effect)가 없다.
- 부수 효과란 다음과 같은 변화 또는 변화가 발생하는 작업을 말한다.
```
  1. 변수의 값이 변경 됨
  2. 자료 구조를 제자리에서 수정함
  3. 객체의 필드값을 설정함
  4. 예외나 오류가 발생하며 실행이 중단됨
  5. 콘솔 또는 파일I/O가 발생함
```
- 이러한 부수 효과들을 제거한 함수들을 순수 함수(Pure Function)이라고 한다.

<br />

### 🏃 순수 함수(Pure Function)
- 함수형 프로그래밍에서 사용하는 함수는 이러한 순수 함수들이다.
```
  1. Memory or I/O의 관점에서 부수 효과(Side Effect)가 없는 함수
  2. 함수의 실행이 외부에 영향을 끼치지 않는 함수
```
- 순수 함수(Pure Function)을 이용하면 다음과 같은 효과를 얻을 수 있다.
```
  1. 함수 자체가 독립적이며 부수 효과(Side Effect)가 없기 때문에 Thread에 안정성을 보장받을 수 있다.
  2. Thread에 안정성을 보장받아 병렬 처리를 동기화 없이 진행할 수 있다.
```

<br />

### 🏃 일급 함수(First Class Function)
- 일급 함수라는 말은 함수를 객체로 취급하는 것을 두고 말한다. 더 쉽게 말하면 일반 변수와 같이 취급할 수 있다는 뜻이다. 어떤 값을 변수에 저장하고, 함수를 호출할 때 파라미터로 넘기고, 함수의 결과로 어떤 값을 리턴할 수 있다.
- 일급 함수는 다음과 같은 특징을 갖고있다.
```
  1. 변수나 데이터 구조 안에 담을 수 있다.
  2. 파라미터로 전달할 수 있다.
  3. 반환값으로 사용할 수 있다.
  4. 할당에 사용된 이름과 무관하게 고유한 구별이 가능하다.
```

<br />

```js
  const startCase = function(str) {
    return str.charAt(0).toUpperCase() + str.slice(1);
  };

  startCase('hello'); // Hello
```
- 위 예제처럼 함수를 변수에 할당하는 형태로 선언할 수 있다. 그리고 할당한 변수를 통해서 함수를 호출할 수 있다.

<br />

```js
  document.querySelector('.my-button').addEventListener('click', (event) => {
    console.log('버튼 클릭!');
  });
```
- 함수를 파라미터로도 전달 할 수 있다. 대표적인 예로 이벤트 리스터의 콜백함수이다.

<br />

### 🏃 참조 투명성(Referential Transparency)
- 참조 투명성은 어떤 함수가 같은 파라미터에 대해서 같은 리턴값을 언제나 보장하는 것을 참조 투명성이라고 합니다.
```
  1. 동일한 인자에 대해 항상 동일한 결과를 반환해야 한다.
  2. 참조 투명성을 통해 기존의 값은 변경되지 않고 유지된다.(Immutable Data)
```

<br />

```js
  const negate = (num) => {
    return num * -1;
  }
```
- negate 함수는 숫자를 받아서 음수는 양수로 양수로 음수로 전환하는 함수이다. 위 함수는 같은 입력에 대해서 항상 같은 출력을 받환한다.

<br />

### 🏃 불변성(Immutability)
- 입력받은 파라미터나 외부 변수를 변경하지 않는 것을 불변이라고 한다.
```js
  const replaceSpace = (str) => {
    return str.replace(/(_|-)/, ' ');
  }

  const startCase = (str) => {
    return str.charAt(0).toUpperCase() + str.slice(1);
  }

  const changePartStartCase = (str) => {
    return str.split(' ').map(startCase).join(' ')
  }
```
- 위 예제에서 `replace()`, `toUpperCase()`, `slice()` 모두 새로운 값을 반환한다.
- 새로운 값을 반환하면 입력 받은 값을 오염시키지 않고 새로운 값을 반환하는 함수를 불변이라고 말할 수 있다.
- 즉, 부수 효과(Side Effect)가 없다고 생각할 수 있다.

<br />

## 👨🏻‍💻 순수함수 장점
- 캐시가 가능하다. 항상 같은 입력에 대해서 같은 값을 반환하기 때문에 함수의 로직이 복잡하고 큰 계산이 드는 함수라면 `memoize`를 이용해서 캐시를 할 수 있다.
- 테스트가 아주 쉽다. 같은 입력에 대해서 같은 출력을 내기 때문에 기대하는 값이 명확하기 때문이다.
- 병렬 처리에 유리하다. 순수 함수는 외부 함수에 대한 참조가 없고, 사이드 이펙트를 만들지 않기 때문에 병렬처리가 가능하다.

<br />

## 참고
https://velog.io/@nakta/FP-in-JS-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EB%A1%9C-%EC%A0%91%ED%95%B4%EB%B3%B4%EB%8A%94-%ED%95%A8%EC%88%98%ED%98%95-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%ED%95%A8%EC%88%98%ED%98%95-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%EC%9D%98-%ED%8A%B9%EC%A7%95 <br />
https://sungjk.github.io/2017/07/17/fp.html <br />
https://mangkyu.tistory.com/111 <br />