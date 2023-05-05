# 💻 함수: 값에 의한 호출(call by value)과 참조에 의한 호출(call by reference)

- 자바스크립트에서 함수 호출 시 전달되는 인수(argument)는 `원시 타입(primitive type)`과 `객체 타입(object type)`으로 구분된다. 이에 따라, 인수 전달 방식도 두 가지로 구분할 수 있다.
  - Call by Value: 원시 타입 인수의 경우, 값이 복사되어 전달된다.
  - Call by Reference: 객체 타입 인수의 경우, 참조 값(reference)가 복사되어 전달된다.

<br />

## call by value

- Call by Value 방식으로 함수 호출을 할 경우, 함수 내부에서 전달된 인수를 변경해도 원래 변수의 값이 변경되지 않는다.

```js
let num = 1;

const increment = (x) => {
  x++;
};

increment(num);
console.log(num); // 1
```

- 위 코드에서 `increment()` 함수는 전달된 x 변수의 값을 1 증가시키는 함수다. 그러나 함수 호출 결과로 num 변수의 값은 훼손되지 않는다.
- 이는 원시 값은 `변경 불가능 한 값(immutable value)`이기 때문에 인자로 넘긴 `원시 값이 복사되어 매개 변수(num)으로 전달`되기 때문이다.

<br />

## call by Reference

- Call by Reference 방식으로 함수 호출을 할 경우, 함수 내부에서 전달된 객체를 변경하면 원래 객체가 변경된다.

```js
const person = { name: "Bob" };

const setName = (person) => {
  person.name = "Alice";
};

setName(person);
console.log(person.name); // 'Alice'
```

- 위 코드에서 setName() 함수는 전달된 person 객체의 name 속성 값을 `Alice`로 변경하는 함수다. call by value 때와 다르게 함수 호출 결과로 person 변수의 name 속성 값도 Alice로 변경된다.
- 왜냐하면 객체는 `변경 가능한 값(mutabled value)`이기 때문에 person 변수가 setName() 함수 내부에서 `참조 값(reference)이 복사되어 전달`되기 때문이다.

<br />

- 이러한 현상을 방지하기 위해서는 `Object.assign, ...연산자` 등으로 객체를 깊은 복사 후에 사용하면 된다.
  - TMI: Object.assign, ...(Spread Operator) 는 객체의 `depth 1`까지만 깊은 복사된다. 따라서 불완전하다.
  - 물론 완전한 깊은 복사를 하는 방법도 있는데 이는 `JSON`, `재귀함수`, `lodash 모듈의 cloneDeep`을 이용하는 것이다.

```js
const person = { name: "Bob" };

// depth1 예제
const setName = (person) => {
  const copiedPerson = { ...person };

  copiedPerson.name = "Alice";
};

setName(person);
console.log(person.name); // 'Bob'
```

<br />

```js
// depth2 예제

const person = { info: { name: "Bob" } };

// depth1
const setName = (person) => {
  const copiedPerson = { ...person };

  copiedPerson.info.name = "Alice";
};

setName(person);
console.log(person.info.name); // 'Alice'
```

<br />
