# ๐ป Enter URL Process

## ๐จ๐ปโ๐ป ์ฃผ์์ฐฝ์ URL์ ์๋ ฅํ๋ฉด ๋ฒ์ด์ง๋ ์ผ(CS)
1. ๋ธ๋ผ์ฐ์ ์ ์ฃผ์์ฐฝ์ URL์ ์๋ ฅ 

<br />

2. ๋ธ๋ผ์ฐ์ ๋ URL์ ํด์ํ๋ค.

```
  URL ๊ตฌ์กฐ: `scheme:[//[user:password@]host[:port]][/]path[?query][#fragment]`
```

<br />

3. URL์ด ๋ฌธ๋ฒ์ ๋ง์ผ๋ฉด Punycode encoding์ URL์ HOST ๋ถ๋ถ์ ์ ์ฉํ๋ค.

<br />

4. HSTS(HTTP Strict Transport Security)๋ชฉ๋ก์ ๋ก๋ํด์ ํ์ธํ๋ค.
    - HSTS ๋ชฉ๋ก์ ์์ผ๋ฉด ์ฒซ ์์ฒญ์ HTTPS๋ก ๋ณด๋ด๊ณ , ์๋ ๊ฒฝ์ฐ HTTP๋ก ๋ณด๋ธ๋ค.

```
  * HTTP Strict Transport Security๋? 
    HTTP ๋์  HTTPS๋ง์ ์ฌ์ฉํ์ฌ ํต์ ํด์ผ ํ๋ค๊ณ  ์น ์ฌ์ดํธ๊ฐ ์น ๋ธ๋ผ์ฐ์ ์ ์๋ฆฌ๋ ๋ณด์๊ธฐ๋ฅ
```

<br />

5. DNS(Domain Name Server)๋ฅผ ์กฐํํ๋ค.

```
  * DNS(Domain Name Server)๋?
    DNS๋ ๋๋ฉ์ธ๋ค์์๋ฒ๋ฅผ ์ผ์ปซ๋๋ค. 
    ์ธํฐ๋ท์ ์๋ฒ๋ค์ ์ ์ผํ๊ฒ ๊ตฌ๋ถํ  ์ ์๋ IP์ฃผ์๋ฅผ ๊ธฐ๋ณธ์ฒด๊ณ๋ก ์ด์ฉํ๋๋ฐ ์ซ์๋ก ์ด๋ฃจ์ด์ง ์กฐํฉ์ด๋ผ ์ธ๊ฐ์ด ๊ธฐ์ตํ๊ธฐ์๋ ๋ฌด๋ฆฌ๊ฐ ๋ฐ๋ฅธ๋ค. 
    ๋ฐ๋ผ์ DNS๋ฅผ ์ด์ฉํด IP์ฃผ์๋ฅผ ์ธ๊ฐ์ด ๊ธฐ์ตํ๊ธฐ ํธํ ์ธ์ด์ฒด๊ณ๋ก ๋ณํํ๋ ์์์ด ํ์ํ๋ฐ ์ด ์ญํ ์ DNS๊ฐ ํ๋ ๊ฒ์ด๋ค.
```

<br />

6. ARP(Address Resolution Protocol)๋ก ๋์์ IP์ MAC Address๋ฅผ ์์๋ธ๋ค.

```
  * ARP(Address Resolution Protocol)๋?
    IP์ฃผ์๋ฅผ MAC(Media Access Control)์ฃผ์๋ก ๋ณํํด์ฃผ๋ ํ๋กํ ์ฝ
```

<br />

7. ๋์๊ณผ TCP ํต์ ์ ํตํด Socket์ ์ฐ๋ค.

<br />

8. HTTPS์ธ ๊ฒฝ์ฐ TLS(Transport Layer Security) handshake๊ฐ ์ถ๊ฐ ๋๋ค.

<br />

9. HTTP ํ๋กํ ์ฝ๋ก ์์ฒญํ๋ค.

<br />

10. HTTP ์๋ฒ๊ฐ ์๋ตํ๋ค.

<br />

11. ์น ๋ธ๋ผ์ฐ์ ๊ฐ ๊ทธ๋ฆฐ๋ค. 
  - ์ฐธ๊ณ  [Browser Rendering Process](https://github.com/ssi02014/Front-Interview/blob/master/Note/Frontend-Overall/browser-rendering-process.md)

<br />

## ์ฐธ๊ณ 
https://owlgwang.tistory.com/1 <br />
https://m.blog.naver.com/PostView.nhn?blogId=rbdi3222&logNo=220623919036&proxyReferer=https:%2F%2Fwww.google.com%2F <br />