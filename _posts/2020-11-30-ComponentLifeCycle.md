---
layout: article
title: React class component
tag: React
---

# React class component

![https://c17an.github.io/assets/images/2020-05-29-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EC%9D%98-%EC%83%9D%EB%AA%85%EC%A3%BC%EA%B8%B0/1.PNG](https://c17an.github.io/assets/images/2020-05-29-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EC%9D%98-%EC%83%9D%EB%AA%85%EC%A3%BC%EA%B8%B0/1.PNG)

react class component는 **Life cycle method**를 가지고 있다

component가 생성될 때, render 전에 호출되는 몇 가지 function들이 존재한다

mounting, updating, unmounting이 있는데

mounting은 태어나는 것,

updating은 말 그대로 일반적인 업데이트를 의미한다

unmounting은 component가 수명을 다하는 것을 의미한다

예를 들어, 페이지를 바꿀 때 component가 죽는 순간이다

state를 사용해서 component를 교체하기도 하는 등

component가 수명을 다하는 것에는 다양한 방법이 있다

# Mount

아래 메서드들은 컴포넌트의 인스턴트가 생성되어 DOM 상에 삽입될 때,

순서대로 호출된다

- **constructor()**
- static getDerivedStateFromProps()
- **render()**
- **componentDidMount()**

## constructor()

메서드를 바인딩하거나 state를 초기화하는 작업이 없다면,

생성자를 구현하지 않아도 된다

React.Component를 상속한 컴포넌트의 생성자를 구현할 때에는

`super(props)` 를 호출해야 한다

그렇지 않으면 `this.props` 가 생성자 내에서 정의되지 않아 버그로 이어질 수 있다

- this.state에 객체를 할당하여 지역 state를 초기화하기 위함
- 인스턴스에 이벤트 처리 메서드를 바인딩

`constructor()` 내부에서 setState()를 호출하면 안 된다

## render()

`render()` 에서드는 클래스 컴포넌트에서 반드시 구현되어야 하는 유일한 메서드이다

이 메서드가 호출되면 `this.props` 와 `this.state` 값을 활용하여 아래 것들 중 하나를 반환해야 한다

- **React 엘리먼트** (예를 들어 `<div />` 와 `<MyComponent />` 는 react가 DOM 노드 또는 사용자가 정의한 컴포넌트를 만들도록 지시하는 react 엘리먼트다)
- **배열과 Fragment**
- **Portal**
- **문자열과 숫자**
- **Boolean 또는 null**

`render()` 함수는 순수해야 한다

즉, 컴포넌트의 state를 변경하지 않고, 호출될 때 마다 동일한 결과를 반환해야 한다

## componentDidMount()

`componentDidMount()` 는 컴포넌트가 마운트된 직후,

즉 트리에 삽입된 직후에 호출된다

외부에서 데이터를 불러와야 한다면, 네트워크 요청을 보내기 적절한 위치다

`componentDidMount()` 에서 즉시 setState()를 호출하는 경우도 있다

이로 인해 추가적인 렌더링이 발생하지만, 브라우저가 화면을 갱신하기 전에 이루어 진다

이 경우 `render()` 가 두 번 호출되지만, 사용자는 그 중간 과정을 볼 수 없을 것이다

대부분의 경우, 앞의 방식을 대신하여 `constructor()` 메서드에서 초기 state를 할당할 수 있다

### 예시 코드

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);
    console.log('hello');
  }
  state = {
    count: 0,
  };
  add = () => {
    this.setState((current) => ({ count: current.count + 1 }));
  };
  minus = () => {
    this.setState((current) => ({ count: current.count - 1 }));
  };
  componentDidMount() {
    console.log('component rendered');
  }
  render() {
    console.log('rendering');
    return (
      <div>
        <h1>The number is {this.state.count}</h1>
        <button onClick={this.add}>Add</button>
        <button onClick={this.minus}>Minus</button>
      </div>
    );
  }
}
```

내 component가 mount될 때,

즉 component가 내 Website에 왔을 때 `constructor()` 함수가 호출되며,

console 창에 "hello"가 찍히는 것을 볼 수 있다

그 이후 `render()` 함수가 실행되며, console창에 "rendering"이 찍힌다

component가 render할 때 `componentDidMount()` 가 실행되어 "component rendered"라 찍히는 것을 볼 수 있다

# Update

props 또는 state가 변경되면 갱신이 발생한다

아래 메서드들은 컴포넌트가 다시 렌더링될 때 순서대로 호출된다

- static getDerivedStateFromProps()
- shouldComponentUpdate()
- **render()**
- getSnapshotBeforeUpdate()
- **componentDidUpdate()**

## componentDidUpdate()

`componentDidUpdate()` 는 갱신이 일어난 직후에 호출된다

이 메서드는 최초 렌더링에서는 호출되지 않는다

컴포넌트가 갱신되었을 때 DOM을 조작하기 위하여 이 메서드를 활용하면 좋다

또한, 이전과 현재의 props를 비교하여 네트워크 요청을 보내는 작업도 이 메서드를 사용하면 된다

(props가 변하지 않았다면 네트워크 요청 보낼 필요 X)

# Unmount

컴포넌트가 DOM 상에서 제거될 때 호출된다

- **componentWillUnmount()**

### 예시 코드

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);
    console.log('hello');
  }
  state = {
    count: 0,
  };
  add = () => {
    this.setState((current) => ({ count: current.count + 1 }));
  };
  minus = () => {
    this.setState((current) => ({ count: current.count - 1 }));
  };
  componentDidMount() {
    console.log('component rendered');
  }
  componentDidUpdate() {
    console.log('I just update!');
  }
  componentWillUnmount() {
    console.log('Good bye');
  }
  render() {
    console.log('rendering');
    return (
      <div>
        <h1>The number is {this.state.count}</h1>
        <button onClick={this.add}>Add</button>
        <button onClick={this.minus}>Minus</button>
      </div>
    );
  }
}
```

1. 위와 마찬가지로 우리가 웹사이트를 열면 constructor() 함수가 발생하여 "hello!"가 찍힘
2. Add 혹은 Minus 버튼을 눌러 상태를 업데이트 하면 "rendering"이 찍힌 후, 업데이트가 되었다는 "I just update!"가 찍힘
3. 우리가 다른 페이지로 이동하게 되면 componentWillUnmount() 함수가 발생하여 "Good bye"가 찍힘
