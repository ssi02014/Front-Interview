# 💻 React 재조정(Reconciliation)

## 👨🏻‍💻 개요

- React는 `선언적 API`를 제공하기 때문에 갱신이 될 때마다 매번 무엇이 바뀌었는지 걱정할 필요가 없다. 이는, 애플리케이션 작성을 무척 쉽게 해주지만, React 내부에서 어떤 일이 발생하는 지는 명확하게 확인하지 못한다.
- 리액트에서는 내부적으로 비교(diffing) 알고리즘으로 시간 복잡도 `O(N)`을 가진 `휴리스틱(heuristic) 알고리즘`을 구현해서 적용한다.
- 리액트는 해당 비교 알고리즘을 통해 컴포넌트의 업데이트가 `예측 가능`해지면서 `고성능` 앱이라고 불러도 손색없을 만큼 빠른 앱을 만들 수 있다.
- 리액트는 다음 `두 가지 가정`을 기반으로 휴리스틱 알고리즘을 구현하였다.

```
1. Two elements of differnt types will produce different trees.
 : 서로 다른 타입을 가진 두 엘리먼트는 다른 트리를 만들어 낸다.

2. The developer can hit at which child elements may be stable across different renders with a key prop.
 : 개발자가 key prop를 통해 자식 엘리먼트의 변경 여부를 표시할 수 있다.
```

<br />

## 👨🏻‍💻 Virtual Dom 이점

![스크린샷 2022-10-04 오후 5 48 05](https://user-images.githubusercontent.com/64779472/193776317-a26f780d-c18a-4a49-a1b6-6c425d17fa5c.png)

- React에서 state나 props가 갱신되면 `render()` 함수가 호출되어 `새로운 엘리먼트(Virtual DOM) 트리를 반환`한다.
- 이때, 효과적으로 UI를 갱신하기 위해서 기존의 오래된 엘리먼트(`Old` Virtual DOM) 트리와 새로운 엘리먼트(`New` Virtual DOM) 트리를 비교해 차이점을 찾아내, 변경된 부분만 `실제 돔(Real DOM)`에 반영한다.
- 즉, Virtual DOM은 DOM이 변경될 때마다 전체 DOM을 `Reflow`하는 것이 아니라 한번만 Reflow를 수행함으로써 부하를 줄이는 것이다.

<br />

## 👨🏻‍💻 비교(diffing) 알고리즘

- 리액트는 두 개(old, new)의 Virtual DOM 트리를 비교할 때, 루트(Root)부터 비교한다. 이후의 동작은 루트 엘리먼트의 타입에 따라 달라진다.

<br />

### 엘리먼트 타입이 다를 경우

```jsx
// div와 p는 다르기 때문에 div는 제거된 후 p태그와 그 하위 엘리먼트가 추가
<div>
  <Counter />
</div>

<p>
  <Counter />
</p>
```

- 위 예제처럼 두 Virtual DOM 트리의 루트 엘리먼트 타입(`div, p`)이 다르면, 리액트는 `이전 트리를 완전히 버리고 새로운 트리를 구축`한다.
- 트리를 버릴 때 이전 DOM 노드들은 모두 파괴된다. 이때 컴포넌트 인스턴스는 `componentWillUnmount()`가 실행된다.
- 새로운 DOM 노드들이 DOM에 삽입될 때는 `componentWillMount()`가 실행되고, `componentDidMount()`가 이어서 실행됩니다.
  - 이전 트리와 연관된 모든 state는 사라집니다. 또한, 루트 엘리먼트 아래의 모든 컴포넌트도 언마운트되고 그 state도 사라지게 된다.
  - 위 예제에서 Counter는 사라지고, 새로 다시 마운트가 될 것이다.

```
componentWillUnmount() : DOM 노드 파괴될 때 실행.
componentWillMount() : 새로운 DOM 노드가 삽입되기 전에 실행.
componentDidMount() : 새로운 DOM 노드가 삽입된 후에 실행.
```

- 🙆🏻‍♂️ 여담으로 componentWillMount는 레거시 코드이며, 현재는 피해야되는 코드이다.
  - componentWillMount는 주로 브라우저가 아닌 `서버사이드 환경`에서 호출하는 용도로 사용했었으며, 더 이상 필요없게 되어 `리액트 v16.3`에서 deprecated되었다.

<br />

### DOM의 엘리먼트의 타입이 같은 경우

- 같은 타입의 두 React DOM 엘리먼트를 비교할 때는 React는 두 엘리먼트의 `속성(Attribute)`을 확인하여, 동일한 속성은 유지하고 변경된 속성들만 갱신한다.

```jsx
// className 변경
<div className="before" title="stuff" />
<div className="after" title="stuff" />
```

- 위 예제에서 두 엘리먼트를 비교하면 React는 현재 DOM 노드 상에 `className`만 수정한다.

```jsx
// style 속성의 color 변경
<div style={{color: 'red', fontWeight: 'bold'}} />
<div style={{color: 'green', fontWeight: 'bold'}} />
```

- 위 예제에서 React는 fontWeight는 수정하지 않고 `color` 속성만 수정한다.
- DOM 노드의 처리가 끝나면, 리액트는 이어서 `해당 노드의 자식들을 재귀적으로 처리한다.`

<br />

### 같은 타입의 Component Element

- 컴포넌트가 갱신되면 인스턴스는 동일하게 유지되어 렌더링 간 state가 유지된다.
- 리액트는 새로운 엘리먼트의 내용을 반영하기 위해 현재 컴포넌트 인스턴스의 props를 갱신한다.
- 이때 해당 인스턴스의 `componentWillReceiveProps`, `componentWillUpdate`, `componentDidUpdate`를 호출한다.
- 다음으로 render() 메서드가 호출되고 비교 알고리즘이 이전 결과와 새로운 결과를 재귀적으로 처리한다.

```
componentWillReceiveProps() : props 갱신 전 호출
componentWillUpdate() : 컴포넌트가 업데이트되기 전 호출
componentDidUpdate() : 컴포넌트가 업데이트된 후 호출
render() 메소드 호출 후 이전과 비교하여 재귀적으로 처리
```

- 🙆🏻‍♂️ 여담으로 componentWillReceiveProps와 componentWillUpdate는 레거시 코드이며, 현재는 피해야되는 코드이다.
  - componentWillReceiveProps는 [getDerivedStateFromProps](https://reactjs.org/docs/react-component.html#static-getderivedstatefromprops)로 대체할 수 있다.
  - componentWillUpdate는 [getSnapshotBeforeUpdate](https://reactjs.org/docs/react-component.html#getsnapshotbeforeupdate) 로 대체할 수 있다.

<br />

## 👨🏻‍💻 자식에 대한 재귀적 처리

- DOM 노드의 자식들을 `재귀적`으로 처리할 때, React는 기본적으로 두 리스트를 순차적으로 순회하고 차이점이 있으면 변경한다.
- 예를 들어, 아래 예제와 같이 자식의 끝에 엘리먼트를 추가하면, 순차적으로 비교하기 때문에 두 Virtual DOM 트리 사이의 변경은 잘 작동할 것이다.

```jsx
// 효율적 예시
<ul>
  <li>first</li>
  <li>second</li>
</ul>

<ul>
  <li>first</li>
  <li>second</li>
  <li>third</li>
</ul>
```

- 리액트는 두 트리에서 `<li>first</li>`가 일치하는 것을 확인하고, `<li>second</li>`가 일치하는 것을 확인한다. 그리고 마지막으로 `<li>third</li>`를 트리에 추가한다.
- 하지만, 아래 예제와 같이 리스트의 맨 앞에 엘리먼트를 추가하는 경우에는 성능이 좋지 않다.

```jsx
// 비 효율적 예시
<ul>
  <li>Duke</li>
  <li>Villanova</li>
</ul>

<ul>
  <li>Connecticut</li>
  <li>Duke</li>
  <li>Villanova</li>
</ul>
```

- React는 `<li>Duke</li>`와 `<li>Villanova</li>` 종속 트리를 그대로 유지하는 대신 모든 자식을 변경합니다. 이러한 비효율은 문제가 될 수 있다.

<br />

### Key

- 위와 같은 문제를 해결하기 위해 리액트는 `Key`를 지원한다. 자식들이 key를 갖고 있다면 리액트는 key를 통해 기존 트리와 이후 트리의 자식들이 일치하는지 확인한다.
- 예를 들어, 위에 비 효율적 예시에 key를 추가하여 트리의 변환 작업이 효율적으로 수행되도록 개선할 수 있다.

```jsx
// 비 효율적 예시에 key 추가
<ul>
  <li key="2015">Duke</li>
  <li key="2016">Villanova</li>
</ul>

<ul>
  <li key="2014">Connecticut</li>
  <li key="2015">Duke</li>
  <li key="2016">Villanova</li>
</ul>
```

- 이제 리액트는 `2014`key를 가진 엘리먼트가 새로 추가되었고, `2015`, `2016` key를 가진 엘리먼트들은 그저 이동만 하면 되는 것을 알 수 있다.
- key의 값으로는 `unique`한 값을 넣어줘야 한다. 최후의 수단으로 index를 넣어 줄 수 있지만 재배열되는 경우 비효율적으로 동작한다.

<br />

## 👨🏻‍💻 고려사항

- 리액트는 휴리스틱 알고리즘에 의존하고 있다. 따라서 휴리스틱이 기반하고 있는 가정에 부합하지 않는 경우 성능이 나빠질 수 있다.
  1. 알고리즘은 다른 컴포넌트 타입을 갖는 종속 트리들의 일치 여부를 확인하지 않습니다. 매우 비슷한 결과물을 출력하는 두 컴포넌트를 교체하고 있다면, 그 둘을 같은 타입으로 만드는 것이 더 나을 수도 있습니다.
  2. key는 반드시 변하지 않고, 예상 가능하며, 유일해야 합니다. 변하는 key(`Math.random()`으로 생성된 값 등)를 사용하면 많은 컴포넌트 인스턴스와 DOM 노드를 불필요하게 재생성하여 성능이 나빠지거나 자식 컴포넌트의 state가 유실될 수 있다.

<br />

## 👨🏻‍💻 참고 문서

- [리액트 재조정 공식문서](https://ko.reactjs.org/docs/reconciliation.html)

<br />
