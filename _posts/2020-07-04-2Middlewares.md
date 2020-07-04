---
layout: article
title: Express Core - Middlewares
tag: NodeJS
---

## Express Core: Middlewares

### middlewares

middleware에 대해 알아보자    
express에서 middleware란  
구조 내에서 중간 처리를 위한 함수를 말한다  
쉽게 말해, **요청과 응답사이에서 거쳐가는 함수**라고 할 수 있다  

우선 우리가 이해해야할 것은 <u>'어떻게 연결이 시작되는가'</u>이다  
request가 어떻게 시작되는 걸까?
시작은 브라우저에서 부터다
우리가 웹사이트에 접속하려고 할 때!  
이 때가 바로 시작점이다  

시작이 되면 index파일을 실행할 것이고,  
우리의 application이 route가 존재하는지 살펴본다    
우리가 <a>localhost:4000/</a>을 주소창에 입력시키고 실행하면  
route가 존재하는지 찾은 다음 (/)이 부분을 보고  
*'이 사용자는 home을 요청하는구나'*라고 받아들인다  
그리고 home을 찾은 후, handleHome 함수를 실행할 것이다  
그럼 handleHome 함수는 우리에게  
'Hello from home!' 이라고 응답을 전송하는 것이다  

하지만 이런 흐름들은 보통 이렇게 간단하게 진행되진 않는다  
보통 중간단계를 거치게 되는데 다시 말해,  
**유저와 마지막 응답 사이에 어떤 것이 존재**한다  
이 것을 바로 **middleware**라고 한다  
express에서의 모든 함수는 middleware가 될 수 있다  

```js
const handleHome = (req, res) => res.send("Hello from home!");

app.get("/", handleHome);
```
우리가 이전에 만들어 놓았던 코드로 middleware를 만들어보자

```js
const handleHome = (req, res) => res.send("Hello from home!");

const betweenHome = () => console.log("I'm between");

app.get("/", betweenHome, handleHome);
```
betweenHome 함수를 만들어 준 다음,  
유저가 home(/)을 요청하고,  
'Hello from home!'으로 응답하는 사이에 둬보자  
이 상태로 새로고침을 하면 console.log로  
'I'm between'을 출력하는 것을 볼 수 있다   

여기서 문제는 구글 크롬으로부터 온 요청을 **계속 처리할 지에 대한 권한을 주지않았다**   
그래서 우리는 그 요청이 handleHome으로 처리할 수 있는 권한을 줘야한다    
바로 **next**라고 하는 key를 이용해서 말이다  

### next

```js
const handleHome = (req, res) => res.send("Hello from home!");

const betweenHome = (req, res, next) => {
    console.log("I'm between");
    next();
}

app.get("/", betweenHome, handleHome);
```
betweenHome 함수에 next를 추가해주자  
express의 connection을 다루는 건  
**request, response** 그리고 **next**이다  
하지만 handleHome 함수에는 next를 넣어줄 필요가 없다  
왜냐하면 handleHome은 middleware가 아닌 마지막 함수기 때문  

아무튼, betweenHome함수에 next key를 추가해주고,  
콘솔로그를 찍은 다음 next 함수를 호출하자  
next함수가 곧 handleHome이 되는 것이다  
이렇게 작성 후 새로고침을 해보면  
console창에 'I'm between'이 뜨고,  
웹 사이트에 'Hello from home!'이 뜨는 것을 볼 수 있다  

### app.use

```js
app.use(betweenHome);
```
이렇게 두면 betweenHome을 **전역적**(globally)으로 둘 수도 있다  
모든 route에 대해서 동작하도록 말이다  

middleware는 우리가 원하는 만큼 가질 수 있는데,  
이 middleware는 **순차적으로 진행**이 된다   
middleware로 유저의 로그인 여부를 체크할 수도 있고,  
파일을 전송할 때 중간에서 가로채 어딘가로 upload할 수도 있고,  
또한 어딘가로 로그를 작성하는 middleware도 가질 수 있다  
이것이 middleware의 기본이고, 작동 원리이다  