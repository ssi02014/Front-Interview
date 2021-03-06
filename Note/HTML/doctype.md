# ๐ป HTML - DOCTYPE
<br />

## ๐จ๐ปโ๐ป DOCTYPE
- DOCTYPE์ Document Type์ ์ฝ์ด์ด๋ค.
- HTML์ `<html>`, `<head>`, `<body>`๋ก ๊ตฌ์ฑ๋์ด ์๋ค. ๊ทธ๋ฌ๋ ์ค์ํ ๋ ํ๋ DOCTYPE์ด ์๋ค. DOCTYPE์ `<html>` ํ๊ทธ ๋ณด๋ค ๋จผ์  ์ ์ธํ๋ ๊ฒ์ด ์ผ๋ฐ์ ์ด๋ฉฐ, `<!DOCTYPE html ...>` ํ์์ผ๋ก ์ ์ธํ๋ค. ์ด๋, ํ๊ทธ๊ฐ ์๋๊ธฐ ๋๋ฌธ์ `</>`๊ณผ ๊ฐ์ด ๋ซ์์ฃผ์ง ์์๋ ๋๋ค.
- HTML์ ํ ๊ฐ์ ์ข๋ฅ๊ฐ ์๋๋ผ ์ฌ๋ฌ ์ข๋ฅ๊ฐ ์๋ค. HTML 4.01 Strict, HTML 4.01 Transitional, XHTML 1.0 ๋ฑ์ด ์๋ค. HTML ์ข๋ฅ์ ๋ฐ๋ผ ๊ฐ์ ์ฝ๋์ HTML ํ์ผ์ ์คํํ์ ๋ ๋ค๋ฅธ ๊ฒฐ๊ณผ๊ฐ ๋ํ๋๋ค.
- ๊ทธ๋ ๊ธฐ ๋๋ฌธ์ `<!DOCTYPE html ...>`์ ์ ์ธํด์ ์ด๋ค HTML ํ์ค์ ๋ฐ๋ผ ์์ฑ๋์์์ ๋ธ๋ผ์ฐ์ ์ ์๋ ค์ค๋ค. ๋ง์ฝ DOCTYPE์ ์ ์ธํ์ง ์์ผ๋ฉด ๋ธ๋ผ์ฐ์ ๋ ์ฌ์ฉ์๊ฐ HTML 4.01์ธ์ง, XHTML 1.0์ธ์ง, HTML5 ์ธ์ง ๋ฌด์์ ๊ธฐ๋ฐ์ผ๋ก ์ฝ๋๋ฅผ ์์ฑํ๋์ง ์ ์๊ฐ ์๋ค.
- DOCTYPE์ ์ ์ธํ  ๊ฒฝ์ฐ ์ด๋ฅผ `Standards Mode(ํ์ค ๋ชจ๋)`๋ผ ํ๊ณ , ์ ์ธ ํ์ง ์๋ ๊ฒฝ์ฐ๋ฅผ `Quirks Mode(๋นํ์ค ๋ชจ๋, ํธํ ๋ชจ๋)`๋ผ๊ณ  ํ๋ค. ํธํ ๋ชจ๋์ ๊ฒฝ์ฐ ๊ฐ ๋ธ๋ผ์ฐ์ ๋ง๋ค ๋ฌธ์๋ฅผ ๋ํ๋ด๋ ๋ฐฉ์์ด ๋ค๋ฅด๊ธฐ ๋๋ฌธ์ `ํฌ๋ก์ค ๋ธ๋ผ์ฐ์ง ์ด์`๊ฐ ์ฌ๊ฐํ๋ค.

<br />

- ํ์ค ๋ชจ๋ ์์ค ์ฝ๋(HTML 5)
```html
<!DOCTYPE html>
<html>
  <head>
  </head>
  <body>
  </body>
</html>
```

<br />

- ๋นํ์ค ๋ชจ๋ ์์ค ์ฝ๋
```html
<html>
  <head>
  </head>
  <body>
  </body>
</html>
```

<br />

## ๐จ๐ปโ๐ป DTD
- `DTD(Document Type Definition)`๋ ๋ฌธ์ ํ์์ ์ ์ํด๋์ ๊ฒ์ผ๋ก DOCTYPE์ ๋ช์ํ  ๋ ์ฌ์ฉํ๋ค. ์ฆ, HTML ๋ฌธ์๊ฐ ์ด๋ค ๋ฌธ์ ํ์์ ๋ฐ๋ฅด๋์ง DOCTYPE์์ DTD๋ฅผ ์ง์ ํ๋ ๊ฒ์ด๋ค.
- ๋ฐ์ ์์๋ฅผ ์ฐธ๊ณ ํ๊ณ  ๋ ์์ธํ๊ฒ ์๊ณ  ์ถ๋ค๋ฉด [W3C Recommended list of Doctype declarations](https://www.w3.org/QA/2002/04/valid-dtd-list.html) ๋ฅผ ํ์ธํ๋ค.

<br />

- XHTML 1.1
- XHTML 1.0
  - Strict DTD
  - Transitional DTD
  - Frameset DTD 
- HTML 4.01
  - Strict DTD
  - Transitional DTD
  - Frameset DTD
- HTML 5

<br />

- ํ ์์ ์์  `HTML5`์ DTD DOCTYPE์ ๋ช์ํ๋ ๊ฒ์ด ์ ์ผ ๋ฐ๋์งํ๋ค.
```html
<!DOCTYPE html>
```

<br />

## ์ฐธ๊ณ 
https://github.com/baeharam/Must-Know-About-Frontend/blob/master/Notes/html/doctype.md <br />
https://developerjio.tistory.com/entry/HTML-DOCTYPE%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B4%EB%A9%B0-%EC%99%9C-%EC%82%AC%EC%9A%A9%ED%95%A0%EA%B9%8C <br />
https://theqoop.tistory.com/265 <br />
