---
layout: article
title: useEffect
tag: React
---

**`useEffect`** 라는 Hook 을 사용하여 컴포넌트가 마운트 됐을 때 (처음 나타났을 때), 언마운트 됐을 때 (사라질 때), 그리고 업데이트 될 때 (특정 props가 바뀔 때) 특정 작업을 처리하는 방법을 알아볼 수 있다

- 참조 링크 : [https://rinae.dev/posts/a-complete-guide-to-useeffect-ko](https://rinae.dev/posts/a-complete-guide-to-useeffect-ko)

### 간단한 예시

```jsx
function User({ user }) {
  useEffect(() => {
    console.log('컴포넌트가 화면에 나타남');
    return () => {
      console.log('컴포넌트가 화면에서 사라짐');
    };
  }, []);
```

등록할 때, 마운트할 때 **"컴포넌트가 화면에 나타남"**

삭제할 때 **"컴포넌트가 화면에서 사라짐"**

![https://i.imgur.com/kBFMe8m.png](https://i.imgur.com/kBFMe8m.png)
