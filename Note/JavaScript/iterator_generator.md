# 💻 iterable/iterator, generator

<br />

## 👨🏻‍💻 이터러블(iterable) / 이터레이터(iterator)

- 이터러블은 `이터레이터를 반환`하는 `[Symbol.iterator]()`메서드를 가진 객체이다.
  - 이터러블엔 `[Symbol.iteraotor]()`가 반드시 구현되어 있어야 한다.
  - `obj[Symbol.iterator]()` 메서드 호출 결과를 `이터레이터`라고 한다.

```js
// 이터러블 예제
const iterable = {
  [Symbol.iterator]() {
    let i = 3;
    return {
      next() {
        return i === 0
          ? { value: undefined, done: true }
          : { value: i--, done: false };
      },
      [Symbol.iterator]() {
        return this;
      },
    };
  },
};
```

- 이터레이터는 `{ value, done }` 객체를 반환하는 `next()` 메서드를 가진 객체이다.
  - 이터레이터엔 `next()`가 반드시 구현되어 있어야 한다. 또한 `done`의 값은 false와 true를 갖는데 true면 반복이 끝났음을 의미한다.

```js
const iterable = {
  //...
};
const iterator = iterable[Symbol.iterator]();
console.log(iterator.next()); // { value: 0, done: false }

/*
	이터레이터가 자기 자신을 반환하는 [Symbol.iterator]()를 갖고 있으면 
	well-formed 이터러블/이터레이터라고 한다.
*/
console.log(iterator[Symbol.iterator]() === iterator); // true
```

<br />

### 이터러블/이터레이터 프로토콜

```js
const iterable = {
  //...
};
const iterator = iterable[Symbol.iterator]();

console.log(iterator.next()); // { value: 0, done: false }

// for...of문
for (const el of iterator) {
  console.log(el); // 1 2
}

// Spread 연산자
const newIterator = [...iterable]; // [0, 1, 2]
console.log(newIterator);
```

- 이터러블/이터레이터 프로토콜이란, 이터러블을 `for...of`, `전개 연산자` 등과 함께 동작하도록 한 규약
- 자바스크립트에서 이터러블/이터레이터 프로토콜을 준수한 객체는 `for...of`문으로 순회할 수 있고, `Spread 문법`의 피연산자가 될 수 있다. 즉, for...of문으로 순회할 수 있고, spread연산자의 피연산자로 쓸 수 있는 객체를 `이터러블`이라고 한다.

<br />

### Built-In Iterable 종류

- `Array`, `String`, `Map`, `Set`, `TypedArray`, `arguments`, `DOM Data Structure(NodeList, HTMLCollection)`

<br />

## 👨🏻‍💻 제너레이터(generator)

```js
function* gen() {
  yield 1;
  yield 2;
  yield 3;
  return 10; // return 값을 넣으면 done이 true일 때 value값을 줄 수 있다.
}

const iter = gen();

/* 
	iter는 이터레이터이자 이터러블이다. 
	따라서 [Symbol.iterator]를 실행하면 자기 자신을 반환한다.
*/
console.log(iter[Symbol.iterator]() === iter); // true
console.log(iter); // 제너레이터 객체 반환: Object [Generator] {}

console.log(iter.next()); // { value: 1, done: false }
console.log(iter.next()); // { value: 2, done: false }
console.log(iter.next()); // { value: 3, done: false }
console.log(iter.next()); // { value: 10, done: true }

// for ... of문 주의: for...of으로 순회할 때는 return의 value는 순회하지 않음
for (const a of gen()) {
  console.log(a); // 1 2 3
}

// Spread 연산자
const newGen = [...gen()];
console.log(newGen); // [ 1, 2, 3 ]
```

- 제너레이터는 ES6에서 도입된 `이터레이터이자 이터러블을 생성하는 함수`
- 제너레이터를 만들려면 제너레이터 함수라 불리는 특별한 문법 구조 `function*` 이 필요하다.
- 제너레이터 함수는 일반 함수와 동작 방식이 다르다. 제너레이터 함수를 호출하면 코드가 실행되지 않고, 대신 실행을 처리하는 특별한 객체, `제너레이터 객체`가 반환된다.
- `next()`는 제너레이터 주요 메서드이다. `next()`를 호출하면 가장 가까운 `yield <value>`문을 만날 때 까지 실행이 지속된다. (value를 생략할 수 있는데, 이 경우에는 undefined가 된다.) 이후, `yield <value>`문을 만나면 실행이 멈추고 산출하고자 하는 값인 value가 반환된다.
- 제너레이터는 `이터러블`이다. 따라서 `for ... of 반복문`을 통해 값을 얻을 수 있고 `spread 연산자`의 피연사자로 사용할 수 있다.

<br />

## 참고

https://www.notion.so/2c4d4292c8574027b50150c5ef6e02b5

<br />
