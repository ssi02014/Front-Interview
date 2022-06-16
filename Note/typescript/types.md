# 💻 타입스크립트 기본 타입(TypeScript)

## 👨🏻‍💻 기본 타입 종류

### Boolean

- 타입이 `진위` 값인 경우에는 아래와 같이 선언합니다.

```ts
const isLoggedIn: boolean = false;
```

<br />

### Number

- 타입이 `숫자`이면 아래와 같이 선언합니다.

```ts
const num: number = 10;
```

<br />

### String

- 자바스크립트 변수의 타입이 `문자열`인 경우 아래와 같이 선언해서 사용합니다.

```ts
const str: string = "hi";
```

<br />

### Array

- 타입이 `배열`인 경우 간단하게 아래와 같이 선언합니다.

```ts
const arr: number[] = [1, 2, 3];
```

- 또는 제네릭을 사용할 수도 있다.

```ts
const arr: Array<number> = [1, 2, 3];
```

<br />

### Tuple

- 튜플은 `배열의 길이가 고정`되고 `각 요소의 타입이 지정`되어 있는 배열 형식을 의미합니다.

```ts
const arr: [string, number] = ["hi", 10];
```

- 만약 정의하지 않은 타입, 인덱스로 접근할 경우 오류가 발생한다.

```ts
arr[1].concat("!"); // Error, number does not have concat
arr[5] = "hello"; // Error, Property 5 does not exist on type [string, number]
```

<br />

### Enum

- Enum은 C, Java와 같은 다른 언어에서 흔하게 쓰이는 타입으로 특정 값(상수)들의 집합을 의미한다.

```ts
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT",
}

const direction: Direction = Direction.Up;
```

<br />

### Any

- 기존에 자바스크립트로 구현되어 있는 웹 서비스 코드에 타입스크립트를 점진적으로 적용할 때 활용하면 좋은 타입입니다. 단어 의미 그대로 `모든 타입에 대해서 허용`한다는 의미를 갖고 있습니다.
- any는 사실 `타입을 검사하지 않는다.` 따라서 타입스크립트에서는 치명적이다 자주 사용하지 않는걸 권장한다.

```ts
const str: any = "hi";
const num: any = 10;
const arr: any = ["a", 2, true];
```

<br />

### Void

- 변수에는 `undefined`와 `null`만 할당하고, 함수에는 `반환 값을 설정할 수 없는 타입`입니다.

```ts
const unUseful: void = undefined;

function notUse(): void {
  console.log("hi");
}
```

<br />

### Never

- 함수의 끝에 절대 도달하지 않는다는 의미를 지닌 타입입니다.

```ts
function neverEnd(): never {
  while (true) {}
}
```

<br />

### 그외

- Null, Undefined

<br />

## 👨🏻‍💻 유틸 타입

### Partial<Type>

- Partial 유틸리티 타입은 `Type` 집합의 모든 프로퍼티를 `선택적(Optional)`으로 타입을 생성한다.

```ts
type Partial<T> = {
  [P in keyof T]?: T[P];
};
```

```ts
interface Todo {
  title: string;
  description: string;
}

function updateTodo(todo: Todo, fieldsToUpdate: Partial<Todo>) {
  return { ...todo, ...fieldsToUpdate };
}

const todo1 = {
  title: "organize desk",
  description: "clear clutter",
};

// optional하게 만들었으니 title이 없어도 된다.
const todo2 = updateTodo(todo1, {
  description: "throw out trash",
});
```

<br />

### Required<Type>

- Required 유틸리티 타입은 `Type` 집합의 모든 프로퍼티를 `필수적(required)`으로 타입을 생성한다.
- Partial과 정반대의 타입이다

```ts
type Required<T> = {
  [P in keyof T]-?: T[P];
};
```

```ts
interface Props {
  a?: number;
  b?: string;
}

const obj: Props = { a: 5 };

const obj2: Required<Props> = { a: 5 };
// Property 'b' is missing in type '{ a: number; }' but required in type 'Required<Props>'.
```

<br />

### Readonly<Type>

- Readonly 유틸리티 타입은 `Type` 집합의 모든 프로퍼티를 `읽기 전용(readonly)`로 설정한 타입을 생성한다.
- 즉 생성된 타입의 프로퍼티는 재 할당될 수 없다.

```ts
type ReadOnly<T> = {
  readonly [P in keyof T]: T[P];
};
```

```ts
interface Todo {
  title: string;
}

const todo: Readonly<Todo> = {
  title: "Delete inactive users",
};

todo.title = "Hello";
// Cannot assign to 'title' because it is a read-only property.
```

<br />

### Record<Keys, Type>

- Record 유틸리티 타입은 `Type`의 프로퍼티 `key의 집합`으로 타입을 생성한다.
- 첫 번째 제네릭 타입 K는 key 값의 타입으로, 두 번째 제네릭 타입 T는 값의 타입으로 갖는 타입을 리턴한다.
- 이 유틸리티 타입은 프로퍼티를 다른 타입에 매핑 시키는데 사용될 수 있다.

```ts
type Record<K, T> = {
  [P in K]: T;
};
```

```ts
interface PageInfo {
  title: string;
}

type Page = "home" | "about" | "contact";

const nav: Record<Page, PageInfo> = {
  about: { title: "about" },
  contact: { title: "contact" },
  home: { title: "home" },
};
```

<br />

### Pick<Type, Keys>

- `Type`에서 프로퍼티 `Keys`의 집합을 `선택`해 타입을 생성합니다.

```ts
type Pick<T, K extends keyof T> = {
  [P in K]: T[P];
};
```

```ts
interface Todo {
  title: string;
  description: string;
  completed: boolean;
}

type TodoPreview = Pick<Todo, "title" | "completed">;

/*
  TodoPreview {
    title: string;
    completed: string;  
  }
*/

const todo: TodoPreview = {
  title: "Clean room",
  completed: false,
};
```

<br />

### Omit<Type, Keys>

- `Type`에서 모든 프로퍼티를 선택하고 `Keys`를 `제거`한 타입을 생성합니다.
- Pick과 반대되는 개념이다.

```ts
type Omit<T, K extends keyof any> = Pick<T, Exclude<keyof T, K>>;
```

```ts
interface Todo {
  title: string;
  description: string;
  completed: boolean;
}

type TodoPreview = Omit<Todo, "description">;

/*
  TodoPreview {
    title: string;
    completed: string;  
  }
*/

const todo: TodoPreview = {
  title: "Clean room",
  completed: false,
};
```

<br />

### Exclude<Type, ExcludedUnion>

- `ExcludedUnion`에 할당할 수 있는 모든 `유니온 멤버`를 `Type`에서 `제외`하여 타입을 생성합니다.

```ts
type Exclude<T, U> = T extends U ? never : T;
```

```ts
type T0 = Exclude<"a" | "b" | "c", "a">;
// type T0 = "b" | "c"

type T1 = Exclude<"a" | "b" | "c", "a" | "b">;
// type T1 = "c"
```

<br />

### Extract<Type, Union>

- `Union`에 할당할 수 있는 `모든 유니온 멤버`를 `Type`에서 가져와서 타입을 생성합니다.

```ts
type Extract<T, U> = T extends U ? T : never;
```

```ts
type T0 = Extract<"a" | "b" | "c", "a" | "f">;
// type T0 = "a"

type T1 = Extract<string | number | (() => void), Function>;
// type T1 = () => void
```

<br />

### Parameters<Type>

- 함수 타입 `Type`의 `매개변수`에 사용된 타입에서 `튜플 타입`을 생성합니다.

```ts
declare function f1(arg: { a: number; b: string }): void;

type T0 = Parameters<() => string>;
// type T0 = []

type T1 = Parameters<(s: string) => void>;
// type T1 = [s: string]

type T2 = Parameters<typeof f1>;
/*
  type T3 = [arg: {
    a: number;
    b: string;
  }]
*/

type T3 = Parameters<any>;
// type T4 = unknown[]

type T4 = Parameters<never>;
// type T5 = never

type T5 = Parameters<string>;
// Type 'string' does not satisfy the constraint '(...args: any) => any'.
```

<br />

### ReturnType<Type>

- 함수 `Type`의 `반환 타입`으로 구성된 타입을 생성합니다.

```ts
declare function f1(): { a: number; b: string };

type T0 = ReturnType<() => string>;
// type T0 = string

type T1 = ReturnType<(s: string) => void>;
// type T1 = void

type T2 = ReturnType<<T>() => T>;
// type T2 = unknown

type T3 = ReturnType<typeof f1>;
/*
  type T3 = {
    a: number;
    b: string;
  }
*/

type T4 = ReturnType<any>;
// type T4 = any

type T5 = ReturnType<never>;
// type T5 = never

type T6 = ReturnType<string>;
// Type 'string' does not satisfy the constraint '(...args: any) => any'.
```

<br />

## 참고

- https://www.typescriptlang.org/ko/docs/handbook/utility-types.html#returntypetype <br />
- https://velog.io/@ggong/Typescript%EC%9D%98-%EC%9C%A0%ED%8B%B8%EB%A6%AC%ED%8B%B0-%ED%83%80%EC%9E%85-2-Partial-Required-ReadOnly-Omit-NonNullable-ReturnType <br />
