---
layout: article
title: 리스트와 Key
tag: React
---

## React에서 Key가 중요한 이유

리액트에서 key는 컴포넌트 배열을 렌더링했을 때 어떤 원소에 변동이 있는지 알기위해 필요하다

유동적인 데이터를 다룰 때, 원소를 새로 생성할 수도, 제거할 수도, 수정할 수도 있다

key가 없을 때는 리스트를 순차적으로 비교하면서 변화를 감지하지만

key가 있다면 이 값을 사용해 어떤 변화가 일어났는지 더욱 빠르게 알 수 있다

## 기본 리스트 컴포넌트

```jsx
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) => <li>{number}</li>);
  return <ul>{listItems}</ul>;
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(<NumberList numbers={numbers} />, document.getElementById('root'));
```

위 코드는 브라우저에는 정상적으로 보여지지만

콘솔창을 확인해보면 리스트의 각 항목에 key를 넣어야한다는 경고창이 뜬다

즉, 엘리먼트 리스트를 만들 때 key는 꼭 포함해주어야한다

```jsx
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) => <li key={number.toString()}>{number}</li>);
  return <ul>{listItems}</ul>;
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(<NumberList numbers={numbers} />, document.getElementById('root'));
```

다음과 같이 `numbers.map()` 안의 각 리스트 항목에 `key` 를 할당하면

키 누락 경고창이 더 이상 뜨지 않는 것을 볼 수 있다

key는 엘리먼트에 안정적인 고유성을 부여하기 위해, **배열 내부의 엘리먼트에 지정해야 함**

key를 선택하는 가장 좋은 방법은 리스트의 다른 항목들 사이에서 해당 항목을 고유하게 식별할 수 있는 문자열을 사용하는 것이다

보통의 경우 데이터 ID를 key로 사용함

```jsx
const todoItems = todos.map((todo, index) => <li key={index}>{todo.text}</li>);
```

만약 렌더링 한 항목에 대한 안정적인 ID가 없다면

최후의 수단으로 항목의 인덱스를 key로 사용할 수 있다

즉, map 함수에 전달되는 콜백 함수의 index값을 사용할 수 있음

항목의 순서가 바뀔 수 있는 경우 key에 인덱스를 사용하는 것은 권장하지 않음 ⇒ 성능이 저하되거나 컴포넌트의 state와 관련된 문제가 발생할 수 있음

## Key로 컴포넌트 추출하기

키는 주변 배열의 context에서만 의미가 있음

예를 들어, `ListItem` 컴포넌트를 추출한 경우,

`ListItem` 안에 있는 `<li>` 엘리먼트가 아니라

배열의 `<ListItem />` 엘리먼트가 key를 가져야 함

### 잘못된 key 사용법

```jsx
function ListItem(props) {
  const value = props.value;
  return (
    // 틀렸습니다! 여기에는 key를 지정할 필요가 없습니다.
    <li key={value.toString()}>{value}</li>
  );
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) => (
    // 틀렸습니다! 여기에 key를 지정해야 합니다.
    <ListItem value={number} />
  ));
  return <ul>{listItems}</ul>;
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(<NumberList numbers={numbers} />, document.getElementById('root'));
```

### 올바른 key 사용법

```jsx
function ListItem(props) {
  // 맞습니다! 여기에는 key를 지정할 필요가 없습니다.
  return <li>{props.value}</li>;
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) => (
    // 맞습니다! 배열 안에 key를 지정해야 합니다.
    <ListItem key={number.toString()} value={number} />
  ));
  return <ul>{listItems}</ul>;
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(<NumberList numbers={numbers} />, document.getElementById('root'));
```
