# 💻 원시 타입(primitive type) vs 객체 타입(object/reference)

- 자바스크립트에서 제공하는 7가지 데이터 타입(숫자, 문자열, 불리언, null, undefined, Symbol, Object)은 크게 `원시 타입(primitive type)`과 `객체(object/reference type)`으로 구분된다.
- 원시 타입과 객체 타입은 크게 3가지 측면에서 다르다.
  - 원시 타입의 값, 즉 원시 값은 `변경 불가능한 값(immutable value)`다.
  - 객체 타입은 `변경 가능한 값(mutable value)`다.
  - 원시 값을 변수에 할당하면 변수(확보된 메모리 공간)에는 `실제 값이 저장`된다.
  - 객체는 변수에 할당하면 변수(확보된 메모리 공간)에 `참조 값이 저장`된다.
  - 원시 값을 갖는 변수를 다른 변수에 할당하면 원본의 원시 값이 복사되어 전달된다. 이를 `값에 의한 전달(pass by value)`라고 한다.
  - 객체는 가리키는 변수를 다른 변수에 할당하면 원본의 참조 값이 복사되어 전달된다. 이를 `참조에 의한 전달(pass by reference)`라고 한다.

<br />

## 원시 값

### 변경 불가능한 값(immutable value)

- 변경 불가능 한 값은 다시 말해, 한번 생성된 원시 값은 `읽기 전용(read only)`값으로서 변경할 수 없음을 의미한다.
  - 이러한 불변성은 원시 값 데이터의 `신뢰성을 보장`한다.
- 참고로! 변경 불가능하다는 것은 변수가 아니라 `값에 대한 이야기이다.` 즉, 원시값 자체를 변경 할 수 없다는 거지 변수 값을 변경할 수 없다는 것은 아니다. 변수는 언제든지 재할당해서 값을 변경 할 수 있다. 아래 예제를 참고하자.

```js
let str = "123";

// 원시값인 문자열을 인덱스로 접근해서 변경함, 에러는 발생하지 않지만 값이 변경되지는 않음
str[0] = "4";

console.log(str); // "123"

str = "456"; // 변수를 재할당해서 값을 바꿈

console.log(str); // "456"
```

<br />

<img width="794" alt="스크린샷 2023-04-17 오전 12 08 25" src="https://user-images.githubusercontent.com/64779472/232322135-9d2accab-2492-411c-a24b-f4c751df5170.png">

- 위 이미지처럼 자바스크립트에서 원시 값을 할당한 변수에 새로운 원시 값을 재할당하면, 메모리 공간에 저장되어 있는 재할당 이전의 원시 값을 변경하는 것이 아닌! `새로운 메모리 공간을 확보하고 재할당한 원시 값을 저장 한 후, 변수는 재할당한 원시값을 가리킨다.`
- 이러한 동작 원리의 이유가 바로 변수에 할당된 `원시 값이 변경 불가능한 값이기 때문이다.`
  - 만약, 원시 값이 변경 가능한 값이라면 변수가 가리키던 메모리 공간의 주소를 바꿀 필요없이 원시 값 자체를 변경하면 그만이다. 당연히 메모리 공간의 주소도 바뀌지 않는다.
  - 하지만, 원시 값은 변경 불가능 한 값이며, 값을 직접 바꿀 수 없다. 따라서 변수 값을 변경하기 위해 재할당 하면 새로운 메모리 공간을 확보하고 재할당한 값을 저장 한 후, 변수가 참조하던 메모리 공간의 주소를 변경한다. 이러한 특징이 바로 `불변성(immutability)`이라 한다.

<br />

### 값에 의한 전달

- 원시 값을 갖는 변수를 다른 변수에 할당하면 원본의 원시 값이 복사되어 전달된다. 이를 `값에 의한 전달(pass by value)`라고 한다.

```js
let score = 80;
let copy = score;

console.log(score); // 80
console.log(copy); // 80

console.log(score === copy); // true
```

- 위 예제처럼 copy 변수에다 score(80로 평가)을 할당하면 copy 변수에도 80이 할당된다. 이때 새로운 숫자 값 80이 생성되어 할당된다.

<img width="512" alt="스크린샷 2023-04-17 오전 12 20 13" src="https://user-images.githubusercontent.com/64779472/232322801-c5965985-8e16-4ce7-bb45-bc52c6395aca.png">

- score와 copy는 같은 숫자 80을 갖는다는 점에서 동일하다. 하지만 위 이미지처럼 score와 copy의 값 80은 각각 다른 메모리 공간에 저장된다.

```js
let score = 80;
let copy = score;

console.log(score === copy); // true

score = 100;
console.log(score); // 100
console.log(copy); // 80

console.log(score === copy); // false
```

- score와 copy 변수의 값 80은 각각 다른 메모리 공간에 저장된 별개의 값을 주의해야한다.
  - 따라서 score 값을 100으로 변경한다면? copy에 어떠한 영향을 주지 않으며, 서로 같은지 비교를 해도 false로 평가된다.

<br />

<img width="766" alt="스크린샷 2023-04-17 오전 1 10 42" src="https://user-images.githubusercontent.com/64779472/232325772-da3fce5d-6e1b-426f-bad4-6d89dea922c1.png">

- 사실 ECMAScript 사양에는 변수를 통해 메모리를 어떻게 관리하는지 정확히 정의되어 있지 않는다.
  - 따라서 실제 자바스크립트 엔진을 구현하는 `제조사에 따라 실제 내부 동작은 미묘한 차이`가 있을 수 있다.
- 기존 그림에서는 변수에 원시 값을 갖는 변수를 할당하면 원시 값이 복사되는 것으로 표현했는데, 바로 위의 그림처럼 변수에 원시 값을 갖는 변수를 할당하는 시점에는 `두 변수가 같은 원시 값을 참조`하다가 어느 한쪽의 변수에 재할당이 이뤄졌을 때 비로소 `새로운 메모리 공간에 재할당된 값을 저장하도록 동작`할 수도 있다.
  - 참고로 실제로 `파이썬`은 이처럼 동작한다.

<br />

- 또 다른 사실2 `값에 의한 전달`이라는 용어도 사실 ECMAScript 사양에 등장하지 않는다. 값에 의한 전달이라는 용어가 오해를 불러일으킬 수 있다.
- 엄격하게 표현하자면 변수에는 값이 전달되는 것이 아니라 `메모리 주소가 전달`되기 때문이다. 이는 변수와 같은 식별자는 `값이 아니라 메모리 주소를 기억`하고 있기 때문이다!
- 식별자는 `어떤 값을 구별해 낼 수 있는 고유한 이름`이다. 값은 `메모리 공간에 저장`되어 있다. 따라서 식별자는 `메모리 공간에 저장되어 있는 어떤 값을 식별해내는 변수다.`
  - 따라서! 식별자는 값이 아닌 메모리 주소를 기억하고 있어야 한다.

<br />

## 객체

### 변경 가능한 값(mutable value)

- 객체(참조) 타입의 값, 즉 `객체는 변경 가능한 값`이다.
- 원시 값을 할당한 `변수가 기억하는 메모리 주소`를 통해 메모리 공간에 접근하면 `원시 값에 접근`할 수 있다.
- 그에 반해, 객체는 할당한 변수가 기억하는 메모리 주소를 통해 메모리 공간에 접근하면 `참조 값(reference value)에 접근`할 수 있다.
  - 참조 값은 `생성된 객체가 저장된 메모리 공간의 주소, 그 자체다.`

<br />

<img width="790" alt="스크린샷 2023-04-17 오전 1 23 34" src="https://user-images.githubusercontent.com/64779472/232326439-fd9fd8c4-e070-42f8-8683-2e3632990529.png">

- 위 그림 처럼 객체를 할당한 변수를 참조하면 메모리 저장되어 있는 `참조 값(생성된 객체가 저장된 메모리 공간의 주소)`을 통해 실제 객체에 접근한다.

<br />

```js
const person = {
  name: "Lee",
};

person.name = "Kim";
person.address = "Seoul";

console.log(person); // { name: "Kim", address: "Seoul" }
```

- 원시 값은 변경 불가능한 값이므로 원시 값을 갖는 변수의 값을 변경하려면 `재할당 외에는 없다.` 심지어 const로 선언했으면 그마저도 안된다.
- 객체는 계속 언급했지만 변경 가능한 값이다. 재할당 없이도 객체의 내용을 직접 바꿀 수 있다. 즉, 프로퍼티 값을 동적으로 추가, 삭제, 갱신이 가능하다.

<br />

<img width="723" alt="스크린샷 2023-04-17 오전 1 28 42" src="https://user-images.githubusercontent.com/64779472/232326691-e21e3854-cc1d-4f69-a4e9-6020fc74bc58.png">

- 위 그림처럼 객체는 메모리에 저장된 객체를 직접 수정 할 수 있다. 이때 객체를 할당한 변수에 재할당을 하지 않았으므로 객체를 할당한 변수의 참조 값은 변경되지 않는다.

<br />

- 객체를 생성하고 관리하는 방식은 매우 복잡하며 비용이 많이 든다.
  - 객체를 변경할 때마다 원시 값처럼 이전 값을 복사해서 새롭게 생성한다면 명확하고 신뢰성은 보장되겠지만, `객체의 크기가 매우 크다면?!` 복사해서 생성하는 비용이 굉장히 많이 든다.
  - 객체는 원시값처럼 크기가 고정적이지도 않고, 프로퍼티의 값이 또 객체일 수도 있다!
  - 결과적으로 메모리의 효율성이 낮고, 성능이 나빠질 수 있다.
- 위와 같은 이유로 객체를 복사해서 생성하는 비용을 절약하여 성능을 향상시키기 위해 객체는 변경 가능한 값으로 설계된 것이다!
- 물론 이러한 구조는 단점도 있다. 원시 값과는 다르게 `여러 개의 식별자가 하나의 객체를 공유할 수도 있다는 것이다!`

<br />

### 참조에 의한 전달

```js
const person = {
  name: "Lee",
};
const copy = person; // 참조 값을 복사

console.log(person === copy); // true

copy.name = "Kim";

console.log(person); // { name: "Kim" }
```

- 객체를 가리키는 원본 변수를 다른 변수에 할당하면 원본의 참조 값이 복사되어 전달된다 이를 `참조에 의한 전달`이라고 한다.

<br />

<img width="739" alt="스크린샷 2023-04-17 오전 1 36 02" src="https://user-images.githubusercontent.com/64779472/232327076-b2a57054-dc4f-4d0a-9371-ac58401c8c0f.png">

- 위 그림처럼 원본 person을 copy에 할당하면 원본 person의 참조 값을 복사해서 copy에 저장한다.
- 이때 person과 copy는 저장된 메모리 주소는 다르지만 동일한 참조 값을 갖는다. 다시 말해 둘 다 같은 객체를 가리킨다.
- 이러한 동작은 위에 코드 예시처럼 원본 또는 사본 중 어느 한쪽의 객체를 변경하면 서로 영향을 주고 받는 결과를 초래한다.

<br />

## 참고

- 모던 자바스크립트 Deep Dive
