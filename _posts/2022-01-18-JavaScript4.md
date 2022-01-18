---
layout: single
title:  "Java Script 기초 - 4"
categories: Java Script
tag: [foundation, JavaScript]
toc: true
author_profile: false
sidebar:
    nav: "docs"
typora-root-url: ../
---

# Java Script

### 객체

```javascript
var grades = {'egoing': 10, 'weekbook': 6, 'hello': 80};
alert(grades['weekbook']);
```

변수명과 중괄호로 객체를 생성한다 weekbook 이라는 key와 6이라는 value 값이다.

```javascript
var grades = new Object();
grades['egoing'] = 10;
grades['weekbook'] = 6;
grades['hello'] = 80;
```

위와 같은 방법으로도 객체를 만들수도 있다.

#### 객체의 속성 접근

```javascript
alert(grades['hello']);
alert(grades.hello);
```

대괄호로 하는것보다 점으로 접근하는것이 더 쉽다

```javascript
grades['week'+'book']
grades.'week'+'book'
```

이렇게 문자열을 결합하여 나타낼경우 대괄호는 잘 작동되지만 점으로하면 Unexpected string이라는 오류가 발생한다.