---
layout: single
title:  "Java Script(객체지향프로그래밍 / 생성자와 new / 전역객체)"
categories: Java Script
tag: [foundation, JavaScript]
toc: true
author_profile: false
sidebar:
    nav: "docs"
typora-root-url: ../
---

# 객체 지향 프로그래밍

객체지향 프로그래밍(OOP : Object Oriented Programming)

프로젝트의 규모가 커지고, 진행되는 과정에서 여러가지 어려움을 겪게된다.

그러다 자연스럽게 이 복잡한 로직들을 기능별로 그룹핑을 하고싶다는 생각이드는데,

예를들어 게시글에서 글목록 / 본문 / 댓글 이 있는데 각각의 기능들에 대하여 관련있는 변수나 메소드들을 모아서 그룹핑 하는것이다. 이 그룹핑된 하나하나에 단위들을 객체라고 부른다.

그룹핑한 객체(기능)을 다른 웹페이지에서도 사용 할 수 있을것 같은데? 가 바로 재활용성이다.

+ 객체 지향 프로그래밍 이라고 하는 것은 객체를 만드는 것이고 그 객체라고 하는 것은 추상적이 아닌 문법적인 기능이 언어 차원에서 제공되는 기능이다. 
+ 객체의 취지에 따라 그 취지에 연관되어 있는 변수와 메소드를 그 객체라고 하는 단단한 껍데기 안에다가 가둬둔 것이며, 서로 연관성이 없는 다른 로직과 구분해 주는 역할을 해주는 역할

### 부품화

객체 지향은 부품화의 정점이라고 할 수 있다. 메소드는 부품화의 예라고 할 수 있다.

연관된 메소드와 그 메소드가 사용하는 변수들을 분류하고 그룹핑하는 것이다. 바로 그렇게 그룹핑 한 대상이 객체(Object)다. 비유하자면 파일과 디렉토리가 있을 때 메소드나 변수가 파일이라면 이 파일을 그룹핑하는 디렉토리가 객체라고 할 수 있다. 이를 통해서 더 큰 단위의 부품을 만들 수 있게 되었다.

#### 은닉화, 캡슐화

하지만 단순히 부품화만 하면 그 부품이 어떻게 사용되는지 방법을 알아야 쓸 수 있을 것이다.

예를 들어 모니터가 어떻게 동작하는지 몰라도 연결만하면 사용할 수 있는 이치이다.

즉, 내부의 동작 방법을 안으로 숨기고 사용자에게는 그 부품의 사용방법만 노출 하고 있는것이다.

이러한 컨셉을 정보의 은닉화(Information Hiding), 또는 캡슐화(Encapsulation)라고 부른다.

#### 인터페이스

잘 만들어진 부품이라면 부품과 부품을 서로 교환 할 수 있어야 한다.

예를 들어 모니터를 빼서 다른 컴퓨터에 똑같이 사용할 수 있는 것을 말한다.

각가의 부품은 미리 정해진 약속에 따라서 신호를 입출력하고, 연결점의 모양을 표준에 맞게 만들면 된다. 이러한 연결점을 인터페이스라고 한다.

만약 HDMI 케이블 구멍에 랜선을 꽃으려고 하면 꽃히지 않는다. 인터페이스란 이질적인 것들이 결합하는 것을 막아주는 역할도 하는 것이다.

### 생성자와 new

#### 객체

```javascript
    <script>
        var person = {}
        person.name = 'egoing';
        person.introduce = function(){
            return 'My name is ' + this.name;
        }
        document.write(person.introduce());
    </script>
```

객체 내의 변수를 프로퍼티(property) 함수를 메소드(method)라고 부른다. 

위 예제는 객체를 만드는 과정이 분산되어 있다. 객체를 정의 할 때 값을 셋팅하도록 변경한다.

```javascript
        var person = {
            'name' : 'egoing',
            'introduce' : function(){
                return 'My name is ' + this.name;
            }
        }
        document.write(person.introduce());
```

가독성도 좋고 내용이 변조될 가능성도 적어진다.

#### 생성자

생성자(constructor)는 객체를 만드는 역할을 하는 함수다. 

함수를 호출할 때 new를 붙이면 새로운 객체를 만든 후에 이를 리턴한다.

```javascript
        function Person(name){
            this.name = name;
            this.introduce = function(){
                return 'My name is ' + this.name;
            }
        }
        var p1 = new Person('egoing');
        document.write(p1.introduce()+"<br>");

        var p2 = new Person('leezche');
        document.write(p2.introduce()+"<br>");
```

위 예제는 생성자 내에서 이 객체의 프로퍼티를 정의하고 있다. 이러한 작업을 초기화라고 한다.

이를 통해서 코드의 재사용성이 대폭 높아졌다.

### 전역객체

전역객체(Global object)는 특수한 객체이다. 모든 객체는 이 전역객체의 프로퍼티이다.

```javascript
        var o = {'func' : function(){
            alert('Hello?');
        }}
        o.func();
        window.o.func();
```

위 예제의 o.func() 와 window.o.func()는 같은 결과가 나온다.

