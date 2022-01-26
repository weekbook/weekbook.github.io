---
layout: single
title:  "Java Script(값으로서 함수와 콜백)"
categories: Java Script
tag: [foundation, JavaScript]
toc: true
author_profile: false
sidebar:
    nav: "docs"
typora-root-url: ../
---

# 함수와 콜백

### 값으로서의 함수

JavaScript에서 함수도 객체다. 다시 말해서 일종의 값이다. 다른 언어의 함수와 다른 점은 값이 될 수 있다는 점이다.

```javascript
function a() {} // var a = function() {}
```

위에 예제에서 함수 a는 변수 a에 담겨진 값이다. 또한 함수는 객체의 값으로 포함될 수 있다.

이렇게 객체의 속성 값으로 담겨진 함수를 메소드(method)라고 부른다.

```javascript
a = {
    b : function() { // 메소드 b
    }
};
```

```javascript
function cal(func, num){
    return func(num)
}
function increase(num){
    return num + 1
}
function decrease(num){
    return num-1
}
alert(cal(increase, 1));
alert(cal(decrease, 1));
```

함수는 값이기 때문에 다른 함수의 인자로 전달 될수도 있다. 위 예제가 그런 예이다.

alert(cal(increase, 1)); 을 실행하면 함수 increase와 값 1이 함수 cal의 인자로 전달된다.

```javascript
        function cal(mode){
            var funcs = {
                'plus' : function(left, right) {return left + right},
                'minus' : function(left, right) {return left - right}
            }
            return funcs[mode];
        }
        alert(cal('plus')(2,1));
        alert(cal('minus')(2,1));
```

함수는 함수의 리턴 값으로도 사용할 수 있다.

cal(mode) 안에 각각 plus와 minus를 인수로 주게되면, cal함수는 반환값으로 funcs 객체를 반환하고 인수로온 plus와 minus가 들어가서 funcs[plus / minus]가 되고, 각 함수를 실행한다

funcs[plus] (2,1) -> left는 2 right는 1 -> 2 + 1 = 3

funcs[minus] (2,1) -> left는 2 right는 1 -> 2 - 1 = 1

```javascript
        var process = [
            function(input) {return input + 10;},
            function(input) {return input * input;},
            function(input) {return input / 2;}
        ];
        var input = 1;
        for(var i=0; i < process.length; i++){
            input = process[i](input);
        }
        alert(input);
```

당연히 배열의 값으로도 사용할 수 있다.

i가 0,1,2로 커지면서 process의 함수 3개도 차례대로 작동한다.

처음에 input은 1이기 때문에 11 -> 11 * 11= 121 -> 121/1=60.5

+ 변수 매개변수 리턴값의 용도로 사용할 수 있는 데이터를 first-class object라고 한다.

### 콜백 함수

값으로 사용될 수 있는 특성을 이용하면 함수의 인자로 함수를 전달할 수 있다. 값으로 전달된 함수는 호출될 수 있기 때문에 이를 이용하면 함수의 동작을 완전히 바꿀 수 있다.

```javascript
        var numbers = [20,10,9,8,7,6,5,4,3,2,1];
        function sortNumber(a,b){
            return b-a;
        }
        alert(numbers.sort(sortNumber));
```

sort함수의 인자로 콜백함수를 정의하면 졍렬기준을 정할 수 있다.

첫 번째 인수가 두 번째 인수보다 작을 경우 - 값 반환

첫 번째 인수가 두 번째 인수보다 클 경우 + 값 반환

음수는 내림차순 / 양수는 오름차순을 의미한다.

따라서 return b-a 는 오름차순이며, return a-b 는 내림차순이다.

#### 비동기 처리

+ 동기적(Synchronous) : 특정 코드를 수행 완료한 이후 아래줄의 코드 수행
+ 비동기적(Asychronous) : 특정 코드를 수행하는 도중에도 아래로 계속 내려가며 수행

+ Ajax(Asychronous JavaScript And XML)
  + Ajax는 빠르게 동작하는 동적인 웹 페이지를 만들기 위한 개발 기법의 하나

![image-20220127001141738](/images/2022-01-24-JavaScript7/image-20220127001141738.png)

$는 jQuery의 특수한 객체이며, 이 객체가 가지고 있는 메소드중에 get을 사용한다.

첫 번째 인자로 json타입의 데이터의 url을 적어주고, 두 번째 인자는 콜백 함수인데 서버 통신을 통한 데이터가 result 부분에 들어가서 console.log로 출력되게 하는 예제이다.

