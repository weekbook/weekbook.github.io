---
layout: single
title:  "Java Script 기초 - 2"
categories: Java Script
tag: [foundation, JavaScript]
toc: true
author_profile: false
sidebar:
    nav: "docs"
typora-root-url: ../
---

# Java Script

### 선언

+ var : 변수를 선언. 추가로 동시에 값을 초기화
+ let : 블록 범위(scope) 지역 변수를 선언. 추가로 동시에 값을 초기화
+ const : 블록 범위 읽기 전용 상수를 선언

### 변수 할당

지정된 초기값 없이 var 혹은 let 문을 사용해서 선언된 변수는 undefined 값을 갖는다.

선언되지 않은 변수에 접근을 시고하는 경우 ReferenceError 예외가 발생한다.

```javascript
var a;
console.log("a 값은 " + a); // "a 값은 undefined"로 로그가 남음.

console.log('b 값은 ' + b); // b 값은 undefined
var b;

console.log("c 값은 " + c); // ReferenceError 예외 던짐

let x;
console.log('x 값은 ' + x); // x 값은 undefined

console.log('y 값은 ' + y); // ReferenceError 예외 던짐
let y;
```

undefined 값은 수치 문액에서 사용될 때 NaN으로 변환된다.

```javascript
var a;
a + 2; // NaN으로 평가
```

null 값을 평가할 때, 수치 문맥에서는 0으로, boolean 문맥에서는 false로 동작한다.

```javascript
var n = null;
console.log(n * 32); // 콘솔에 0 으로 로그가 남음.
```

### 조건문을 이용한 간단한 로그인 예제

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>자바스크립트 테스트</title>
</head>
<body>
    <script>
        var id = prompt('아이디를 입력해주세요');
        var password = prompt('비밀번호를 입력해주세요');
        if((id=='weekbook' || 'gugucon' || 'strawberry') && password=='111111'){
            alert('로그인 하셨습니다. ' + id + '님 반갑습니다.');
        }else{
            alert('아이디가 일치하지 않습니다.');
        }
    </script>
</body>
</html>
```

### false로 간주되는 데이터 형

```javascript
if(!''){
        alert('빈 문자열');
}
if(!undefined){
        alert('undefined');
}
```

빈문자열과 undefined는 false로 간주한다.

### 반복문

while이용

```html
var i = 0;
while(i<10){
             document.write("Coding everybody" +i+ "<br>");
             i = i + 1;
             }
```

for이용

```html
var i = 0;
for(var i = 0; i < 10; i++){
                      document.write("Coding everybody" +i+ "<br>");
                      }
```

