# ๐ป JSX(JavaScript XML)

## ๐จ๐ปโ๐ป JSX

- JSX(JavaScriptย XML)๋ย `Javascript์ XML์ ์ถ๊ฐํ ํ์ฅํ ๋ฌธ๋ฒ์ด๋ค.`
- JSX๋ ๋ฆฌ์กํธ๋ก ํ๋ก์ ํธ๋ฅผ ๊ฐ๋ฐํ  ๋ ์ฌ์ฉ๋๋ฏ๋ก ๊ณต์์ ์ธ ์๋ฐ์คํฌ๋ฆฝํธ ๋ฌธ๋ฒ์ ์๋๋ค.
- ๋ธ๋ผ์ฐ์ ์์ ์คํํ๊ธฐ ์ ์ `๋ฐ๋ฒจ`์ ์ฌ์ฉํ์ฌ ์ผ๋ฐ ์๋ฐ์คํฌ๋ฆฝํธ ํํ์ ์ฝ๋๋ก ๋ณํ๋๋ค.
- ์๋ฐ์คํฌ๋ฆฝํธ์์ HTML ์์ฑํ๋ฏ์ด ํ๊ธฐ ๋๋ฌธ์ ๊ฐ๋์ฑ์ด ๋๊ณ  ์์ฑํ๊ธฐ ์ฝ๋ค.
- ๊ฐ๋ฐ์๊ฐ JSX๋ฅผ ์์ฑํ๋ฉด ๋ฆฌ์กํธ ์์ง์ JSX๋ฅผ ๊ธฐ์กด ์๋ฐ์คํฌ๋ฆฝํธ๋ก ํด์ํ๋ค. ์ด๋ฅผ `์ ์ธํ ํ๋ฉด ๊ธฐ์ `์ด๋ผ๊ณ  ํ๋ค.

<br />

## ๐จ๐ปโ๐ป JSX ๋ฌธ๋ฒ

- ๋ฐ๋์ ๋ถ๋ชจ ์์ ํ๋๊ฐ ๊ฐ์ธ ์๋ ํํ์ฌ์ผ ํ๋ค.

```jsx
// ์ ์ ์ฝ๋ 1(<div></div>)
function App() {
  return (
    <div>
      <div>Hello</div>
      <div>GodDaeHee!</div>
    </div>
  );
}

// ์ ์ ์ฝ๋ 2(<React.Fragment></React.Fragment>)
function App() {
  return (
    <React.Fragment>
      <div>Hello</div>
      <div>GodDaeHee!</div>
    </React.Fragment>
  );
}

// ์ ์ ์ฝ๋(<></>)
function App() {
  return (
    <>
      <div>Hello</div>
      <div>GodDaeHee!</div>
    </>
  );
}
```

<br />

- JSX ์์์๋ `{}` ๋ฅผ ์ฌ์ฉํด ์๋ฐ์คํฌ๋ฆฝํธ ํํ์์ ์์ฑํ  ์ ์๋ค.

```jsx
function App() {
  const name = "JeonMinjae";

  return (
    <div>
      <div>Hello</div>
      <div>{name}!</div>
    </div>
  );
}
```

<br />

- if๋ฌธ๊ณผ for๋ฌธ ๋์  `์ผํญ ์ฐ์ฐ์`๋ `&& ์ฐ์ฐ์`๋ฅผ ์ด์ฉํ ์กฐ๊ฑด๋ถ ๋ ๋๋ง

```jsx
function App() {
  const name = "react";

  return (
    <div>
      <div>Hello</div>
      <div>{name === "react" ? <h1>True</h1> : <h1>False</h1>}</div>
    </div>
  );
}
```

<br />

- JSX์์ ์๋ฐ์คํฌ๋ฆฝํธ ๋ฌธ๋ฒ์ ์ฐ๋ ค๋ฉด `{}`๋ฅผ ์ฌ์ฉํด์ผ ๋๊ธฐ ๋๋ฌธ์, ์คํ์ผ์ ์ ์ฉํ  ๋์๋ ๊ฐ์ฒด ํํ๋ก ๋ฃ์ด์ฃผ์ด์ผ ํ๋ค. ๋ํ camelCase ํ๋กํผํฐ ๋ช๋ช ๊ท์น์ ์ฌ์ฉํ๋ค.

```jsx
function App() {
  const name = "JeonMinjae";

  return (
    <div>
      <div>Hello</div>
      <div style={{ fontSize: "12px" }} className="name">
        {name}
      </div>
    </div>
  );
}
```

<br />

## ์ฐธ๊ณ 

- https://www.notion.so/a42647e064864e469b66acacfe69652b
