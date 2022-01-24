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