---
layout: article
title: CSS Seletors
tag: CSS
---

# Type, Class & ID Selector

## Type Selector

타입 선택자(Type Selector)는 h1, p, a, div 등 HTML 요소를 선택하는 선택자이다

### 예시 1)
```html
<h5>Type Selector</h5>
<p>
    Lorem ipsum dolor sit amet consectetur adipisicing elit. 
    Amet quisquam suscipit molestias rerum repudiandae laudantium 
    ipsa veritatis. Esse, dignissimos fugit.
</p>
```

```css
h5 {
    font-size: 30px;
    color: #ffc82c;
}

p {
    color: #0066ff;
}
```

<style>
    #h5 {
        color:#ffc82c;
        font-size: 30px;
    }
    #p {
        color:#0066ff;
    }
</style>
<h5 id="h5">Type Selector</h5> 
<p id="p">
    Lorem ipsum dolor sit amet consectetur adipisicing elit. Amet quisquam suscipit molestias rerum repudiandae laudantium ipsa veritatis. Esse, dignissimos fugit.
</p>

### 예시 2)

```html
<p>
    Hello
    <strong>
        Seunghye!
    </strong>
</p>
```
```css
strong {
    color: #ffc82c;
}
```

<p>
    Hello
    <strong style="color:#ffc82c">
        Seunghye!
    </strong>
</p>

### 예시 3)

```html
<h6>Hello!</h6>
<p>
    Lorem ipsum dolor sit amet consectetur adipisicing elit. Rem eligendi dignissimos, ad voluptate est aperiam cum minus doloribus hic velit laudantium cupiditate sapiente eveniet dolores tenetur impedit, non voluptatum maxime accusamus sint pariatur minima commodi! Quia est, omnis vitae nihil a numquam adipisci, recusandae similique quasi quis obcaecati neque nobis.
</p>
```
```css
h6, p {
    color: #fa5858;
}
```

<h6 style="color:#fa5858; font-size:30px">Hello!</h6>
<p style="color:#fa5858">
Lorem ipsum dolor sit amet consectetur adipisicing elit. Rem eligendi dignissimos, ad voluptate est aperiam cum minus doloribus hic velit laudantium cupiditate sapiente eveniet dolores tenetur impedit, non voluptatum maxime accusamus sint pariatur minima commodi! Quia est, omnis vitae nihil a numquam adipisci, recusandae similique quasi quis obcaecati neque nobis.
</p>

⭐️ 위와 같이 쉼표를 사용해 <br>
복수의 셀렉터를 연속하여 지정할 수 있다

## Class Selector

Class Selector는 어트리뷰트 값을 지정하여 일치하는 요소를 선택한다  
이 때, class 어트리뷰트 값은 중복될 수 있다  
클래스 셀렉터에 스타일을 적용할 때는 class 값 앞에 .(마침표)를 찍어준다  
ex) .box

```html
<div class="box">
    <!--  -->
</div>
<div class="box">
    <!--  -->
</div>
<div class="box">
    <!--  -->
</div>
```
```css
.box {
    color: red;
}
```
가령 세 개의 div박스에 동일한 스타일을 적용하고 싶을 때,  
동일한 클래스를 선언하면 3개의 div에 동일하게 스타일을 적용할 수 있다  
여러 개의 스타일 요소를 동시에 적용할 수 있기 때문에
class는 아주 중요하고 유용한 요소이다

```html
<div class="box-0 box-1 box2">
    <!--  -->
</div>
```
클래스명은 동시에 여러개를 가질 수 있다  
반드시 스페이스로 간격을 주어야 한다  
위와 같은 경우 div의 클래스는  
"box-0", "box-1", "box-2" 총 세개가 존재하는 셈이다

```css
.box-0.box-1 {
    color: red;
}

.box-0 .box-1 {
    color: blue;
}
```
여기서 주의할 점이 있다  
위와 같은 경우 .box-0.box-1 과 .box-0 .box-1이 같은 의미일까?  
아니다. 저 둘은 완전히 다른 의미를 가지고 있다  
.box-0.box-1와 같이 클래스명을 공백없이 붙여서 적어줄 경우,  
이것은 ".box-0이자, .box-1"라는 의미로 하나를 의미하는 것이다  
.box-0 .box-1와 같이 클래스명을 공백으로 띄우면,  
.box-0의 하위 요소에서 .box-1를 찾는 셈이 된다

### 예시)

```html
<div class="box-0 box-1 box-2">
    <ul class="box-3">
        <li>
            item 01
        </li>
        <li>
            item 02
        </li>
        <li>    
            item 03
        </li>
    </ul>
</div>
```
```css
.box-0.box-2 {
    /* box-0이자 box-2를 의미 즉, div가 선택된 것 */
}

.box-0 .box-3 {
    /* box-0 하위 요소에 있는 box-3을 의미 즉, ul이 선택된 것*/
}

.box-2 .box-3 {
    /* 위와 같다. box-2 하위 요소에 있는 box-3을 의미 */
}
```

## ID Selector

ID Selector는 id 어트리뷰트 값을 지정하여 일치하는 요소를 선택한다  
id 값을 중복될 수 없는 유일한 값이다
id 값 앞에 #을 붙여 사용한다

### 예시 1)

```html
<div id="apple">
    <!--  -->
</div>
```
```css
#apple {
    font-style: italic;
}
```

### 예시 2)

```html
<div class="box" id="apple">
    <!--  -->
</div>
```
위와 같은 상황에서
id가 apple이자,  
class는 box인 요소를 선택자로 표현하고 싶을 때,

```css
#apple.box {
    /*  */
}

혹은

.box#apple {
    /*  */
}
```
위와 같이 표현할 수 있다  
주의할 점은 반드시 공백 없이 붙여주는 것  
위에서도 보았듯, 공백이 들어가면 다른의미가 되어버리기 때문이다  

# Child, Descendant & Sibling Combinators

이번에는 Child(자식), Descendant(자손) & Sibling Combinators(형제) 셀렉터에 대해 알아보자

```html
<section>
    <h1>
        Hello
    </h1>
    <ul>
        <li>
            <h1>
                list item1
            </h1>
            <p>
                Lorem ipsum dolor sit amet consecteur
            </p>
        </li>
        <li>
            <h1>
                list item2
            </h1>
            <p>
                Lorem ipsum dolor sit amet consecteur
            </p>
        </li>
        <li>
            <h1>
                list item3
            </h1>
            <p>
                Lorem ipsum dolor sit amet consecteur
            </p>
        </li>
    </ul>
</section>
```
위와 같은 HTML 문서에서,  
section의 자식 요소는 h1과 ul이 된다는 것은 모두 짐작하는 내용일 것이다  
그럼 ul 안의 li는 section의 자식 요소가 될 수 있을까?  
li는 ul이 낳은 자식 요소로 li는 section의 자손이라고 할 수 있다

li의 자식요소는 h1과 p 요소가 있는 것을 볼 수 있는데,  
이 때 li의 자식 h1태그는 section의 자식 h1과는 다른 셈이다  
그리고 li안의 h1과 p 태그는 계층이 같은 형제이다

이것이 자식, 자손, 형제의 개념이다

## Child Selector(자식 선택자)

**parent > child**

Child Selector는 >(꺽쇠)를 사용하여 표현한다  
parent 안의 수많은 자식과 자손이 있는데,  
"parent가 직접적으로 감싸고있는 요소를 선택하겠다"라는 의미가 된다 

```css
section > h1 {
    /*  */
}
```
위와 같이 작성해주면, section 요소의 바로 직계 자식인 h1만 선택이 되는 것이다  
li의 h1태그는 자손이므로 선택이 되지 않음!

## Descendant Selector(자손 선택자)

**parent descendants**

자식 선택자와 달리 꺽쇠(>)를 사용하지 않고 공백( )을 사용해 준다  
만약 저 위의 html 문서에서 
모든 section안의 모든 h1태그를 선택하여 꾸며주고 싶을 때

```css
section h1 {
    /*  */
}
```
이렇게 적어주면 section 요소 하위에 있는 모든 자손(자식) h1태그들이 선택된다

## Sibling Combinators Selector(형제 선택자들)

```html
<section>
    <h1>Menu</h1>
    <ol>
        <li>Menu1</li>
        <li class="active">Menu2</li>
        <li>Menu3</li>
        <li>Menu4</li>
        <li>Menu5</li>
    </ol>
</section>
```

```css
.active {
    font-weight: 700;
}
```

우선 메뉴 리스트를 만들고 Menu2에는 폰트를 굵게 표시해 주었다  
내가 만약 active class를 기준으로  
그 밑의 li 요소들의 색상을 바꾸고 싶다고 할 때

```css
.active ~ li {
    color: red;
}
```
위와 같이 적어주면  
active 클래스를 기준으로 그 밑에 있는 모든 li 형제요소들의 색깔이  
빨간색으로 바뀌는 것을 볼 수 있다

만약 active 바로 다음에 오는  
한 형제요소의 색상만 변경하고 싶은 경우

```css
.active + li {
    color: blue;
}
```
이렇게 작성해주면  
Menu3의 색상만이 파란색으로 바뀌는 것을 볼 수 있다

# Structural Pseudo-classes

Structural Pseudo-classes는 요소의 특수 상태를 정의할 때 사용한다  

## element:first-child

element의 첫번째 요소를 선택한다 

### 예시 )

```html
<section>
    <h1>Menu</h1>
    <ol>
        <li>Menu1</li>
        <li>Menu2</li>
        <li>Menu3</li>
        <li>Menu4</li>
        <li>Menu5</li>
    </ol>
</section>
```
```css
li:first-child {
    color: red;
}
```
<style>
    .first li:first-child {
        color: red;
    }
</style>
 <ol class="first">
    <li>Menu1</li>
    <li>Menu2</li>
    <li>Menu3</li>
    <li>Menu4</li>
    <li>Menu5</li>
</ol>

## element:last-child

element의 마지막 요소를 선택한다

### 예시 )

```html
<section>
    <h1>Menu</h1>
    <ol>
        <li>Menu1</li>
        <li>Menu2</li>
        <li>Menu3</li>
        <li>Menu4</li>
        <li>Menu5</li>
    </ol>
</section>
```
```css
li:last-child {
    color: red;
}
```
<style>
    .last li:last-child {
        color: red;
    }
</style>
 <ol class="last">
    <li>Menu1</li>
    <li>Menu2</li>
    <li>Menu3</li>
    <li>Menu4</li>
    <li>Menu5</li>
</ol>

## element:nth-child(n)

### 예시 1)

```html
<section>
    <h1>Menu</h1>
    <ol>
        <li>Menu1</li>
        <li>Menu2</li>
        <li>Menu3</li>
        <li>Menu4</li>
        <li>Menu5</li>
    </ol>
</section>
```
```css
li:nth-child(3) {
    color: red;
}
```
<style>
    .nth li:nth-child(3) {
        color: red;
    }
</style>
 <ol class="nth">
    <li>Menu1</li>
    <li>Menu2</li>
    <li>Menu3</li>
    <li>Menu4</li>
    <li>Menu5</li>
</ol>

### 예시 2)

```html
<section>
    <h1>Menu</h1>
    <ol>
        <li>Menu1</li>
        <li>Menu2</li>
        <li>Menu3</li>
        <li>Menu4</li>
        <li>Menu5</li>
    </ol>
</section>
```
```css
li:nth-child(2n) {
    color: red;
}
li:nth-child(2n-1) {
    color: blue;
}
```
<style>
    .nth2 li:nth-child(2n) {
        color: red;
    }
    .nth2 li:nth-child(2n-1) {
        color: blue;
    }
</style>
 <ol class="nth2">
    <li>Menu1</li>
    <li>Menu2</li>
    <li>Menu3</li>
    <li>Menu4</li>
    <li>Menu5</li>
</ol>

```css
li:nth-child(2n) {
    color: red;
}
```

위와 같이 짝수는 2n, 홀수는 2n-1로 표현할 수도 있음


# User Action Pseudo-classes

User Action Pseudo-classes는 동적 가상 클래스 선택자이다
어떤 상태나 조건을 만족했을 때 사용할 수 있는 선택자이다

## element:hover

요소에 커서를 올렸을 때 요소를 변경하고 싶은 경우 사용할 수 있다

### 예시 )

```html
<section>
    <a href="#">
        Seunghye Channel
    </a>
</section>
```

```css
a:hover {
    color:#7e5bef;
}
```
<style>
    .hover a {
        color:#333333
    }

    .hover a:hover {
        color:#7e5bef;
    }
</style>
<section class="hover">
    <a href="#">
        Seunghye Channel
    </a>
</section>

a 태그에 마우스를 올리면 색상이 바뀌는 것을 확인할 수 있다


## element:active

어떤 요소가 활성화 되었을 때의 상태를 말한다  
마우스를 사용하는 경우, 보통 마우스 버튼을 누르는 순간부터 떼는 시점까지를 의미한다


### 예시 )

```html
<section>
    <a href="#">
        Seunghye Channel
    </a>
</section>
```

```css
a:hover {
    color:#7e5bef;
}

a:active {
    color:#592dea;
}
```
<style>
    .hover a {
        color:#333333
    }

    .hover a:hover {
        color:#7e5bef;
    }

    .hover a:active {
        color:#592dea;
    }
</style>
<section class="hover">
    <a href="#">
        Seunghye Channel
    </a>
</section>

## element:focus

포커스가 되었을 때 입력 필드를 선택하고 스타일을 지정할 때 사용한다  
즉 input같은 경우, input 필드를 눌러  
무언가를 적을 수 있는 상태를 알리고 싶을 때 focus를 적용한다  

### 예시 )
```html
<section>
    <input type="email" placeholder="이메일을 입력하세요">
</section>
```
```css
input:focus {
    border-color: #1fb6ff;
}
```

<style>
    .focus input:focus {
        border-color: #1fb6ff;
    }
</style>
<section class="focus">
    <input type="email" placeholder="이메일을 입력하세요">
</section>

Form을 작성할 때 이러한 동적 가상 클래스 선택자를 유용하게 쓸 수 있다

# CSS 선택자 우선순위

```css
p {
    color: blue;
}

p {
    color: hotpink;
}
```
CSS에서는 기본적으로 나중에 선언된 녀석이 덮어버리는게 기본 원칙  
위와 같은 경우 p 태그는 hotpink 색상으로 적용된다

선택자에도 우선순위가 존재하는데  
3순위는 Type 선택자,  
2순위는 Class, Pseudo-Class 선택자,  
1순위는 ID 선택자이다

```css
.box p {
    color: blue;
}

p {
    color: hotpink;
}
```

위와 같은 경우에는 .box p 선택자가 p 선택자보다 우선 순위가 되는 것이다

이러한 룰을 깨버리는 강력한 두 가지가 존재하는데,  
첫 번째는 **Inline style**이다
html 파일 내에 스타일을 적용하는 것을 의미한다

```html
<p style="font-size: 32px">
    Hello!
</p>
```
위와 같이 html 문서 내에서 inline style을 적용하면  
CSS파일에서 아무리 p 셀렉터에 값을 주어도
inline style이 우선 적용된다  
이 경우 아무리 ID class를 사용한다하더라도,  
inline style을 이기지는 못한다

그리고 두 번째는 **!important**이다   
이것은 inline style도 이겨버리는 아주 강력한 힘을 가지고 있다

```css
* {
    color: hotpink !important;
}
```
위와 같이 스타일을 선언한 후 옆에 **!important**를 입력하면  
어떠한 스타일도 다 무시하고 !important에 적용된 스타일만을 시행한다

하지만, inline style이나 !important는 피치못할 사정이 아니라면 사용을 지양하는 것이 좋다  
스타일 요소를 작성하다보면 무수히 많은 양이 되어버린다
이와 같은 강제적 요소를 사용하게 되면  
나중에 문제의 원인을 찾는데 시간이 오래 걸리기도 하고,  
수정이 번거로워지는 단점이 있으므로  
아주 중요하고 피치못할 사정이 있을 때만 사용하도록 하자!  