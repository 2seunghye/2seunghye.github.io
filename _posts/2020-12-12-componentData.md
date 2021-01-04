---
layout: article
title: Component 간 data 교환
tag: React
---

# 2020-12-12 :: Component 간 data 교환

1. 부모 component에서 callback을 method로 선언한다
2. 이 callback을 자식1 component에게 props로 전달한다
3. 자식 component에서 특정 method안에서 this.props.callback을 실행시켜 자기 자신(자식1 component)의 data에 접근한다
4. 부모component의 method인 callback에서 setState를 실행해서자기 자신(부모component) state에 자식1component의 data를 보관한다
5. 이후 부모component의 다른 method 어디서나 state에 있는자식1component의 data에 접근가능하다
6. 부모component에서 render실행 시, 자식2component를 호출할 때부모component의 state에 보관해둔 자식1component의 data를 전달 가능
