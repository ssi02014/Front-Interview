# π» νμμ€ν¬λ¦½νΈ κΈ°λ³Έ νμ(TypeScript)

## π¨π»βπ» κΈ°λ³Έ νμ μ’λ₯

### Boolean

- νμμ΄ `μ§μ` κ°μΈ κ²½μ°μλ μλμ κ°μ΄ μ μΈν©λλ€.

```ts
const isLoggedIn: boolean = false;
```

<br />

### Number

- νμμ΄ `μ«μ`μ΄λ©΄ μλμ κ°μ΄ μ μΈν©λλ€.

```ts
const num: number = 10;
```

<br />

### String

- μλ°μ€ν¬λ¦½νΈ λ³μμ νμμ΄ `λ¬Έμμ΄`μΈ κ²½μ° μλμ κ°μ΄ μ μΈν΄μ μ¬μ©ν©λλ€.

```ts
const str: string = "hi";
```

<br />

### Array

- νμμ΄ `λ°°μ΄`μΈ κ²½μ° κ°λ¨νκ² μλμ κ°μ΄ μ μΈν©λλ€.

```ts
const arr: number[] = [1, 2, 3];
```

- λλ μ λ€λ¦­μ μ¬μ©ν  μλ μλ€.

```ts
const arr: Array<number> = [1, 2, 3];
```

<br />

### Tuple

- ννμ `λ°°μ΄μ κΈΈμ΄κ° κ³ μ `λκ³  `κ° μμμ νμμ΄ μ§μ `λμ΄ μλ λ°°μ΄ νμμ μλ―Έν©λλ€.

```ts
const arr: [string, number] = ["hi", 10];
```

- λ§μ½ μ μνμ§ μμ νμ, μΈλ±μ€λ‘ μ κ·Όν  κ²½μ° μ€λ₯κ° λ°μνλ€.

```ts
arr[1].concat("!"); // Error, number does not have concat
arr[5] = "hello"; // Error, Property 5 does not exist on type [string, number]
```

<br />

### Enum

- Enumμ C, Javaμ κ°μ λ€λ₯Έ μΈμ΄μμ ννκ² μ°μ΄λ νμμΌλ‘ νΉμ  κ°(μμ)λ€μ μ§ν©μ μλ―Ένλ€.

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

- κΈ°μ‘΄μ μλ°μ€ν¬λ¦½νΈλ‘ κ΅¬νλμ΄ μλ μΉ μλΉμ€ μ½λμ νμμ€ν¬λ¦½νΈλ₯Ό μ μ§μ μΌλ‘ μ μ©ν  λ νμ©νλ©΄ μ’μ νμμλλ€. λ¨μ΄ μλ―Έ κ·Έλλ‘ `λͺ¨λ  νμμ λν΄μ νμ©`νλ€λ μλ―Έλ₯Ό κ°κ³  μμ΅λλ€.
- anyλ μ¬μ€ `νμμ κ²μ¬νμ§ μλλ€.` λ°λΌμ νμμ€ν¬λ¦½νΈμμλ μΉλͺμ μ΄λ€ μμ£Ό μ¬μ©νμ§ μλκ±Έ κΆμ₯νλ€.

```ts
const str: any = "hi";
const num: any = 10;
const arr: any = ["a", 2, true];
```

<br />

### Void

- λ³μμλΒ `undefined`μΒ `null`λ§ ν λΉνκ³ , ν¨μμλ `λ°ν κ°μ μ€μ ν  μ μλ νμ`μλλ€.

```ts
const unUseful: void = undefined;

function notUse(): void {
  console.log("hi");
}
```

<br />

### Never

- ν¨μμ λμ μ λ λλ¬νμ§ μλλ€λ μλ―Έλ₯Ό μ§λ νμμλλ€.

```ts
function neverEnd(): never {
  while (true) {}
}
```

<br />

### κ·ΈμΈ

- Null, Undefined

<br />

## π¨π»βπ» μ νΈ νμ

### Partial<Type>

- Partial μ νΈλ¦¬ν° νμμ `Type` μ§ν©μ λͺ¨λ  νλ‘νΌν°λ₯Ό `μ νμ (Optional)`μΌλ‘ νμμ μμ±νλ€.

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

// optionalνκ² λ§λ€μμΌλ titleμ΄ μμ΄λ λλ€.
const todo2 = updateTodo(todo1, {
  description: "throw out trash",
});
```

<br />

### Required<Type>

- Required μ νΈλ¦¬ν° νμμ `Type` μ§ν©μ λͺ¨λ  νλ‘νΌν°λ₯Ό `νμμ (required)`μΌλ‘ νμμ μμ±νλ€.
- Partialκ³Ό μ λ°λμ νμμ΄λ€

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

- Readonly μ νΈλ¦¬ν° νμμ `Type` μ§ν©μ λͺ¨λ  νλ‘νΌν°λ₯Ό `μ½κΈ° μ μ©(readonly)`λ‘ μ€μ ν νμμ μμ±νλ€.
- μ¦ μμ±λ νμμ νλ‘νΌν°λ μ¬ ν λΉλ  μ μλ€.

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

- Record μ νΈλ¦¬ν° νμμ `Type`μ νλ‘νΌν° `keyμ μ§ν©`μΌλ‘ νμμ μμ±νλ€.
- μ²« λ²μ§Έ μ λ€λ¦­ νμ Kλ key κ°μ νμμΌλ‘, λ λ²μ§Έ μ λ€λ¦­ νμ Tλ κ°μ νμμΌλ‘ κ°λ νμμ λ¦¬ν΄νλ€.
- μ΄ μ νΈλ¦¬ν° νμμ νλ‘νΌν°λ₯Ό λ€λ₯Έ νμμ λ§€ν μν€λλ° μ¬μ©λ  μ μλ€.

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

- `Type`μμ νλ‘νΌν° `Keys`μ μ§ν©μ `μ ν`ν΄ νμμ μμ±ν©λλ€.

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

- `Type`μμ λͺ¨λ  νλ‘νΌν°λ₯Ό μ ννκ³  `Keys`λ₯Ό `μ κ±°`ν νμμ μμ±ν©λλ€.
- Pickκ³Ό λ°λλλ κ°λμ΄λ€.

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

- `ExcludedUnion`μ ν λΉν  μ μλ λͺ¨λ  `μ λμ¨ λ©€λ²`λ₯Ό `Type`μμ `μ μΈ`νμ¬ νμμ μμ±ν©λλ€.

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

- `Union`μ ν λΉν  μ μλ `λͺ¨λ  μ λμ¨ λ©€λ²`λ₯Ό `Type`μμ κ°μ Έμμ νμμ μμ±ν©λλ€.

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

- ν¨μ νμ `Type`μ `λ§€κ°λ³μ`μ μ¬μ©λ νμμμ `νν νμ`μ μμ±ν©λλ€.

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

- ν¨μ `Type`μ `λ°ν νμ`μΌλ‘ κ΅¬μ±λ νμμ μμ±ν©λλ€.

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

## μ°Έκ³ 

- https://www.typescriptlang.org/ko/docs/handbook/utility-types.html#returntypetype <br />
- https://velog.io/@ggong/Typescript%EC%9D%98-%EC%9C%A0%ED%8B%B8%EB%A6%AC%ED%8B%B0-%ED%83%80%EC%9E%85-2-Partial-Required-ReadOnly-Omit-NonNullable-ReturnType <br />
