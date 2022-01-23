---
layout: single
title:  "Java Script(UI/API, 정규 표현식)"
categories: Java Script
tag: [foundation, JavaScript]
toc: true
author_profile: false
sidebar:
    nav: "docs"
typora-root-url: ../
---

# Java Script

### UI와 API의 차이?

+ UI(User Interface)란?

  사람 입장에서 컴퓨터와 의사소통이 가능하게 만드는 접점을 의미한다.

  + 키보드 A를 누르면 A가 출력된다.
  + Window + R키를 누르면 실행창이 나온다.
  + 구글 홈페이지에서 버튼을 클릭하거나 드래그하면 파란색으로 변하거나 다른 창이 나온다

  UI는 사용자 입장에서 컴퓨터와 대화를 하는 접점을 의미하며, 우리는 해당 접점을 통해 화면에 'A' 글자를 출력한다던지, 구글의 앱이 화면을 출력하는 특정한 결과를 얻는다.

+ API(Application Programming Interface)란?

  API는 앱(Application) 입장에서의 대화를 위한 접점이라고 할 수 있다.

  App입장에서는 자신보다 상위에 있는 시스템(운영체제)과 대화하고, 접점은 특수한 Code(함수)가 되게 된다.

  + 브라우저 상단에 javascript:alert("Hello World"); 라고 하면 팝업창이 뜨게되는데, 이것은 alert라는 함수를 상위 시스템에 주었을 때, 해당 팝업을 돌려주는 것이다.

![image-20220123160202117](/images/2022-01-23-JavaScript5/image-20220123160202117.png)

### 자바스크립트의 API

자바스크립트의 API는 크게 자바스크립트 자체의 API와 자바스크립트가 동작하는 호스트 환경의 API로 구분된다.

+ 자바스크립트 API 문서

  자바스크립트에 대한 여러 내용들이 기술되어있다.

  + ECMAScript (표준문서)
  + 자바스크립트 사전 (생활코딩)
  + 자바스크립트 레퍼런스 (MDN)
  + jscript 레퍼런스 (MSDN)

+ 호스트 환경의 API 문서

  각각의 호스트 환경에서만 동작하는 API

  + 웹브라우저 API
  + Node.js API
  + Google Apps Script API

### 정규식 표현

정규표현식은 문자열에서 특정한 문자를 찾아내는 도구이다. 먼저 컴파일과 실행과정이 있다. 

컴파일은 검출하고자 하는 패턴을 만드는 일이다. 우선 정규표현식 객체를 만들어야한다

+ 정규표현식 리터럴

  ```java
  var pattern = /a/
  ```

+ 정규표현식 객체 생성자

  ```javascript
  var pattern = new RegExp('a');
  ```

#### exec()

컴파일을해서 객체를 만들었다면 이제 문자열에서 원하는 문자를 찾아내야 한다.

<img src="/images/2022-01-23-JavaScript5/image-20220123163020009.png" alt="image-20220123163020009" style="zoom:67%;" />

+ exec() 함수를 이용하여 만든 패턴 a문자열을 찾아내서 추출한다.

<img src="/images/2022-01-23-JavaScript5/image-20220123163159084.png" alt="image-20220123163159084" style="zoom:67%;" />

만약 뒤에 /a./ 에서 .은 1문자 라는 뜻이다. 즉, a뒤에 어떠한 문자든 상관없지만 무조건 있어야 한다는 뜻이다. 때문에 예제에서 3번째 줄에 a뒤에 공백이기때문에 null이 나온다

반면에 4번째줄에서는 a다음에 b라는 문자가 있기때문에 ab라는 결과가 나온다.

#### test()

<img src="/images/2022-01-23-JavaScript5/image-20220123163501584.png" alt="image-20220123163501584" style="zoom:67%;" />

+ test() 함수는 해당 패턴이 있는가? 에대한 true와 false를 반환한다.

  정리하면 exec()는 필요한 정보를 추출하기 위함 / test()는 필요한 정보가 있는지 없는지

#### match()

<img src="/images/2022-01-23-JavaScript5/image-20220123195545445.png" alt="image-20220123195545445" style="zoom:67%;" />

+ match() 함수는 exec()함수와 비슷하다

<img src="/images/2022-01-23-JavaScript5/image-20220123195739650.png" alt="image-20220123195739650" style="zoom:67%;" />

#### replace()

+ replace()함수는 해당 문자와 같다면 두번째 인자로 바꾼다.

<img src="/images/2022-01-23-JavaScript5/image-20220123200045306.png" alt="image-20220123200045306" style="zoom: 67%;" />

문자뒤에 i를 붙이면 대문자 소문자를 가리지 않게된다.

<img src="/images/2022-01-23-JavaScript5/image-20220123200620487.png" alt="image-20220123200620487" style="zoom:67%;" />

문자뒤에 g를 붙이면 모든 결과를 리턴한다. 

<img src="/images/2022-01-23-JavaScript5/image-20220123200724112.png" alt="image-20220123200724112" style="zoom:67%;" />

i와 g를 같이쓰면 대,소문자 가리지않고 모든결과를 리턴한다.

#### 캡처

<img src="/images/2022-01-23-JavaScript5/image-20220123204930786.png" alt="image-20220123204930786" style="zoom:67%;" />

/(\w+)\s(\w+)/; 을 그림으로 표현하면 밑에와 같다

<img src="/images/2022-01-23-JavaScript5/image-20220123205051584.png" alt="image-20220123205051584" style="zoom: 50%;" />

+ \w는 A-Z, a~z, 0~9 까지 나타내는 문자를 의미한다.

+ +는 수량자를 의미하며 하나 이상이라는 뜻이기때문에 A , AA같은 문자나 단어도 포함된다.

+ \s 는 공백을 뜻한다.

```javascript
var result = str.replace(pattern, "$2, $1");
```

replace를 이용하여 pattern에 해당하는 문자를 뒤에있는 문자로 치환한다.

$2는 everybody이며 $1은 coding을 의미하므로 결과는 everybody, coding이 나온다.

중간의 공백은 ,(컴마) 뒤에 붙게된다.