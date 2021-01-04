---
layout: article
title: React 기초 개념
tag: React
---

React 기초 개념을 다시한 번 짚고 넘어가자

## Component

React의 가장 큰 특징이자 장점은 Component-based 라는 것

컴포넌트는 **"하나의 의미를 가진 독립적인 단위의 모듈"**인데,

쉽게 말해 나만의 HTML 태그라고 생각하면 된다

### 함수 컴포넌트와 클래스 컴포넌트

예를 들어 화면에 "Hello, {name}"을 띄운다고 하면

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

이렇게 `<h1>Hello, {props.name}</h1>` 엘리먼트를 반환하는

Welcome 이라는 컴포넌트를 정의해 주고

```jsx
const element = <Welcome name="Seunghye" />;

ReactDOM.render(element, document.getElementById('root'));
```

`ReactDOM.render()` 를 사용하여 만들어준 Welcome 컴포넌트를

element 라는 변수에 담아 호출해서 렌더링 해준다

컴포넌트의 이름은 항상 **대문자**로 시작해야 함

컴포넌트는 위와 같은 **함수형**으로 만들 수 있고, ES6 문법인 **class**를 이용하여 만들 수도 있다 !

```jsx
// class를 이용한 컴포넌트
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

## Props

props는 "상위 컴포넌트가 하위 컴포넌트에게 내려주는 데이터"이다

props = 객체

위 예시에서 element라는 엘리먼트를 만들 때 우리는 이미 props를 전달해 줬다

`<Welcome name="seunghye" />` 에서 `{name: "seunghye"}` 라는 객체,

props를 하위 `Welcome` 컴포넌트에 전달해줬고,

그로 인해 화면에 Hello, seunghye가 보이게 되는 것

Props 컴포넌트는 읽기 전용이다. 하위 컴포넌트는 props를 변경할 수 없고 사용만 할 수 있음 ⇒ 변경되지 말아야 할 데이터를 효율적으로 관리할 수 있음

## State

state는 **"컴포넌트가 독립적으로 갖는 상태"**이다

이 역시 객체의 형태로, 컴포넌트 안에서만 제어되어 보관, 관리됨

Welcome 메세지 뒤에 메세지가 렌더링 될 때의 현재 시각을 알려주는 텍스트를 렌더링 해보자

```jsx
class Clock extends React.Component {
	constructor(props) {
		super(props);
		this.state = {date: new Date()};
	}

render(){
	return (
		<div>
			<h1>Hello, {this.props.name}</h1>
			<h2>It is {this.state.date.toLocaleTimeString()}. </h2>
		</div>
	}
}

ReactDOM.render(
	<Clock name="seunghye" />,
	document.getElementById("root")
);
```

Clock 이라는 컴포넌트를 만들고, date라는 state를 지정해주면 됨

**state는 class component**만 가질 수 있음

```jsx
// 시계가 매 초마다 스스로 업데이트 하도록

class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = { date: new Date() };
  }

  componentDidMount() {
    this.timerID = setInterval(() => this.tick(), 1000);
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date(),
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, {this.props.name}</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(<Clock name="seunghye" />, document.getElementById('root'));
```

state를 직접 변경할 수 없고, React Component의 내장 메소드인 `setState()` 를 사용해야 한다 ⇒ `setState()` 가 실행될 때 마다 state가 변경된 것을 인지하고 표시될 내용을 알아내기 위해 `render()` 메소드를 다시 호출 함

## Lifting State Up

React는 **단방향 데이터 플로우**를 가지고 있음

즉, 부모만 자식에게 데이터를 줄 수 있고 자식은 부모에게 데이터를 줄 수 없다는 뜻

하지만, 자식이 부모의 상태를 변경해야 한다면?

⇒ Lifting state up 사용

1. 상위 컴포넌트에서 state를 변경시키는 함수를 만든다 `handleState = () => {this.setState()}`
2. 그리고 이 함수를 자식에게 props로 넘김
3. 자식은 이 함수를 받아 사용하면 부모의 상태가 변경됨. 이 때 상태가 변경하므로 `render` 가 다시 실행됨

이 때 중요한 것은, 상위 컴포넌트에서 this를 꼭 bind 해서 넘겨야 함
