---
layout: article
title: Express Core - Middlewares (2)
tag: NodeJS
---

### Morgan

이번엔 Morgan이라는 middleware를 설치해보자  
Morgan은 **logging(로깅)에 도움을 주는 middleware**이다  
logging이란 <u>무슨 일이 어디서 일어났는지를 기록하는 것</u>을 말한다  
`npm install morgan` 이라고 입력하면 설치는 끝난다  

index.js를 열어 morgan을 import해보자  
```js
import morgan from "morgan";

app.use(morgan(""))
```
이렇게 morgan을 import하고,  
*app.use(morgan(""))*을 입력해주면  
morgan을 사용할 준비는 완료가 됐다  
morgan은 몇 가지 로깅 옵션 인자를 가질 수 있는데  
하나씩 살펴보도록 하자  

```js
app.use(morgan("tiny"));
```
**tiny**를 입력하면  
내가 페이지를 새로고침 할 때마다  
`GET / 304 - - 0.159 ms` 이런 값들이 콘솔에 뜨는 것을 볼 수 있다  
tiny는 최소화된 로그를 출력하는 인자로,    
`:method :url :status :res[content-length] - :response-time ms` 형태로 나타난다  

```js
app.use(morgan("combined"));
```
**combined**는 표준 Apache combined 로그를 출력한다    
`remote-addr - :remote-user [:date[clf]] ":method :url HTTP/:http-version" :status` 형태로 나타난다  
어떤 종류의 접속인지, 어떤 브라우저인지 등등을 꽤 길게 보여준다    

```js
app.use(morgan("common"));
``` 
**common**은 표준 Apache common 로그를 출력한다  
`:remote-addr - :remote-user [:date[clf]] ":method :url HTTP/:http-version" :status :res`  
형태로 나타난다  
 
```js
app.use(morgan("dev"));
```
내가 사용할 dev 인자   
**dev**는 개발용을 위해 response에 따라 색상이 입혀진 축약된 로그를 출력한다  
`:method :url :status :response-time ms - :res[content-length]` 형태로 나타난다    
:status값이 빨간색이면 서버 에러코드,   
노란색이면 클라이언트 에러 코드,  
청록색은 리다이렉션 코드, 그외 코드는 컬러가 없다    

### Helmet

우리가 또 사용해 볼 middleware는 helmet이라는 것이다    
helmet은 **node.js 앱의 보안에 도움이 되는 것**이다  
`npm install helmet`을 입력하면 설치 끝!  

```js
import helmet from "helmet";

app.use("helmet");
```
morgan과 같이 helmet을 import하고 use해주면 완료!  
helmet을 이용하면 http헤더를 적절히 설정하여  
몇 가지 잘 알려진 웹 취약성으로부터 앱을 보호할 수 있다    
보안을 위해 helmet을 꼭 설치하는 버릇을 들이도록 하자  

### coocie/body parser
마지막으로 다뤄볼 middleware는  
body parser와 cookie parser이다  
둘 다 express의 middleware인데,  
cookie와 body 다루는 것을 도와준다  

기본적으로 누군가 form을 채워 나에게 전송한다면  
이 form은 서버에 의해서 받아져야만 한다  
만약 누군가가 이름과 비밀번호를 입력하여 전송하면  
특정한 형태로 서버에 의해 받아져야만 한다는 것이다  
form을 받았을 때, 그 데이터를 갖고 있는  
request object에 접근할 수 있어야 하는데  
이걸 위해 **body parser**가 필요하다  
즉, **body로부터 정보를 얻을 수 있게 해주는 것**  

그리고 우리는 session을 다루기 위해  
**cookie에 유저 정보를 저장**하게 되는데   
이를 위해 필요한 것이 바로 **cookie parser**인 것이다  

`npm install body-parser`와  
`npm install cookie-parser`를 입력하여 설치를 해주자 

```js
import cookieParser from "cookie-parser";
import bodyParser from "body-parser";

app use(cookieParser());
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }))
```

지금껏 해왔던 것 같이 import 한 후, use해주면 끝  
이 때, body-parser에는 우리가 정의해야 할 옵션이 있다  
json이란 옵션이 있고, urlencoded란 옵션 등이 있다  
이것을 설정해주는 이유는 **서버가 무엇을 전송하는지 알 수 있어야 하기 때문**이다  

예를 들어 만약 json을 전송한다면,  
서버는 json을 이해하길 바래야한다  
우리가 일반적인 html form을 전송한다면  
서버가 urlencoded라는 것을 이해하길 바래야 한다  
이게 서버가 유저로부터 받은 데이터를 이해하는 방법이다  

지금 당장은 이해가 안될 수 있지만,  
우리가 만들고 사용하다보면  
어떤 영향을 주고 어떻게 도움을 주는 지 알 수 있을 것이다  


이 외에도 아주 많은 middleware들이 존재한다    
시작하기에 이정도 middleware면 충분하다  
앞으로 필요할 때마다 middleware를 추가하도록 하자  