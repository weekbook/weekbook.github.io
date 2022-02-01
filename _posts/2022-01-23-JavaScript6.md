---
layout: single
title:  "Java Script(유효범위)"
categories: JavaScript
tag: [foundation, JavaScript]
toc: true
author_profile: false
sidebar:
    nav: "docs"
typora-root-url: ../
---

# 유효범위

### 전역변수, 지역변수

```javascript
		var vscope = 'global';
        function fscope(){
            var vscope = 'local';
            alert(vscope);
        }
        fscope();
```

위 결과로 local이라는 값이 나온다. alert안에 있는 vscope는 제일 가까운 즉, 함수 안에 있는 변수부터 찾기때문에 local이 나온다. 만약 함수 안에 vscope 변수가 없다면 바깥쪽 vscope를 찾게된다.

함수 안에있는 변수를 지역변수(local)이라고 하며, 바깥쪽에있는 변수를 전역변수(global)이라고 한다.

```javascript
    <script>
        var vscope = 'global';
        function fscope(){
            var vscope = 'local';
            var lv = 'local variables';
            alert(lv);
        }
        fscope();
        alert(lv);
    </script>
```

<img src="/images/2022-01-23-JavaScript6/image-20220123225735203.png" alt="image-20220123225735203" style="zoom:67%;" />

위 예제를 실행시키면 lv is not defined라는 에러가 발생한다.

지역변수인 lv는 함수 안쪽에서만 사용할 수 있기 때문에 바깥쪽에서 alert(lv)를 해놓아도 정의되지 않았다고 뜬다.

```javascript
    <script>
        var vscope = 'global';
        function fscope(){
            var vscope = 'local';
        }
        fscope();
        alert(vscope);
    </script>
```

위 예제의 결과로는 global이 나오지만, 함수 안 vscope변수 앞의 var를 제거하면 local이 나온다 왜일까?

var을 붙이면 local지역의 vscope를 변경하는거지만, var을 제거하면 전역변수의 vscope를 변경하는 것이다.

#### 전역변수를 써야하나 지역변수를 써야하나?

프로젝트의 범위가 커지면, 분명히 변수의 이름이 겹칠 경우가 많이 생긴다.

때문에 전역변수를 써야하는 분명한 이유가 있지 않는이상 지역변수로 하는것이 대부분이다.

이와같은 뜻으로 항상 변수에 var를 붙이는것도 이러한 이유이다.  var를 제거하면 전역변수를 변경하게 되기 때문이다.

#### 전역변수의 사용

```javascript
        var MYAPP = {}
        MYAPP.calculator = {
            'left' : null,
            'right' : null
        }
        MYAPP.coordinate = {
            'left' : null,
            'right' : null
        }
        MYAPP.calculator.left = 10;
        MYAPP.calculator.right = 20;
        function sum(){
            return MYAPP.calculator.left + MYAPP.calculator.right;
        }
        document.write(sum());
```

불가피하게 전역변수를 사용해야 하는 경우는 하나의 객체를 전역변수로 만들고 객체의 속성으로 변수를 관리하는 방법을 사용한다.

만약 하나의 전역변수라도 사용하고 싶지 않다면?

```javascript
        (function(){
            var MYAPP = {}
            MYAPP.calculator = {
                'left' : null,
                'right' : null,
                'middle' : null
            }
            MYAPP.coordinate = {
                'left' : null,
                'right' : null
            }
            MYAPP.calculator.left = 10;
            MYAPP.calculator.right = 20;
            MYAPP.calculator.middle = 30;
            function sum(){
                return MYAPP.calculator.left + MYAPP.calculator.right + MYAPP.calculator.middle;
            }
            document.write(sum());
        }())
```

함수를 정의하고 바로 호출하는 익명함수를 사용한다.

#### 다른 언어와의 유효범위 차이점

자바스크립트는 함수에 대한 유효범위만을 제공한다. 많은 언어들이 블록(대체로 {,})에 대한 유효범위를 제공하는 것과 다른점이다. 

```javascript
        for(var i = 0; i < 1; i++){
            var name = 'coding everybody';
        }
        alert (name);
```

자바스크립트로 위 예제를 실행하면 잘 실행이된다.

```java
for(int i = 0; i < 10; i++){
    String name = "egoing";
}
System.out.println(name);
```

하지만 위에 자바로 쓰여지 예제를 실행하면 에러가 발생한다.

즉, 자바스크립트는 함수의 중괄호 안에서 선언된 변수만이 지역변수로 선언된다.

#### 정적 유효범위

자바스크립트는 함수가 선언된 시점에서의 유효범위를 갖는다. 이러한 유효범위의 방식을 정적 유효범위(static scoping) 혹은 렉시컬(lexical scoping) 이라고 한다.

```javascript
        var i = 5; // 전역변수

        function a(){
            var i = 10; // 지역변수
            b();
        }
        function b() {
            document.write(i);
        }
        a();
```

b함수의 document.write(i)에서 i는 함수를 호출한 a함수의 지역변수인 10을 출력할까 아니면 전역변수인 5를 출력할까?  답은 전역변수인 5를 출력한다.

사용될 때가아닌 정의될 때의 시점을 바라본다.
