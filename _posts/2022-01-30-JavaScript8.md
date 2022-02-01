---
layout: single
title:  "Java Script(매개변수 / 함수호출방법)"
categories: JavaScript
tag: [foundation, JavaScript]
toc: true
author_profile: false
sidebar:
    nav: "docs"
typora-root-url: ../
---

# arguments / 함수호출

### arguments

함수에는 arguments라는 변수에 담긴 숨겨진 유사 배열이 있다. 이 배열에는 함수를 호출할 때 입력한 인자가 담겨있다.

```javascript
        function sum(){
            var i, _sum = 0;
            for(i=0; i<arguments.length; i++){
                document.write(i+' : '+arguments[i]+'<br>');
                _sum += arguments[i];
            }
            return _sum;
        }
        document.write('result : ' + sum(1,2,3,4));
```

위 예제의 sum함수의 매개변수를 따로 정해놓지 않았음에도 불과하고 함수에 4개의 인자를 넣어서 사용하고있다. 따로 지정하지 않아도 에러가 뜨지않고 허용하기 때문이다.

argument는 자바스크립트가 정해놓은 단어이다. arguments.length를 사용하면 들어온 인자가 몇개인지 알 수 있다. 위 예제대로하면 4이다. 

#### 매개변수의 수

매개변수와 관련된 두가지 수가 있다. 하나는 함수.length, 다른 하나는 arguments.length이다.

함수.length는 함수로 전달된 실제 인자의 수를 의미하고,  arguments.length는 함수에 정의된 인자의 수를 의미한다. 

```javascript
        function one(arg1){
            console.log(
                'one.length', one.length,
                'arguments', arguments.length
            );
        }
        one('val1', 'val2'); // one.length 1 arguments 2
```

### 함수호출(apply)

```javascript
function func(){
}
func();
```

JavaScript는 함수를 호출하는 특별한 방법을 제공한다. 함수를 객체라고 하였는데, 위 예제에서 함수 func는 Function 이라는 객체의 인스턴스다. 따라서 func는 객체 function이 가지고 있는 메소드들을 상속하고 있다.

```javascript
function sum(arg1, arg2){
    return arg1 + arg2;
}
alert(sum.apply(null, [1,2])) // null을 이용한것은 대단히 비효율적
```

함수 sum은 Function 객체의 인스턴스이다. 그렇기 때문에 객체Function의 메소드 apply를 호출 할 수 있다. .apply와 .call은 같은 취지의 함수호출 메소드이다.

2번째 인자에 배열형태로 값을 넣으면 sum(1,2)와 같은 결과가 나온다.

```javascript
        o1 = {val1:1, val2:2, val3:3}
        o2 = {v1:10, v2:50, v3:100, v4:25}
        function sum(){
            var _sum = 0;
            for (name in this){
                _sum += this[name];
            }
            return _sum;
        }
        alert(sum.apply(o1)) // 6
        alert(sum.apply(o2)) // 185
```

apply를 사용하면 객체를 인자로 넣어서 사용 할 수 있다.

sum함수에서 this는 함수선언단계에서는 가리키고있는것이 없지만,

사용하는 부분에서 객체를 인자로 줌으로써 암시적으로 var this = o1 이 된다.

따라서 객체의 인덱스를 차례대로 더하면서 모든 더한값을 띄우게 된다.

```javascript
        function sum(){
            var _sum = 0;
            for (name in this){
                if(typeof this[name] !== 'function'){
                    _sum += this[name];
                }
            }
            return _sum;
        }
        o1 = {val1:1, val2:2, val3:3, sum:sum}
        o2 = {v1:10, v2:50, v3:100, v4:25, sum:sum}
        alert(o1.sum());
        alert(o2.sum());
```

객체.함수명 방법을 사용하여 하는 방법도 가능하지만 객체안에 sum함수를 추가로 넣어줘야하고 타입이 함수인것을 걸러내기위해 sum함수에 추가해줘야하는 부분도있기 때문에 코드가 복잡해진다.
