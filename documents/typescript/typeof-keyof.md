# 💻 타입스크립트 typeof/keyof

## typeof 연산자

- 타입스크립트에서 typeof 연산자는 객체 데이터를 객체 타입으로 변환해주는 역할을한다.

```ts
const fruit = {
  apple: "사과",
  banana: "바나나",
  melon: "멜론",
} as const; // (*) as const를 붙여줘야 함

type Fruit = typeof fruit;

/*
  type Fruit = {
    apple: string;
    banana: string;
    melon: string;
  }
/*
```

- 위 예제에서 fruit 객체는 타입으로서는 사용할 수 없다.
- 그래서 정의한 객체의 쓰인 타입 구조를 그대로 가져와서 독립된 타입으로 만들어서 사용하고 싶다면 이 typeof 키워드를 사용하면 된다.
- typof연산자는 객체뿐만아니라 함수에서도 활용할 수 있다.

```ts
const divide = (x: number, y: number) => x / y;

type Divide = typeof divide;
// type Divide = (x: number, y: number) => number
```

- 이때 class와 같은 경우에는 클래스 자체가 객체 타입이 될 수 있으므로 typeof를 안붙여도 된다.

<br />

- 혼란스러울 수 있는게 사실 typeof연산자는 기존의 자바스크립트에서 피연산자의 데이터 타입을 반환해주는 역할로 쓰였다.

```js
typeof 12; // 'number'
```

- 값의 관점에서 typeof연산자는 자바스크립트의 런타임 typeof 연산자이며, 타입스크립트에서 타입 관점으로 사용하는 typeof 연산자는 해당 객체를 읽어서 타입을 반환하는 연산자임을 기억하자.

<br />

## keyof 연산자

- 타입스크립트에서 keyof 연산자는 객체 형태의 타입에서 가지고 있는 모든 key값들을 유니온 타입으로 만들어주는 연산자이다.

```ts
interface Fruit {
  apple: string;
  banana: string;
  melon: string;
}

type FruitUnionKey = keyof typeof fruit;
// type FruitUnionKey = apple | banana | melon

const apple: FruitUnionKey = "apple";
const banana: FruitUnionKey = "banana";
const melon: FruitUnionKey = "melon";
```

<br />

## typeof와 keyof의 활용

- keyof와 typeof를 함께 활용할 수 있는데 예를 들어 아래와 같은 fruit 객체에서의 apple, banana, melon key들만 가져와서 상수타입으로 활용하려면 다음과 같이 활용할 수 있다.

```ts
const fruit = {
  apple: "사과",
  banana: "바나나",
  melon: "멜론",
};

type FruitUnionKey = keyof typeof fruit;
// type FruitUnionKey = "apple" | "banana" | "melon"
```

- 이와 반대로 value값인 사과, 바나나, 멜론들을 가져와서 상수타입으로 활용하려면 다음과 같이 활용할 수 있다.

```ts
const fruit = {
  apple: "사과",
  banana: "바나나",
  melon: "멜론",
} as const; // (*) as const를 붙여줘야 함

type FruitUnionValues = (typeof fruit)[keyof typeof fruit];
// type FruitUnionValues = "사과" | "바나나" | "멜론"
```

<br />
