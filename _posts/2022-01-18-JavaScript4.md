---
layout: single
title:  "Java Script(객체, 모듈, 라이브러리)"
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

#### in 연산자

객체가 가지고 있는 프로퍼티 및 메소드의 존재 여부를 Boolean으로 반환한다.

#### for in문으로 열거하기

```javascript
var grades = {'egoing': 10, 'weekbook': 6, 'hello': 80};
for (key in grades){
    document.write("<li>key : " + key + " value : " + grades[key] + "</li>");
}
```

grades라는 변수의 값들을 하나씩 가져와서 key에 담기고 key변수에는 객체의 값들의 키값이 된다.  body태그에서 ul태그안에 script태그를 넣고 document.write 안에 li태그를 사용하면 보다 깔끔하게 정리된다.

![image-20220123134352986](/images/2022-01-18-JavaScript4/image-20220123134352986.png)

#### 객체에 담을 수 있는것

```javascript
        var grades = {
            'list' : {'egoing' : 10, 'weekbook' : 8, 'himan' : 80},
            'show' : function(){
                alert('Hello world');
            }
        }
        alert(grades['list']['egoing']);
        alert(grades['show']());
```

객체안에 객체를 담을 수도있고, 함수도 담을 수 있다.

```javascript
        var grades = {
            'list' : {'egoing' : 10, 'weekbook' : 8, 'himan' : 80},
            'show' : function(){
                for(var name in this.list){
                    console.log(name, this.list[name]);
                }
            }
        }
        grades.show();
```

this는 함수가 소속되어 있는 객체를 가리킨다. this는 grades를 가리키기때문에 this.list를 사용하면 list객체를 가리킨다는 뜻이다.

![image-20220123140154096](/images/2022-01-18-JavaScript4/image-20220123140154096.png)

### 모듈

프로그램은 작고 단순한 것에서 크고 복잡한 것으로 진화한다. 그 과정에서 코드의 재활용성을 높이고, 유지보수를 쉽게 할 수 있는 다양한 기법이 사용된다. 그 중 하나가  코드를 여러개의 파일로 분리하는 것이다. 

+ 자주 사용되는 코드를 별도의 파일로 만들어서 필요할 때마다 재활용
+ 코드를 개선하면 이를 사용하고 있는 모든 애플리케이션의 동작이 개선
+ 코드 수정 시에 필요한 로직을 빠르기 찾음
+ 필요한 로직만을 로드해서 메모리의 낭비 줄임
+ 한번 다운로드된 모듈은 웹브라우저에 의해서 저장되기 때문에 동일한 로직을 로드 할 때 시간과 네트워크 트래픽을 절약(브라우저만 해당)

```javascript
<head>
    <script src="greeting.js"></script>
</head>
```

greeting.js라는 다른 파일을 읽어들여서 그 파일 안에 있는 내용을 현재 파일에 가져올 수 있다

### 라이브러리

모듈이 프로그램을 구성하는 작은 부품으로서의 로직을 의미한다면, 라이브러리는 자주 사용되는 로직을 재사용하기 편리하도록 잘 정리한 일련의 코드들의 집합을 의미한다.

jQuery라는 라이브러리를 사용하여 수 많은 기능을 사용할 수 있다.

jQuery를 사용하는 여러 방법이 있지만, 그중에 코드를 복사해서 붙여넣는 방식을 이용하였다

![image-20220123152557253](/images/2022-01-18-JavaScript4/image-20220123152557253.png)

```javascript
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script src="jquery.js"></script>
</head>
<body>
        <ul id="list">
            <li>empty</li>
            <li>empty</li>
            <li>empty</li>
            <li>empty</li>
        </ul>
        <input type="button" value="execute" id="execute_btn">
        <script>
            $('#execute_btn').click(function(){
                $('#list li').text('coding everybody');
            }) 
        </script>
</body>
</html>
```

<img src="/images/2022-01-18-JavaScript4/image-20220123152833916.png" alt="image-20220123152833916" style="zoom: 67%;" />

<img src="/images/2022-01-18-JavaScript4/image-20220123152839893.png" alt="image-20220123152839893" style="zoom:50%;" />

버튼을 누르면 글자 내용이 바뀌는 예제이다.

.click 이벤트 함수와 .text로 글자를 바꾸는 함수를 사용한것이다.