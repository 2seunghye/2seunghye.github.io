---
layout: article
title: JavaScript Testing
tag: TDD
---

## 작업환경 설정

- 새로운 디렉터리 안에서 `npm init -y` 입력
- 그 안에서 `npm i --save jest` jest 설치
- Jest ⇒ 페이스북팀에서 Jasmine 기반으로만든 테스팅 프레임워크

### sum.js

```jsx
function sum(a, b) {
  return a + b;
}

module.exports = sum;
```

간단한 덧셈함수를 만들고, `module.exports = sum;` 으로 내보낸다

### sum.test.js

```jsx
const sum = require('./sum');

test('1 + 2 = 3', () => {
  expect(sum(1, 2)).toBe(3);
});
```

여기서 `test` 함수는 새로운 테스트 케이스를 만드는 함수

`expect` 는 값이 ~일 것이다 라고 사전에 정의를 하고,

통과를 하면 테스트 성공 통과를 하지 않으면 테스트를 실패시킴

`toBe` 는 matchers라고 부르는 함수

특정 값이 어떤 조건을 만족하는지, 어떤 함수가 실행됐는지, 에러가 났는지 등을 확인할 수 있게 해줌

위의 toBe는 특정 값이 우리가 정한 값과 일치하는지 확인해줌

### package.json

```jsx
{
  ...
  "scripts": {
    "test": "jest --watchAll --verbose"
  }
}
```

package.json에 `scripts` 를 다음과 같이 추가

`npm test` 를 실행해보자

![2020-12-23%20%E1%84%8C%E1%85%A1%E1%84%87%E1%85%A1%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%B8%E1%84%90%E1%85%B3%20%E1%84%90%E1%85%A6%E1%84%89%E1%85%B3%E1%84%90%E1%85%B5%E1%86%BC%201cdc497a83ac49a1a6c6adf16032d508/Untitled.png](2020-12-23%20%E1%84%8C%E1%85%A1%E1%84%87%E1%85%A1%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%B8%E1%84%90%E1%85%B3%20%E1%84%90%E1%85%A6%E1%84%89%E1%85%B3%E1%84%90%E1%85%B5%E1%86%BC%201cdc497a83ac49a1a6c6adf16032d508/Untitled.png)

test가 pass된 것을 확인할 수 있다

### sum.js

```jsx
function sum(a, b) {
  return a - b;
}

module.exports = sum;
```

a + b 를 a - b 로 수정한 후 test를 돌려보자

![2020-12-23%20%E1%84%8C%E1%85%A1%E1%84%87%E1%85%A1%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%B8%E1%84%90%E1%85%B3%20%E1%84%90%E1%85%A6%E1%84%89%E1%85%B3%E1%84%90%E1%85%B5%E1%86%BC%201cdc497a83ac49a1a6c6adf16032d508/Untitled%201.png](2020-12-23%20%E1%84%8C%E1%85%A1%E1%84%87%E1%85%A1%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%B8%E1%84%90%E1%85%B3%20%E1%84%90%E1%85%A6%E1%84%89%E1%85%B3%E1%84%90%E1%85%B5%E1%86%BC%201cdc497a83ac49a1a6c6adf16032d508/Untitled%201.png)

기대하는 값은 3인데 받은 값은 -1로 오류가 난 것을 볼 수 있다

## test ⇒ it

### sum.test.js

```jsx
const sum = require('./sum');

it('calculates 1 + 2', () => {
  expect(sum(1, 2)).toBe(3);
});

it('1 + 2 잘 더해진다', () => {
  expect(sum(1, 2)).toBe(3);
});
```

우리는 `test` 라는 키워드 대신 `it` 을 사용할 수 있다

작동방식은 완전히 똑같지만, `it` 을 사용하면 "말이 되게" 작성할 수 있음

설명을 영어로 작성해도, 한국어로 작성해도 상관 없음

## describe

### sum.js

```jsx
function sum(a, b) {
  return a + b;
}

function sumOf(numbers) {
  let result = 0;
  numbers.forEach((n) => {
    result += n;
  });
  return result;
}

// 각각 내보내기
exports.sum = sum;
exports.sumOf = sumOf;
```

### sum.test.js

```jsx
const { sum, sumOf } = require('./sum');

describe('sum', () => {
  it('calculates 1 + 2', () => {
    expect(sum(1, 2)).toBe(3);
  });

  it('calculates all numbers', () => {
    const array = [1, 2, 3, 4, 5];
    expect(sumOf(array)).toBe(15);
  });
});
```

![2020-12-23%20%E1%84%8C%E1%85%A1%E1%84%87%E1%85%A1%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%B8%E1%84%90%E1%85%B3%20%E1%84%90%E1%85%A6%E1%84%89%E1%85%B3%E1%84%90%E1%85%B5%E1%86%BC%201cdc497a83ac49a1a6c6adf16032d508/Untitled%202.png](2020-12-23%20%E1%84%8C%E1%85%A1%E1%84%87%E1%85%A1%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%B8%E1%84%90%E1%85%B3%20%E1%84%90%E1%85%A6%E1%84%89%E1%85%B3%E1%84%90%E1%85%B5%E1%86%BC%201cdc497a83ac49a1a6c6adf16032d508/Untitled%202.png)

이렇게 describe로 감싸면, 여러 테스트 케이스가 sum 이라는 이름으로 분류됨
