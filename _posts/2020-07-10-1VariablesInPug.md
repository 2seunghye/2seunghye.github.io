---
layout: article
title: Variables in Pug
tag: NodeJS
---

## Local Variables in Pug 

controller에 있는 정보를 템플릿에 추가하는 법을 알아보자  
한 템플릿에만 추가할 수도 있고, 전체 템플릿에 추가할 수도 있다    
우선, **템플릿 전체에 추가하는 법**부터 알아보자    
헤더가 라우트 객체에 접근하도록 해야하는데, 이를 위해서는 **미들웨어를 사용**해야한다  
미들웨어는 레이어와 같이 **위에서 밑으로 한단계씩** 내려간다  
middlewares.js파일을 생성해 locals라는 미들웨어를 만들어보자  
local변수를 global변수로 사용하도록 만들어주는 거라고 생각하면 된다  
local 기능을 통해 변수에 접근할 수 있다  

```js
export const localsMiddleware = (req, res, next) => {

}
```
우선 localMiddleware라는 함수를 만들어 **export한 후**,  
app.js에서 **import**해주자  
이제 이 함수에 **locals를 추가**할건데,   
locals가 추가되면 그것들을 템플릿, 컨트롤러, 어디에서든 사용할 수 있다  
미들웨어를 잘못 위치하면 router에서 locals에 접근을 못할 수 있기 때문에,   
어디에 위치시켜야할지 잘 알아야 한다  

```js
// 잘못된 예
app.use(routes.home, globalRouter);
app.use(routes.users, userRouter);
app.use(localsMiddleware);
app.use(routes.videos, videoRouter);
```
예를 들어, 저 위치에 미들웨어를 위치시키면  
앞서 알아보았듯 위에서 밑으로 실행되기 때문에  
globalRouter와 userRouter는 locals에 접근을 못한다  

```js
// 올바른 예
app.use(localsMiddleware);
app.use(routes.home, globalRouter);
app.use(routes.users, userRouter);
app.use(routes.videos, videoRouter);
```
그래서 미들웨어를 라우터 위에 위치시켜   
밑의 라우터들이 locals에 접근할 수 있도록 위치시켜주어야 한다

```js
exprot const localsMiddleware = (req, res, next) => {
    res.locals.siteName = "My Project";
}
```
이제 middleware에 locals를 추가해보자  
`res.locals`이후에 아무거나 설정할 수 있다  
예를 들어, 나는 템플릿 마다 title을 동일하게 주고싶어서  
siteName이라는 변수에 "My Project"라는 값을 설정해주었다  
이제 siteName은 어디서든 사용할 수 있다  

이전에 만들어두었던 main layout 페이지를 열어보자
```html
doctype html
html
    head
        title My Project
    body
        header
            h1 Project
        main
            block content
        footer
            span &copy; leesh's project
```
title에 직접 My Project라고 입력한 것을 볼 수 있다  
이것을 locals를 사용해 변경해보자

```html
doctype html
html
    head
        title #{siteName}
    body
        header
            h1 Project
        main
            block content
        footer
            span &copy; leesh's project
```
**#{siteName}**이라고 작성해주면,  
타이틀에 My Project값이 잘 뜨는 것을 확인할 수 있다

또 다른 locals도 추가해보자

```js
exprot const localsMiddleware = (req, res, next) => {
    res.locals.siteName = "My Project";
    res.locals.routes = routes;
}
```
routes에 routes.js객체를 추가하였다  
이 파일 또한 import해보자  
이제 routes는 어디서든 사용할 수 있게 되었다  

```html
header.header
    .header_column
    a(href=routes.home)
        i.fab.fa-youtube
    .header_column
        ul
            li 
                a(href=routes.join) Join
            li 
                a(href=routes.login) Log In 
```
locals의 routes를 이렇게 활용할 수 있다  

```js
exprot const localsMiddleware = (req, res, next) => {
    res.locals.siteName = "My Project";
    res.locals.routes = routes;
    next();
}
```
그리고 가장 중요한 것!  
**미들웨어가 next에 req를 전달**해야한다  
미들웨어가 커넥션과 라우트들 사이에 있으니 next()를 입력해주어야 한다  
즉, **코드 사이에 들어가있기 때문에 <u>next함수를 써 주어야만,</u>**  
**<u>다음 함수로 넘어간다는 것</u>**이다 

이렇게 전역적으로(글로벌) 사용할 수 있는 변수를 추가하고, 사용해보았다  
이 변수들은 앞서 말했듯, 모든 템플릿에서 사용할 수 있다 

## Template Variables in Pug

이번엔 한 템플릿에만 변수를 추가하는 방법을 알아보자  
지금 내 프로젝트의 타이틀은 "My Project"이다    
근데 타이틀의 형식을 "home | My Project", "join | My Project" 이런 식으로,    
페이지마다 타이틀이 변경되도록 만들고 싶다  

우선 추가하고싶은 템플릿을 열어보자   
나는 videoController.js 파일을 열어보았다
```js
export const home = (req, res) => res.render("home", { pageTitle: "Home"});
```
첫 번째 인자만 적혀있던 함수에 두 번째 인자를 추가해주었다  
첫 번째 인자는 템플릿이고, **두 번째 인자는 템플릿에 추가할 정보가 담긴 객체**이다  
**{ } 안에** pageTitle **변수를 추가**해주었다  
이제 이 pageTitle은 home 템플릿으로 잘 전달됐을 것이다  
home 템플릿은 layouts/main을 extend하고 있다  
그럼 main.pug 파일을 다시 열어보자  

```
doctype html
html
    head
        <script src="https://kit.fontawesome.com/a83f597bce.js" crossorigin="anonymous"></script>
        title #{pageTitle} | #{siteName}
    body
        include ../partials/header
        main
            block content
        include ../partials/footer
```
title 을 #{pageTitle} | #{siteName} 로 적어주었다  
그럼 <a>http://localhost:4000/home</a>을 열었을 때  
home 템플릿에서 선언해준 pageTitle "home"과  
locals siteName "My Project"가 잘 적용되어,  
**_home | My Project_** 가 title로 잘 뜨는 것을 확인할 수 있다  
이렇게 다른 템플릿들에도 같은 작업을 할 수 있다  

이렇게 변수를 템플릿에 전달하는 방법을 알아보았다  
전달하고 싶은 건 무엇이든 전달할 수 있다!  