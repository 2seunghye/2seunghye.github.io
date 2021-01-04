---
layout: article
title: Input 상태 관리 / useRef
tag: React
---

# useState Input 관리

useState를 이용해 input 상태 관리하는 법을 알아보자

input에 입력하는 값이 하단에 나타나게 하고,

초기화 버튼을 누르면 input 값이 비워지도록 구현해보자

![2020-12-18%20Input%20%E1%84%89%E1%85%A1%E1%86%BC%E1%84%90%E1%85%A2%20%E1%84%80%E1%85%AA%E1%86%AB%E1%84%85%E1%85%B5%20useRef%20ceeffb1334f443aea0d718461b8128f4/Dec-18-2020_17-23-33.gif](2020-12-18%20Input%20%E1%84%89%E1%85%A1%E1%86%BC%E1%84%90%E1%85%A2%20%E1%84%80%E1%85%AA%E1%86%AB%E1%84%85%E1%85%B5%20useRef%20ceeffb1334f443aea0d718461b8128f4/Dec-18-2020_17-23-33.gif)

```jsx
// InputSample.js

import React, { useState } from 'react';

function InputSample() {
  const [text, setText] = useState('');

  const onChange = (e) => {
    setText(e.target.value);
  };

  const onReset = () => {
    setText('');
  };
  return (
    <div>
      <input onChange={onChange} value={text} />
      <button onClick={onReset}>초기화</button>
      <div>
        <b>값: </b>
        {text}
      </div>
    </div>
  );
}

export default InputSample;
```

```jsx
// App.js

function App() {
  return <InputSample />;
}

export default App;
```

이번에는 input의 `onChange` 라는 이벤트를 사용한다

이벤트에 등록하는 함수에서 이벤트 객체 `e` 를 파라미터로 받아와서 사용할 수 있다

이 객체의 `e.target` 은 이벤트가 발생한 DOM인 input DOM을 가르킨다

이 DOM의 `value` 값, 즉 `e.target.value` 를 조회하면 현재 input에 입력한 값이 무엇인지 알 수 있다

이 값을 `useState` 를 통해 관리해주면 됨

이 때 주의해야하는 점은 input 상태를 관리할 때는

input태그의 `value` 값을 설정해주어야 한다는 것이다

그렇게 해야, 상태가 바뀌었을 때 input의 내용도 업데이트 된다

# 여러개의 input 상태 관리하기

![2020-12-18%20Input%20%E1%84%89%E1%85%A1%E1%86%BC%E1%84%90%E1%85%A2%20%E1%84%80%E1%85%AA%E1%86%AB%E1%84%85%E1%85%B5%20useRef%20ceeffb1334f443aea0d718461b8128f4/Dec-18-2020_17-21-00.gif](2020-12-18%20Input%20%E1%84%89%E1%85%A1%E1%86%BC%E1%84%90%E1%85%A2%20%E1%84%80%E1%85%AA%E1%86%AB%E1%84%85%E1%85%B5%20useRef%20ceeffb1334f443aea0d718461b8128f4/Dec-18-2020_17-21-00.gif)

```jsx
// InputSample.js

import React, { useState } from 'react';

function InputSample() {
  const [inputs, setInputs] = useState({
    name: '',
    nickname: '',
  });

  const { name, nickname } = inputs;

  const onChange = (e) => {
    const { name, value } = e.target;

    setInputs({
      ...inputs,
      [name]: value,
    });
  };

  const onReset = () => {
    setInputs({
      name: '',
      nickname: '',
    });
  };
  return (
    <div>
      <input placeholder="이름" name="name" onChange={onChange} value={name} />
      <input placeholder="닉네임" name="nickname" onChange={onChange} value={nickname} />
      <button onClick={onReset}>초기화</button>
      <div>
        <b>값: </b>
        {name} ({nickname})
      </div>
    </div>
  );
}

export default InputSample;
```

input의 개수가 여러 개 일 때는 단순히 `useState` 를 여러번 사용하고 `onChange` 도 여러 개 만들어서 구현할 수 있지만

더 좋은 방법은 `input` 에 `name` 을 설정하고 이벤트가 발생했을 때 이 값을 참조하는 것

그리고 `useState` 에서는 문자열이 아니라 **객체 형태의 상태**를 관리해 주어야 함

리액트 상태에서 객체를 수정할 때는

```jsx
inputs[name] = value;
```

위와 같이 수정하면 안 됨

새로운 객체를 만들어서 새로운 객체에 변화를 주고 이를 상태로 사용해주어야 한다

```jsx
setInputs({
  ...inputs,
  [name]: value,
});
```

❗️이 부분이 핵심

객체의 내용을 모두 "펼쳐서" 기존 객체를 복사하고,

[name]의 값을 `value` 로 업데이트 한다는 의미

이러한 작업을 "불변성을 지킨다" 라고 부른다

불변성을 지켜주어야만 리액트 컴포넌트 상태가 업데이트 됐음을 감지할 수 있고,

이에 따라 필요한 리렌더링이 진행된다

만약 `inputs[name]=value` 와 같이 기존 상태를 직접 수정하게 되면, 값을 바꿔도 리렌더링이 되지 않음

# useRef

JavaScript를 사용할 때는, 특정 DOM을 선택해야하는 상황에서 `getElementById` , `querySelector` 같은 DOM Selector 함수를 사용한다

리액트를 사용하는 프로젝트에서도 가끔씩 DOM을 직접 선택해야하는 상황이 발생한다

예를 들어, 특정 엘리먼트의 크기를 가져와야 한다든지, 스크롤바 위치를 가져와야 한다든지, 포커스를 설정해줘야한다든지 등 다양항 상황이 있다

이 때 리액트에서 사용하는 것이 `ref` 이다

함수형 컴포넌트에서 `ref` 를 사용할 때는 `useRef` 라는 Hook함수를 사용한다

우리가 위에서 만든 InputSample에서는 초기화 버튼을 누르면 초기화 버튼에 포커스가 그대로 남아있게 된다

초기화 버튼을 클릭했을 때 이름 input에 포커스가 잡히도록 `useRef` 를 사용해보자

![2020-12-18%20Input%20%E1%84%89%E1%85%A1%E1%86%BC%E1%84%90%E1%85%A2%20%E1%84%80%E1%85%AA%E1%86%AB%E1%84%85%E1%85%B5%20useRef%20ceeffb1334f443aea0d718461b8128f4/Dec-18-2020_17-51-00.gif](2020-12-18%20Input%20%E1%84%89%E1%85%A1%E1%86%BC%E1%84%90%E1%85%A2%20%E1%84%80%E1%85%AA%E1%86%AB%E1%84%85%E1%85%B5%20useRef%20ceeffb1334f443aea0d718461b8128f4/Dec-18-2020_17-51-00.gif)

```jsx
// InputSample.js

// useRef 추가
import React, { useState, useRef } from 'react';

function InputSample() {
  const [inputs, setInputs] = useState({
    name: '',
    nickname: '',
  });

  // useRef()를 사용하여 Ref객체를 만듦
  const nameInput = useRef();

  const { name, nickname } = inputs;

  const onChange = (e) => {
    const { name, value } = e.target;

    setInputs({
      ...inputs,
      [name]: value,
    });
  };

  const onReset = () => {
    setInputs({
      name: '',
      nickname: '',
    });
    // focus 설정
    nameInput.current.focus();
  };
  return (
    // 우리가 선택하고 싶은 DOM에 ref값으로 설정해줌
    <div>
      <input placeholder="이름" name="name" onChange={onChange} value={name} ref={nameInput} />
      <input placeholder="닉네임" name="nickname" onChange={onChange} value={nickname} />
      <button onClick={onReset}>초기화</button>
      <div>
        <b>값: </b>
        {name} ({nickname})
      </div>
    </div>
  );
}

export default InputSample;
```

`useRef()` 를 사용하여 Ref 객체를 만들고,

이 객체를 우리가 선택하고 싶은 DOM에 `ref` 값으로 설정해 준다

그러면, Ref 객체의 `.current` 값은 우리가 원하는 DOM을 가르키게 됨

위 예제에서는 `onReset` 함수에서 input에 포커스를 하는 `focus()` DOM API를 호출해 주었다
