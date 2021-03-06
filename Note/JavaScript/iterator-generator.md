# π» iterable/iterator, generator

<br />

## π¨π»βπ» μ΄ν°λ¬λΈ(iterable) / μ΄ν°λ μ΄ν°(iterator)

- μ΄ν°λ¬λΈμ `μ΄ν°λ μ΄ν°λ₯Ό λ°ν`νλ `[Symbol.iterator]()`λ©μλλ₯Ό κ°μ§ κ°μ²΄μ΄λ€.
  - μ΄ν°λ¬λΈμ `[Symbol.iteraotor]()`κ° λ°λμ κ΅¬νλμ΄ μμ΄μΌ νλ€.
  - `obj[Symbol.iterator]()` λ©μλ νΈμΆ κ²°κ³Όλ₯Ό `μ΄ν°λ μ΄ν°`λΌκ³  νλ€.

```js
// μ΄ν°λ¬λΈ μμ 
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

- μ΄ν°λ μ΄ν°λ `{ value, done }` κ°μ²΄λ₯Ό λ°ννλ `next()` λ©μλλ₯Ό κ°μ§ κ°μ²΄μ΄λ€.
  - μ΄ν°λ μ΄ν°μ `next()`κ° λ°λμ κ΅¬νλμ΄ μμ΄μΌ νλ€. λν `done`μ κ°μ falseμ trueλ₯Ό κ°λλ° trueλ©΄ λ°λ³΅μ΄ λλ¬μμ μλ―Ένλ€.

```js
const iterable = {
  //...
};
const iterator = iterable[Symbol.iterator]();
console.log(iterator.next()); // { value: 0, done: false }

/*
	μ΄ν°λ μ΄ν°κ° μκΈ° μμ μ λ°ννλ [Symbol.iterator]()λ₯Ό κ°κ³  μμΌλ©΄ 
	well-formed μ΄ν°λ¬λΈ/μ΄ν°λ μ΄ν°λΌκ³  νλ€.
*/
console.log(iterator[Symbol.iterator]() === iterator); // true
```

<br />

### μ΄ν°λ¬λΈ/μ΄ν°λ μ΄ν° νλ‘ν μ½

```js
const iterable = {
  //...
};
const iterator = iterable[Symbol.iterator]();

console.log(iterator.next()); // { value: 0, done: false }

// for...ofλ¬Έ
for (const el of iterator) {
  console.log(el); // 1 2
}

// Spread μ°μ°μ
const newIterator = [...iterable]; // [0, 1, 2]
console.log(newIterator);
```

- μ΄ν°λ¬λΈ/μ΄ν°λ μ΄ν° νλ‘ν μ½μ΄λ, μ΄ν°λ¬λΈμ `for...of`, `μ κ° μ°μ°μ` λ±κ³Ό ν¨κ» λμνλλ‘ ν κ·μ½
- μλ°μ€ν¬λ¦½νΈμμ μ΄ν°λ¬λΈ/μ΄ν°λ μ΄ν° νλ‘ν μ½μ μ€μν κ°μ²΄λ `for...of`λ¬ΈμΌλ‘ μνν  μ μκ³ , `Spread λ¬Έλ²`μ νΌμ°μ°μκ° λ  μ μλ€. μ¦, for...ofλ¬ΈμΌλ‘ μνν  μ μκ³ , spreadμ°μ°μμ νΌμ°μ°μλ‘ μΈ μ μλ κ°μ²΄λ₯Ό `μ΄ν°λ¬λΈ`μ΄λΌκ³  νλ€.

<br />

### Built-In Iterable μ’λ₯

- `Array`, `String`, `Map`, `Set`, `TypedArray`, `arguments`, `DOM Data Structure(NodeList, HTMLCollection)`

<br />

## π¨π»βπ» μ λλ μ΄ν°(generator)

```js
function* gen() {
  yield 1;
  yield 2;
  yield 3;
  return 10; // return κ°μ λ£μΌλ©΄ doneμ΄ trueμΌ λ valueκ°μ μ€ μ μλ€.
}

const iter = gen();

/* 
	iterλ μ΄ν°λ μ΄ν°μ΄μ μ΄ν°λ¬λΈμ΄λ€. 
	λ°λΌμ [Symbol.iterator]λ₯Ό μ€ννλ©΄ μκΈ° μμ μ λ°ννλ€.
*/
console.log(iter[Symbol.iterator]() === iter); // true
console.log(iter); // μ λλ μ΄ν° κ°μ²΄ λ°ν: Object [Generator] {}

console.log(iter.next()); // { value: 1, done: false }
console.log(iter.next()); // { value: 2, done: false }
console.log(iter.next()); // { value: 3, done: false }
console.log(iter.next()); // { value: 10, done: true }

// for ... ofλ¬Έ μ£Όμ: for...ofμΌλ‘ μνν  λλ returnμ valueλ μννμ§ μμ
for (const a of gen()) {
  console.log(a); // 1 2 3
}

// Spread μ°μ°μ
const newGen = [...gen()];
console.log(newGen); // [ 1, 2, 3 ]
```

- μ λλ μ΄ν°λ ES6μμ λμλ `μ΄ν°λ μ΄ν°μ΄μ μ΄ν°λ¬λΈμ μμ±νλ ν¨μ`
- μ λλ μ΄ν°λ₯Ό λ§λ€λ €λ©΄ μ λλ μ΄ν° ν¨μλΌ λΆλ¦¬λ νΉλ³ν λ¬Έλ² κ΅¬μ‘° `function*` μ΄ νμνλ€.
- μ λλ μ΄ν° ν¨μλ μΌλ° ν¨μμ λμ λ°©μμ΄ λ€λ₯΄λ€. μ λλ μ΄ν° ν¨μλ₯Ό νΈμΆνλ©΄ μ½λκ° μ€νλμ§ μκ³ , λμ  μ€νμ μ²λ¦¬νλ νΉλ³ν κ°μ²΄, `μ λλ μ΄ν° κ°μ²΄`κ° λ°νλλ€.
- `next()`λ μ λλ μ΄ν° μ£Όμ λ©μλμ΄λ€. `next()`λ₯Ό νΈμΆνλ©΄ κ°μ₯ κ°κΉμ΄ `yield <value>`λ¬Έμ λ§λ  λ κΉμ§ μ€νμ΄ μ§μλλ€. (valueλ₯Ό μλ΅ν  μ μλλ°, μ΄ κ²½μ°μλ undefinedκ° λλ€.) μ΄ν, `yield <value>`λ¬Έμ λ§λλ©΄ μ€νμ΄ λ©μΆκ³  μ°μΆνκ³ μ νλ κ°μΈ valueκ° λ°νλλ€.
- μ λλ μ΄ν°λ `μ΄ν°λ¬λΈ`μ΄λ€. λ°λΌμ `for ... of λ°λ³΅λ¬Έ`μ ν΅ν΄ κ°μ μ»μ μ μκ³  `spread μ°μ°μ`μ νΌμ°μ¬μλ‘ μ¬μ©ν  μ μλ€.

<br />

## μ°Έκ³ 

https://www.notion.so/2c4d4292c8574027b50150c5ef6e02b5

<br />
