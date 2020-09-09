---
layout: article
title: Before Flex-Box(block, inline, inline-block)
tag: CSS
---

어떤 기술을 배울 때, 이 기술이 어떤 문제점을 해결했는지를 아는 것이 중요하다  
마찬가지로 flex-box를 배우기 전에 우리가 왜 flex-box를 사용해야 하는지,  
그 전에 사용하던 방법은 어떤 문제점이 있는지 짚고 넘어가야 한다  
우리가 이전에 사용하던 inline, block, inline-block에 대해 간단하게 알아보자

## display: block

```html
<div class="box">block 1</div>
<div class="box">block 2</div>
<div class="box">block 3</div>
```

```css
.box {
  display: block;
  background: #0066ff;
  width: 100px;
  height: 100px;
  margin-bottom: 2px;
}
```

<div class="container">
    <div class="block"><span>block 1</span></div>
    <div class="block"><span>block 2</span></div>
    <div class="block"><span>block 3</span></div>
</div>

<style>
    .container {
        width: 400px;
        height: 306px;
        border: 1px solid #333;
    }

    .block {
        position: relative;
        background: #0066ff;
        width: 100px;
        height: 100px;
        margin-bottom: 2px;
        color: #fff;
    }

    span{
        position:absolute;top:50%;left:50%;transform: translate(-50%, -50%)  
    }
</style>

block은 옆에 어떠한 element도 올 수 없는 것이 특징이다  
보다시피 각 box는 margin을 따로 설정해 두지 않았음에도,  
옆으로 큰 margin을 가지고 있는 것을 볼 수 있다  
다시 말해, block 요소는 전후 줄 바꿈이 들어가 다른 요소들을 다른 줄로 밀어내고 혼자 한 줄을 차지한다  
대표적인 block 요소로 `<div>`나 `<p>`, `<h1>`태그 등이 있다  
block 요소 옆에는 어떠한 요소도 올 수 없다는 것이 block의 기본 속성이다

## display: inline

```
<div class="box">inline 1</div>
<div class="box">inline 2</div>
<div class="box">inline 3</div>
```

```
.box {
  display: inline;
  background: #0066ff;
  width: 100px;
  height: 100px;
}
```

<div class="container">
    <div class="inline">inline 1</div>
    <div class="inline">inline 2</div>
    <div class="inline">inline 3</div>
</div>

<style>
    .inline {
        display: inline;
        background: #0066ff;
        width: 100px;
        height: 100px;
        color: #fff;
    }
</style>

inline은 box가 아닌 element이다  
inline element로 `<span>`이나 `<a>`, `<em>`태그 등을 둘 수 있다  
이때 inline 요소의 특징은 **너비와 높이를 가지고 있지 않다**는 것이다  
위의 코드를 보면 알 수 있듯이,  
width와 height를 지정해줬음에도 불구하고,  
너비와 높이는 변하지 않은 것을 볼 수 있다  
inline이라는 말 그대로, 같은 직선에 요소들이 놓여있는 것이다

```
.box {
  display: inline;
  margin-right: 50px;
}
```

<div class="inline-container">
    <div class="inline2">inline 1</div>
    <div class="inline2">inline 2</div>
    <div class="inline2">inline 3</div>
</div>

<style>
    .inline-container {
        width: 330px;
        height: 30px;
        border: 1px solid #333;
    }

    .inline2 {
        display: inline;
        background: #0066ff;
        margin-right: 50px;
        color: #fff;
    }
</style>

margin과 padding 속성은 위, 아래는 적용이 되지 않고 왼쪽, 오른쪽만 적용이 가능하다  
그 이유는? 간단하다  
inline 속성은 한 직선에 놓여있기 때문에 선을 벗어나게 하는 속성(width, height, padding-bottom(top), margin-bottom(top))은 적용할 수 없다  
하지만 위와 같이 선을 벗어나지 않고 직선 안에서 간격을 조절하는 padding-left(right), margin-left(right)는 사용할 수 있다

## display: inline-block

```
<div class="inline-block">inline-block 1</div>
<div class="inline-block">inline-block 2</div>
<div class="inline-block">inline-block 3</div>
```

```
.inline-block {
  display: inline-block;
  width: 100px;
  height: 100px;
}
```

<div class="container">
    <div class="inline-block"><span>inline-block 1</span></div>
    <div class="inline-block"><span>inline-block 2</span></div>
    <div class="inline-block"><span>inline-block 3</span></div>
</div>

<style>
    .inline-block {
        display: inline-block;
        position: relative;
        background: #0066ff;
        color: #fff;
        width: 100px;
        height: 100px;
        margin-bottom: 2px;
    }

    span{
        position:absolute;top:50%;left:50%;transform: translate(-50%, -50%)  
    }
</style>

inline-block은 기본적으로 inline 엘리먼트처럼 전후 줄 바꿈 없이 한 줄에 다른 요소들과 나란히 배치되면서, block 속성을 유지할 수 있게 해준다  
기본적인 inline-block 요소로는 `<button>`이나 `<select>`태그 등이 있다  
inline-block을 사용하면, block이 서로 옆에 있을 수 있다  
하지만, box를 살펴보면 우리가 설정하지 않은 알 수 없는 여백들이 존재한다  
또 다른 문제점을 살펴보자

```
<div class="inline-block">inline-block 1</div>
<div class="inline-block">inline-block 2</div>
<div class="inline-block">inline-block 3</div>
```

```
.inline-block {
  display: inline-block;
  width: 100px;
  height: 100px;
}

.inline-block:nth-child(2) {
  margin-left: 40px;
}

.inline-block:nth-child(3) {
  margin-left: 40px;
}
```

<div class="container">
    <div class="problem"><span>1</span></div>
    <div class="problem"><span>2</span></div>
    <div class="problem"><span>3</span></div>
</div>

<style>
    .problem {
        position: relative;
        display:inline-block;
        background: #0066ff;
        color: #fff;
        width: 100px;
        height: 100px;
    }

    .problem:nth-child(2){
        margin-left: 46.5px;
    }

    .problem:nth-child(3){
        margin-left: 46.5px;
    }

    span{
        position:absolute;top:50%;left:50%;transform: translate(-50%, -50%)  
    }
</style>

우리가 만약 inline-block 아이템들을 적당한 간격으로 띄우기 위해  
margin-left 값을 주었다고 생각해보자  
저 요소를 감싸고 있는 container가 현재 나의 데스크탑이라고 하였을 때,  
각 요소는 일정한 간격을 두고 잘 떨어져 있어 완벽해 보인다  
하지만 핸드폰으로 본다면?  
요소는 그대로 두고, container 박스 사이즈를 조절하여 확인해보자

<div class="phone-container">
    <div class="problem"><span>1</span></div>
    <div class="problem"><span>2</span></div>
    <div class="problem"><span>3</span></div>
</div>

<style>
    .phone-container{
        width: 250px;
        height: 350px;
        border: 1px solid #333;
        color: #fff;
    }
</style>

</style>

이렇게 레이아웃이 다 망가져 버린다  
우리는 모두 다른 screen 크기를 가지고 있기 때문에,  
inline-block으로 레이아웃을 구성하기에는 많은 불편함이 존재한다  
이러한 문제들이 바로 우리가 flex-box를 쓰게 될 이유이다
