# 💻 콜백 함수와 고차 함수

## 콜백 함수(Callback Function)

- 자바스크립트에서는 일급 객체인 함수를 다른 함수의 매개변수로 넣을 수 있다.
- 이와 같이 `다른 함수의 매개변수로 들어가는 함수`를 `콜백 함수`라고 한다.

<br />

## 고차 함수(Higher-Order Function, HOG)

- 고차함수는 `매개 변수를 통해 함수의 외부에서 콜백 함수를 전달 받은 함수`를 `고차 함수`라고 한다.
- 고차 함수는 매개변수를 통해 전달받은 콜백 함수의 호출 시점을 결정해서 호출한다.
- 즉! 콜백 함수는 고차 함수에 의해 호출되고, 이때 고차 함수는 필요에 따라 콜백 함수에 인수를 전달 할 수도 있다.

<br />

## 콜백, 고차 함수 기본 예제

```js
const testFunc = (n) => {
  for (let i = 0; i < n; i++) {
    console.log(i);
  }
};

// 고차함수 higherOrderFunc
const higherOrderFunc = (n, func) => {
  if (func) {
    func(n); // 인자로 받아온 콜백 함수를 호출
  }
};

// testFunc higherOrderFunc의 인자로 넘겨주고 있음 즉, 여기서 testFunc이 콜백함수
higherOrderFunc(5, testFunc);
```

<br />

## 대표적인 고차함수

- 우리가 흔히 사용하는 배열 메서드들이 고차 함수의 대표적인 예라고 할 수 있다.
- 아래 예제를 확인해보면 배열 메서드들(map, filter, ...)의 인자로 `화살표 함수(콜백 함수)`를 인자로 넣어주고 있다.

```js
const arr = [1, 2, 3, 4, 5];

// map
const testArr1 = arr.map((el) => el * 2);

// filter
const testArr2 = arr.filter((el) => el % 2 === 0);

// reduce
const sum = arr.reduce((acc, cur) => acc + cur, 0);
```

<br />
