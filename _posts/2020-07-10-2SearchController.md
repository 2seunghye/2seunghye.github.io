---
layout: article
title: Search Controller
tag: NodeJS
---

## Search Controller

이번에 만들어볼 것은 **search controller**이다  
어떤 기능을 추가하고 싶냐면,  
내가 원하는 키워드를 검색했을 때  
무엇에 대해 검색했는지 알려주는 문구를 띄우고싶다  

예를 들어, 검색창에 'food'라는 단어를 입력하고 서치버튼을 눌렀을 때,  
'food'를 찾는 search 페이지를 띄우고  
동시에 'Searching for: food'라는 문구를 content 상단에 띄우고싶다    
이 기능을 실행하는 controller를 만들어보자    

우선 partials/header 파일을 수정해보자  
column을 하나 더 추가하여 search 폼을 만든다

```html
header.header
    .header_column
    a(href=routes.home)
        i.fab.fa-youtube
    .header_column
        form(action=routes.search method="get")
            input(type="text", placeholder="Search by term...", name="term")
    .header_column
        ul
            li 
                a(href=routes.join) Join
            li 
                a(href=routes.login) Log In 
```

먼저 form 태그를 생성한 후  
**action**값은 search페이지인 **_roues.search_**로 지정하고,  
**method**값은 '**get**'을 준다    
그 다음, 검색할 수 있는 input 태그를 추가한다  

이 때, name값을 정해주지 않으면 input 필드에 값을 입력해도   
search주소 뒤에 '?'가 붙게된다  
name="term"으로 지정해놓으면 'food'를 검색했을 때,  
<a>http://localhost:4000/search?term=food</a>의 형식으로  
검색한 값이 주소창에 잘 뜨게된다  

이제 search 페이지를 수정해보자  
클래서명이 search_header인 div를 추가해  
내가 원하는 "**Searching for: 'term'**" 값이 뜨도록 만든다  

```html
extends layouts/main

block content
    .search_header
        h3 Searching for: #{searchingBy}
```
h3태그를 추가해 "**Searching for: #{searchingBy}**" 라는 텍스트가 뜨도록 해주었다  
아직까지는 검색창에 'food'를 입력해도  
"Searching for: " 까지만 뜨게된다  
아직 searchingBy라는 변수를 설정해주지 않았기 때문이다  

videoController.js 파일을 열어 컨트롤러를 수정해보자  
우선 console.log(req)를 입력한다  
term=food가 req에서 보이는 지 확인하는 작업이다  
새로고침을 해보면 무수히 많은 값들이 뜬다  
여기서 'food'를 찾아보면  
query 안에 'food'가 담겨있는 것을 볼 수 있다

그럼 console.log(req.query)를 실행시켜보자  
console을 확인해 보면, { term: 'food' }가 보인다  
그럼 우리가 검색한 검색어는 req.query.term에 담겨있는 것을 알 수 있다

```js
export const search = (req, res) => {
    const {
        query: { term: searchingBy }
    } = req;
    res.render("search", { pageTitle: "Search", searchingBy });
}
```
`const searchingBy = req.query.term`의 방식은  
ECMAScript, ES6 이전의 코딩 방식이다  
`const {} = req`는 새로운 방식이다  
{  } 안에서 query를 가져온다  
`{query: { term }}`은 req.query.term을 한 것과 같다  
term의 이름을 `{ term: searchingBy }`와 같이 바꿀 수 있다  
이 term의 변수명을 searchingBy로 바꿔주었다  
그럼 searchingBy는 이제 req.query.term과 같아졌다  
그리고 searchingBy 변수정보를 템플릿에 추가해주었다   

이제 home 화면으로 가서, 'food'를 검색해보면  
"Searching for: food"라는 값이 잘 뜬다  
이렇게 search controller 만들기 끝!  