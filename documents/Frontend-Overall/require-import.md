# 💻 require와 import
<br />

## 👨🏻‍💻 require와 import
- 기본적으로 require와 import를 모듈 키워드이다. 외부 파일이나 라이브러리를 불러올 때 사용한다.
- require는 Node.js에서 사용되고 있는 `CommonJs` 모듈 키워드이고, import는 `ES6`에서 새로 도입된 모듈 키워드이다.
- 둘 다 다른 파일의 코드를 불러온다는 같은 목적을 갖고 있지만, 다른 문법 구조를 지니고 있다.

<br />

### 🏃 기본 예제
```js
  const library = require('library');
  
  import library from 'library';
```

<br />

### 🏃 주요 차이점
- require는 CommonJS를 사용하는 Node.js의 키워드이지만 import()는 ES6에서 도입된 키워드이다.
- require는 파일에 작성한 곳에  남아 있으며 import는 항상 맨 위로 이동한다.
- require는 프로그램의 어느 지정에서나 호출 할 수 있지만 import()는 파일의 시작 부분에서만 실행할 수 있다.
- require과 import는 동시에 사용할 수 없다.

<br />

### 🏃 정리
-  일반적으로 import가 사용자가 필요한 모듈 부분만 선택하도 불러올 수 있기 때문에 더 선호된다. 또한, require보다 성능이 우수하며 메모리를 절약할 수 있다.
- 최근 ES6 모듈 시스템인 import가 많이 사용되고 있지만 아직까지 import 키워드가 100% 대체되어 사용할 수 없다. 
- `<script>` 태그를 사용하는 브라우저 환경, `Node.js`에서도 아직은 CommonJS를 기본 모듈 시스템으로 채택하고 있기 때문에 `Babel`과 같은 ES6 코드를 변환(transpile)해주는 도구를 사용할 수 없는 경우에는 require 키워드를 사용해야 한다.

<br />