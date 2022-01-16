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

#### return

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

#### 인자

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

#### 함수를 정의하는 또 다른 방법

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

#### 익명함수

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

### 배열

연관된 데이터를 모아서 통으로 관리하기 위해서 사용하는 데이터 타입

```javascript
        var member = ['egoing', 'hello', 'coding']
        alert(member[0])
        alert(member[1])
        alert(member[2])
```

배열 각각의 데이터를 원소(Element)이라고 부르며, 0,1,2는 인덱스이다.

```javascript
        function get_members(){
            return ['egoing', 'hello', 'coding'];
        }
        var members = get_members();
        document.write(members[0])
        document.write(members[1])
        document.write(members[2])
```

기존에는 함수를 통해 하나의 값만 리턴을 했다면, 위 예제는 배열을 통해 하나의 함수를 이용하여 여러개의 정보를 반환할 수 있다.

#### 배열의 사용

```javascript
        for(var i = 0; i < members.length; i++){
            document.write(members[i] + "<br>")
        }
```

length를 사용하여 members 배열의 길이를 알 수 있다. members 변수의 길이가 3이므로

0, 1, 2 즉 3번 반복하며 배열의 모든 원소값을 출력한다.

#### 추가

```javascript
        var li = ['a','b','c','d','e'];
        li.push('f');
        alert(li);
```

배열의 끝에 원소를 추가하는 방법이다. push는 인자로 전달된 값을 배열에 추가하는 명령이다.

```javascript
        var li = ['a','b','c','d','e'];
        li = li.concat(['f','g']);
        alert(li);
```

복소의 원소를 배열에 추가하는 방법이다. concat은 인자로 전달된 값을 추가하는 명령이다.

```javascript
        var li = ['a','b','c','d','e'];
        li.unshift('z');
        alert(li);
```

배열의 시작점에 원소를 추가하는 방법이다. unshift는 인자로 전달한 값을 배열의 첫번째 원소로 추가하고 배열의 기존 값들의 색인을 1씩 증가시킨다.

#### splice

```javascript
        var li = ['a','b','c','d','e'];
        li.splice(2,0,'B');
        alert(li);
```

splice는 첫번째 인자에 해당하는 원소부터 두번째 인자에 해당하는 원소의 숫자만큼의 값을 배열로부터 제거한 후에 리턴한다. 그리고 세번째 인자부터 전달된 인자들을 첫번째 인자의 원소 뒤에 추가한다.

![image-20220117001346087](/images/2022-01-15-JavaScript3/image-20220117001346087.png)

인자

- index : 배열에 추가할 특정 배열의 위치를 가르키는 index
- howmany : index에서부터 제거될 원소들의 수. index부터 index+howmany에 해당하는 원소들은 삭제된다. 이 값이 0이면 어떠한 원소도 삭제되지 않는다.
- element1,..,elementN : index와 index+howmany 사이에 추가될 값

```javascript
        var li = ['a','b','c','d','e'];
        alert(li.splice(3));
        alert(li);
```

![image-20220117001956367](/images/2022-01-15-JavaScript3/image-20220117001956367.png)

![image-20220117002004408](/images/2022-01-15-JavaScript3/image-20220117002004408.png)

splice를 통해 삭제된 값은 반환된다. 

#### 제거

```javascript
        var num = [1,2,3,4,5,6,7,8,9,10];
        num.shift();
        alert(num);
```

배열의 첫번째 원소를 제거하는 방법이다. shift를 사용하여 1이 제거된다.

```javascript
        var num = [1,2,3,4,5,6,7,8,9,10];
        num.pop();
        alert(num);
```

배열의 마지막 원소를 제거하는 방법이다. pop을 사용하여 10이 제거된다.

#### 정렬

```javascript
        var num = ['c','e','a','b','d'];
        num.sort();
        alert(num);
```

배열의 정렬방법이다. sort를 사용하면 a, b, c, d, e로 정렬된다.

```javascript
        var num = ['c','e','a','b','d'];
        num.reverse();
        alert(num);
```

reverse를 사용하면 역순으로 정렬된다.

![image-20220117003035390](/images/2022-01-15-JavaScript3/image-20220117003035390.png)

숫자의 경우 암시적으로 문자열로 형변환을 하기 때문에 숫자1이 숫자 10보다 먼저 나온다.

sort(sortfunc)는 sortfunc부분에 정렬기준을 직접 정의할 수 있다.
