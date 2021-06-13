# 💻 JSON(JavaScript Object Notation)
<br />

## 👨🏻‍💻 JSON
- 🌟 JSON이란, `JavaScript Object Notation`라는 의미의 축약어로 데이터를 저장하거나 전송할 때 많이 사용되는 `경량의 DATA 교환 형식`이다.
- 자바스크립트에서 객체를 만들 때 사용하는 표현식을 의미한다.
- JSON 표현식은 사람과 기계 모두 이해하기 쉬우며 용량이 작어서, 최근에는 JSON이 XML을 대체해서 데이터 전송 등에 많이 사용한다.
- JSON은 데이터 포맷일 뿐이며 어떠한 통신 방법도, 프로그래밍 방법도 아닌 단순히 데이터를 표시하는 표현 방법이다.

<br />

## 👨🏻‍💻 JSON의 특징
- 서버와 클라이언트 간의 교류에서 일반적으로 많이 사용한다.
- 자바스크립트 객체 표기법과 아주 유사하다.
- 자바스크립트를 이용하여 JSON 형식의 문서를 쉽게 자바스크립트 객체로 변환할 수 있는 이점이 있다.
- JSON 문서 형식은 자바스크립트 객체의 형식을 기반으로 만들어 졌다.
- 자바스크립트 문법과 유사하지만 `텍스트 형식`일 뿐이다.
- 자바스크립트 뿐만아니라 다른 프로그래밍 언어를 이용해서도 쉽게 만들 수 있다.
- 특정 언어에 종속되지 않는다. 대부분의 프로그래밍 언어에서 JSON 포맷의 데이터를 핸들링 할 수 있는 라이브러리를 제공한다. 

<br />

## 👨🏻‍💻 JSON 문법
- XML처럼 태그로 표현하기 보다는 `중괄호({})` 형식으로 하고, 값을 `,`로 나열하기에 표현이 간단하다.
- JSON 형식은 자바스크립트 객체와 마찬가지로 `key/value` 형식으로 구성되며, key값이나 문자열은 항상 `쌍따옴표("")`를 이용하여 표기한다.
- 객체, 배열 등의 표기를 사용할 수 있다.
- 일반 자바스크립트 객체처럼 원하는 만큼 중첩시켜서 사용할 수 있다.
- JSON형식에는 null, number, string, array, object, boolean을 사용할 수 있다.
```json
{
  "employees": [
    {
      "name": "Surim",
      "lastName": "Son"
    },
    {
      "name": "Someone",
      "lastName": "Huh"
    },
    {
      "name": "Someone else",
      "lastName": "Kim"
    } 
  ]
}
```

<br />

## 👨🏻‍💻 JSON 형식
### 🏃 name-value 형식의 쌍(pair)
- 여러 가지 언어들에서 object, hashtable, struct로 실현되었다.
- { String key: String Value }
```json
  {
    "firstName": "Kwon",
    "lastName": "YoungJae",
    "email": "kyoje11@gmail.com"
  }
```

<br />

### 🏃 값들의 순서화된 리스트 형식
- 여러 가지 언어들에서 배열(Array), 리스트(List)로 실현되었다.
- [value1, value2, ...]
```json
  {
    "firstName": "Kwon",
    "lastName": "YoungJae",
    "email": "kyoje11@gmail.com",
    "hobby": ["puzzles","swimming"]
  }
```

<br />

## 👨🏻‍💻 JSON을 JavaScript Object로 변환
- JSON.parse(JSON으로 변화시킬 문자열): JSON 형식의 텍스트를 자바스크립트 객체로 변환
- JSON.stringify(JSON 문자열로 변환할 값): 자바스크립트 객체를 JSON 텍스트로 변환한다.
```js
const jsonText = '{ "name": "Someone else", "lastName": "Kim" }'; // JSON 형식의 문자열
const realObject = JSON.parse(jsonText);
const jsonText2 = JSON.stringify(realObject);

console.log(realObject); // { name: 'Someone else', lastName: 'Kim' }
console.log(jsonText2); // {"name":"Someone else","lastName":"Kim"}
```

<br />

```js
    fetch("https://jsonplaceholder.typicode.com/posts", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(body),
    })
      .then((response) => response.json())
      .then((data) => console.log(data));
```
- 위는 fetch에서 사용된 JSON.stringify이다.

<br />

## 참고
https://velog.io/@surim014/JSON%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80 <br />
https://nesoy.github.io/articles/2017-02/JSON <br />
