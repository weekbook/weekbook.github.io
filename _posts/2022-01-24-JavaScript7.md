---
layout: single
title:  "Java Script(값으로서 함수와 콜백 / 클로저)"
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

### 클로저

+ 클로저(closure)는 내부함수가 외부함수의 맥락에 접근할 수 있는 것을 가르킨다. 

#### 내부함수

```javascript
        function outter() {
            function inner() {
                var title = 'coding everybody';
                alert(title);
            }
            inner();
        }
        outter();
```

자바스크립트는 함수 안에서 또 다른 함수를 선언할 수 있다.

함수 outter의 내부에는 함수 inner가 정의 되어 있다. 함수 inner를 내부 함수라고 한다.

```javascript
        function outter() {
            var title = 'coding everybody';
            function inner() {
                alert(title);
            }
            inner();
        }
        outter();
```

위 예제는 내부함수에서 title을 호출했을때 외부함수의 지역변수에 접근할 수 있음을 보여줌

#### 클로저

내부함수는 외부함수의 지역변수에 접근 할 수 있는데 외부함수의 실행이 끝나고 외부함수가 소멸된 이후에도 내부함수가 외부함수의 변수에 접근할 수 있다. 이러한 매커니즘을 클로저라고한다.

```javascript
        function outter(){
            var title = 'coding everybody';
            return function(){
                alert(title);
            }
        }
        inner = outter();
        inner();
```

위 예제를 실행하면 정상적으로 coding everybody가 뜨게된다.

inner = outter(); 부분에서 outter함수가 종료되어 죽었는데도 사용이 가능하다.

즉, 외부함수가 종료된 이후에도 내부함수를 통해서 접근할 수 있다.

#### private vatiable

```javascript

        function factory_movie(title){
            return{
                get_title : function(){
                    return title;
                },
                set_title : function(_title){
                    if(typeof _title === 'String'){
                        title = _title
                    }else{
                        alert('제목은 문자열이어야 합니다.')
                    }
                }
            }
        }
        ghost = factory_movie('Ghost in the shell');
        matrix = factory_movie('Matrix');
        alert(ghost.get_title());
        alert(matrix.get_title());
        ghost.set_title('1')

        alert(ghost.get_title());
        alert(matrix.get_title());
```

만약 변수가 누구나 수정이 가능하고, 변경할 수 있다면 소프트웨어에 결함이 생길 확률이 높다.

위 예제는 외부 함수인 factory_movie, 내부 함수 get_title / set_title이 존재한다.

ghost, matrix 변수는 각각에 내부함수들의 기능들이 들어가있고 외부함수는 종료되었다.

get_title함수로 외부함수의 인자로 받은 title값을 반환한다

set_title은 인자를 하나 받아서 그 인자가 문자열인지 확인 후 기존 title변수를 변화시킨다.

여기서 변화시킬때 ghost와 matrix는 각각 따로이기때문에 결과가 동일하지는 않다.

#### 클로저의 응용

```javascript
        var arr=[]
        for(var i = 0; i < 5; i++){
            arr[i] = function(id){
                return function(){
                    return id;
                }
            }(i);
        }
        for(var index in arr){
            console.log(arr[index]());
        }
```

for문 내부 함수를 마지막에 (i)변수를 넣어 줌으로써 function(id)의 id값으로 넣어준다.

다시 function(id) 함수의 내부함수인 function() 에서 id값을 그냥 return하기 때문에 제일 안의 내부함수 값은 id값을 그대로 갖는 것이며, 상위 함수는 내부함수가 뱉어낸 id값을 다시 return해준다. 그러면 function(id)함수는 그냥 i값으 id값으로 해서 값의 형태로 결과를 내어주기때문에 결국 i=0일때 arr[0] = 0; 이라는 결과가 된다.
