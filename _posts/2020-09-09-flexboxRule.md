---
layout: article
title: Rules of Flex-box
tag: CSS
---

## first rule of flexbox

가장 먼저 알아야 할 flex-box의 규칙이 있다  
flex-box는 children과 직접 얘기를 하지 않는다  
우리는 지금껏 box의 위치, box의 margin, box의 공간 등을 직접 지정해 주었지만,  
flexbox에서는 이 일을 하지 않아도 된다  
flexbox에서 아이템들을 움직이고 싶을 때, 가장 먼저 해야 하는 것은  
flex container를 만들어주는 것이다

```html
<div class="container">
  <div class="box">1</div>
  <div class="box">2</div>
  <div class="box">3</div>
</div>
```

```css
.container {
  display: flex;
}
```

<div class="flexbox">
    <div class="box"><span class="span">1</span></div>
    <div class="box"><span class="span">2</span></div>
    <div class="box"><span class="span">3</span></div>
</div>

<style>
    .flexbox{
        width: 500px;
        height: 250px;
        border: 1px solid #333;
        color: #fff;
        display:flex;
    }

    .box {
        position: relative;
        background: #f9c00c;
        width: 100px;
        height: 100px;
    }

    .span{
        position:absolute;top:50%;left:50%;transform: translate(-50%, -50%)  
    }
</style>

이렇게 요소들을 감싸는 상자를 하나 만들어 준 후,  
`display: flex;`를 적어주면 바로 inline-block과 같은 결과를 얻을 수 있다

이때 주의해야 할 점은, flex 속성을 사용하기 위해서는  
자식 요소에 바로 붙어있는 부모에 적용해야 한다  
{:.info}

## Main Axis and Cross Axis

flex container의 flex-direction 기본값은 **row(행)**이다  
위에서도 볼 수 있듯이, 3개의 box가 row(가로)로 놓여 있는 것을 볼 수 있다  
이렇게 수평으로 놓인 요소들의 위치를 바꾸는 방법은 아주 간단하다  
position 속성 중 하나인 **justify-content**를 사용하는 것

```html
<div class="flex-container">
  <div class="flex-item"></div>
  <div class="flex-item"></div>
  <div class="flex-item"></div>
</div>
```

```css
.flex-container {
  display: flex;
  justify-content: center;
}
```

<div class="flexbox11">
    <div class="flex-item"></div>
    <div class="flex-item"></div>
    <div class="flex-item"></div>
</div>

<style>
    .flexbox11{
        width: 500px;
        border: 1px solid #333;
        display:flex;
        justify-content: center;
    }

    .flex-item {
        background: #f9c00c;
        width: 100px;
        height: 100px;
    }
</style>

justify-content는 수평축에 있는 flex children의 위치를 변경한다  
justify-content에는 많은 property가 존재한다  
우선 center를 적용해보았더니, 아이템들이 모두 중간에 온 것을 확인할 수 있다  
우리는 어떠한 계산을 할 필요가 없다  
flex를 사용하면 browser가 스스로 계산을 해주기 때문!

```css
.flex-container {
  display: flex;
  justify-content: space-between;
}
```

<div class="flexbox2">
    <div class="flex-item2"></div>
    <div class="flex-item2"></div>
    <div class="flex-item2"></div>
</div>

<style>
    .flexbox2{
        width: 500px;
        border: 1px solid #333;
        display:flex;
        justify-content: space-between;
    }

    .flex-item2 {
        background: #f9c00c;
        width: 100px;
        height: 100px;
    }
</style>

또 다른 property로 space-between를 적용하였더니,  
요소들 사이에 여유 공간을 두고 배치된 것을 확인할 수 있다

```css
.flex-container {
  display: flex;
  justify-content: space-around;
}
```

<div class="flexbox3">
    <div class="flex-item3"></div>
    <div class="flex-item3"></div>
    <div class="flex-item3"></div>
</div>

<style>
    .flexbox3{
        width: 500px;
        border: 1px solid #333;
        display:flex;
        justify-content: space-around;
    }

    .flex-item3 {
        background: #f9c00c;
        width: 100px;
        height: 100px;
    }
</style>

space-around property는 앞, 뒤, 요소들 사이에 일정한 간격을 두고 배치가 된다

여기서 꼭 기억해야 할 것이 있다  
flexbox를 사용할 때 main axis와 cross axis를 항상 염두에 두어야 한다  
flex-direction이 row라면,
main axis는 horizontal axis(수평축)이 된다.  
다시 말해, 기본 방향이 row 면 main axis는 가로가 되는 것이다  
main axis에서는 justify-content를 사용하여 item을 움직일 수 있다

```css
.flex-container {
  display: flex;
  justify-content: space-around;
  align-items: center;
}
```

<div class="flexbox4">
    <div class="flex-item4"></div>
    <div class="flex-item4"></div>
    <div class="flex-item4"></div>
</div>

<style>
    .flexbox4{
        width: 500px;
        height: 300px;
        border: 1px solid #333;
        display:flex;
        justify-content: space-around;
        align-items: center;
    }

    .flex-item4 {
        background: #f9c00c;
        width: 100px;
        height: 100px;
    }
</style>

cross axis는 vertical(세로)가 된다  
우리는 요소들을 가로뿐 아니라 세로로도 배치를 하고 싶다  
그렇듯 cross axis(세로) 기준으로 요소를 움직이고 싶을 때는  
align-items를 사용하면 된다!

이때, 많은 사람들이 마주치는 문제가 있다  
바로 `align-items: center;`를 적용했음에도 불구하고,  
수직 가운데로 가지 않는다는 문제이다  
이 문제는 바로 요소들을 감싸고 있는 flex container에 높이가 지정되어 있지 않기 때문이다  
기본적으로 container에 높이를 지정해 주지 않으면 요소들의 크기만큼 높이가 차지가 된다  
그렇기 때문에 align-items를 사용해도 이동할 공간이 없기 때문에 변동이 없는 것처럼 보인다  
위와 같이 container의 height를 지정해 주면 수직 방향으로도 item들이 배치가 된 것을 확인할 수 있다

align-items는 justify-content property와 다르다  
center property를 확인해 보았으니 stretch property를 적용해보자

```css
.flex-container {
  display: flex;
  justify-content: space-around;
  align-items: stretch;
}
```

<div class="flexbox5">
    <div class="flex-item5"></div>
    <div class="flex-item5"></div>
    <div class="flex-item5"></div>
</div>

<style>
    .flexbox5{
        width: 500px;
        height: 300px;
        border: 1px solid #333;
        display:flex;
        justify-content: space-around;
        align-items: stretch;
    }

    .flex-item5 {
        background: #f9c00c;
        width: 100px;
    }
</style>

`align-items: stretch;`는 전체 높이까지 쭉 뻗어서 채워준다  
이때, box 요소에 height가 지정되어 있으면 적용되지 않는다!  
stretch 속성을 사용하고 싶다면 아이템들의 height 값을 해제해 주자

```css
.flex-container {
  display: flex;
  justify-content: space-around;
  align-items: flex-end;
}
```

<div class="flexbox6">
    <div class="flex-item6"></div>
    <div class="flex-item6"></div>
    <div class="flex-item6"></div>
</div>

<style>
    .flexbox6{
        width: 500px;
        height: 300px;
        border: 1px solid #333;
        display:flex;
        justify-content: space-around;
        align-items: flex-end;
    }

    .flex-item6 {
        background: #f9c00c;
        width: 100px;
        height: 100px;
    }
</style>

`align-items: flex-end;`를 적용하면, item들을 맨 끝에 배치한다  
flex-start는 기본 값이기 때문에 굳이 쓰지 않아도 된다

## Column and Row

이제 `flex-direction: column`에 대해 알아보자

```css
.flex-container {
  display: flex;
  flex-direction: column
  align-items: center;
}
```

<div class="flexbox-column">
    <div class="box-column"></div>
    <div class="box-column"></div>
    <div class="box-column"></div>
</div>

<style>
    .flexbox-column{
        display:flex;
        width: 500px;
        height: 500px;
        border: 1px solid #333;
        flex-direction: column;
        align-items: center;

    }

    .box-column {
        background: #f9c00c;
        width: 100px;
        height: 100px;
    }
</style>

분명 앞에서 가로축으로 아이템을 이동하기 위해서는  
justify-content를 사용해야 한다고 했는데,  
여기서는 align-items를 사용한 것을 볼 수 있다

그 이유는, `flex-direction: column` 일 때는  
main axis가 세로축이 되고, cross axis는 가로축이 되기 때문이다  
이 말은 즉, align-items: center를 적용하였을 때,  
cross axis는 가로축이기 때문에 가로축을 기준으로 중간에 배치된 것이다

```css
.flex-container {
  display: flex;
  flex-direction: column
  align-items: flex-end;
}
```

<div class="flexbox-column2">
    <div class="box-column2"></div>
    <div class="box-column2"></div>
    <div class="box-column2"></div>
</div>

<style>
    .flexbox-column2{
        display:flex;
        width: 500px;
        height: 500px;
        border: 1px solid #333;
        flex-direction: column;
        align-items: flex-end;

    }

    .box-column2 {
        background: #f9c00c;
        width: 100px;
        height: 100px;
    }
</style>

```css
.flex-container {
  display: flex;
  flex-direction: column
  justify-content: center;
}
```

<div class="flexbox-column3">
    <div class="box-column3"></div>
    <div class="box-column3"></div>
    <div class="box-column3"></div>
</div>

<style>
    .flexbox-column3{
        display:flex;
        width: 500px;
        height: 500px;
        border: 1px solid #333;
        flex-direction: column;
        justify-content: center;

    }

    .box-column3 {
        background: #f9c00c;
        width: 100px;
        height: 100px;
    }
</style>

```css
.flex-container {
  display: flex;
  flex-direction: column
  justify-content: space-around;
  align-items: stretch;
}
```

<div class="flexbox-column4">
    <div class="box-column4"></div>
    <div class="box-column4"></div>
    <div class="box-column4"></div>
</div>

<style>
    .flexbox-column4{
        display:flex;
        width: 500px;
        height: 500px;
        border: 1px solid #333;
        flex-direction: column;
        justify-content: space-around;
        align-items: stretch;
    }

    .box-column4 {
        background: #f9c00c;
        height: 100px;
    }
</style>

이게 바로 가장 간단하고 중요한 flexbox의 규칙이다

✨다시 정리  
👉🏻 **flex-direction: row**일 때,  
justify-content >> 가로축  
align-items >> 세로축  
👉🏻 **flex-direction: column**일 때,  
justify-content >> 세로축  
align-items >> 가로축  
{:.info}
