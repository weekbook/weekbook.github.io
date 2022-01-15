---
layout: single
title:  "Java Script 기초 - 3"
categories: Java Script
tag: [foundation, JavaScript]
toc: true
author_profile: false
sidebar:
    nav: "docs"
typora-root-url: ../
---

# Java Script

### 함수

```javascript
function 함수명([인자...[,인자]]){
    코드
    return 반환값
}
```

자바스크립트는 함수형 언어라고 불릴 정도로 다른 언어에 비해서 함수의 위상이 높다.

+ 재사용성
+ 유지보수 용이
+ 가독성

### return

함수 내에서 사용한 return은 return 뒤에 따라오는 값을 함수의 결과로 반환한다.

그리고 동시에 함수를 종료시킨다.

```javascript
        function get_member1(){
            return 'egoing';
            return 'leezche';
            return 'egoing';
            return 'egoing';
        }
        alert(get_member1());
```

위에 예제를 실행하면 첫 번째 return인 egoing만 alert로 실행되고 함수는 종료된다.

### 인자

```javascript
function get_argument(arg){
    return arg;
}
alert(get_argument(1));
alert(get_argument(2));

function get_argument2(arg1, arg2){
    return arg1 + arg2;
}
alert(get_argument(10, 20));
alert(get_argument(20, 30));
```

괄호 안 arg를 매개변수(parameter) 라고 부르며,

alert안에 있는 함수 괄호 안의 값을 인자(argument) 라고 한다.

### 함수를 정의하는 또 다른 방법

```javascript
function numbering() {
    i=0;
    while(i<10){
        document.write(i);
        i += 1;
    }
}

numbering = function(){
    i=0;
    while(i<10){
        document.write(i);
        i += 1;
    }
```

위와 아래의 함수 정의는 동일한 결과이다.

### 익명함수

```javascript
(function (){
    i=0;
    while(i<10){
        document.write(i);
        i+=1;
    }
})();
```

함수의 정의를 하는 동시에 호출하는 방법이다.
