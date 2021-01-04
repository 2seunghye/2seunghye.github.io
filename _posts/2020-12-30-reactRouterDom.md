---
layout: article
title: react-router-dom
tag: React
---

# 2020-12-30 :: react-router-dom

리액트 라우트를 쓰기 위한 모듈

react-router와 react-router-dom 이 필요하다

```jsx
npm i react-router react-router-dom
```

react-router는 웹, 앱 모두 사용할 수 있음

react-router-dom은 웹브라우저에서 사용하기 위해 필요한 것

react-router만 설치해도 종속성에 의해 react-router-dom이 설치됨

종류는 staticRouter와 hashRouter,BrowserRouter가 있다

제일 많이 쓰는 건 BrowserRouter

```jsx
import React from 'react';
import { BrowerRouter } from 'react-touter-dom';
import TestChild from './TestChild';

const Test () => {
	retern (
		<BrowserRouter>
			<Link to="주소">라우터보기</Link>
			<Route path="./경로" component={TestChild}></Route>
		</BrowserRouter>
	)
};
```

가상의 주소로 넘어갈 수 있도록 앵커 태그가 필요한데,

a 태그를 사용할 경우 에러가 난다

리액트 라우터는 페이지가 존재하는게 아니라 페이지가 이동하는 것처럼 흉내내는 것이기 때문

따라서 브라우저에서 제공하는 a 태그를 사용할 경우 라우터가 인식하지 못함

리액트 라우터에서 제공하는 <Link> 태그를 사용해 준다

<Link> 태그는 페이지의 이동이 아니라 보여지게 흉내내는 것

라우터에게 보여져야 할 주소값을 전달한다

브라우저 상에서는 Link가 a 태그로 표현됨

이 때 Link 태그를 클릭하여 주소를 이동한 후에 새로고침을 하게 되면 에러가 발생한다

또한 주소창에 주소를 입력하고 접근해도 에러가 발생

이것은 주소창으로 접근시에 서버에 요청이 가기 때문인데,

가상의 주소는 프론트에서만 알고 있기 때문에 서버에서는 에러를 반환한다

이 부분은 실제 페이지가 여러개가 아니기 때문

```jsx
import React from 'react';
import './App.css';
import WordBookPage from './View/WordBookPage';
import Test from './routes/Test';
import Gnb from './Components/Navigation/Gnb';

import { HashRouter, Route } from 'react-router-dom';

function App() {
  return (
    <HashRouter>
      <Gnb />
      <Route path="/" exact={true} component={WordBookPage} />
      <Route path="/test" component={Test} />
    </HashRouter>
  );
}

export default App;
```

첫번째 라우트의 경우 `exact` 가 붙어있는데

이게 붙어있으면 주어진 경로와 정확히 맞아 떨어져야만 설정한 컴포넌트를 보여준다

만약 `exact` 를 붙이지 않고 실행한다면

WordBookPage와 Test 두 컴포넌트가 같이 보여진다

왜냐하면 `/test` 에도 `/` 가 있기 때문에 매칭이 되어 보여지기 때문

HashRouter는 BrowserRouter와 거의 비슷하지만 주소 사이에 hash 값이 들어가게 됨

[ localhost:3000/#/주소] 와 같은 형태로 보여짐

HashRouter의 장점은 주소를 이동한 후에 새로고침을 해도 에러가 나지 않고 화면이 나타난다

이유는 해쉬값(#) 때문

BrowserRouter는 주소가 깔끔한 대신 새로고침 시 서버에 요청이 들어가게 되는데 hashRouter는 해쉬값 때문에 서버에 요청이 가지 않는다

단점은 서버가 주소의 이동을 모름(페이지 존재유무)

관리자 페이지나 SEO에 전혀 상관이 없는 사이트 같은 경우에는 해쉬 라우터를 사용하기도 함

해쉬 라우터는 배포시 편한 장점이 있다

브라우저 라우터를 쓰면 검직엔진에는 검색이 되나 새로고침이나 주소값 접근의 문제를 해결해야 함

이것은 서버에 추가적인 세팅으로 해결할 수 있다

페이지가 존재하는 것을 서버에 알려줘야 함

서버쪽 세팅 시 검색엔진도 신경써야 함

### location, match, history

history에는 앞으로 가기, 뒤로 가기 등 페이지 이동에 대한 이력이 남아있음

제공하는 메서드들이 있어 go 나 go back 등의 기능을 제공할 수 있다

그래서 history를 통해 눈속임으로 페이지의 이동을 구현할 수 있음

match는 path가 실제 라우트에 등록한 값을 알 수 있다

:name(예시) 파라미터에 실제 어떤 값이 들어왔는지 알 수 있음

이 값은 match의 params에 들어가 있음

location은 주소에 대한 정보나 서치, 해쉬 값 등이 들어 있다

라우터에서 import 하던 것을 똑같이 import 해준다
