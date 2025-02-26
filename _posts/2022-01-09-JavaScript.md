---
layout: single
title:  "Java Script란? / 비교 연산자"
categories: JavaScript
tag: [foundation, JavaScript]
toc: true
author_profile: false
sidebar:
    nav: "docs"
typora-root-url: ../
---

# Java Script

자바스크립트는 웹페이제 생동감을 불어넣기 위해 만들어진 프로그래밍 언어이다.

이러한 자바스크립트로 작성한 프로그램을 스크립트라고 부른다. 

스크립트는 웹페이지의 HTML안에 작성할 수 있는데, 웹페이지를 불러올 때 

스크립트가 자동으로 실행된다.



### 자바 스크립트 엔진

브라우저엔 '자바스크립트 가상 머신' 이라 불리는 엔진이 내장되어 있다.

V8 - Chrome 과 Opera에서 쓰인다.

SpiderMonkey - Firefox에서 쓰인다.

IE는 버전에 따라 Trident나 Chakra라 불리는 엔진을 사용한다.

ChakraCore는 Microsoft Edge에 사용되며, SquirrelFish는 Safari에 사용된다.

엔진은 프로세스 각 단계마다 최적화를 진행한다. 심지어 컴파일이 끝나고 실행 중인 코드를 감시하면서,

이 코드로 흘러가는 데이터를 분석하고, 분석 결과를 토대로 기계어로 전환된 코드를 다시 최적화하기도 한다. 

이런 과정을 거치면 스크립트 실행 속도는 더욱 더 빨라진다.



### 브라우저에서 할 수 있는 일

브라우저 환경에선 웹페이지 조작, 클라이언트와 서버의 상호작용에 관한 모든 일을 할 수 있다.

+ 페이지에 새로운 HTML을 추가하거나 기존 HTML, 혹은 스타일 수정하기
+ 마우스 클릭이나 포인터의 움직임, 키보드 키 눌림 등과 같은 사용자 행동에 반응하기
+ 네트워크를 통해 원격 서버에 요청을 보내거나, 파일 다운로드, 업로드하기([AJAX](https://en.wikipedia.org/wiki/Ajax_(programming))나 [COMET](https://en.wikipedia.org/wiki/Comet_(programming))과 같은 기술 사용)
+ 쿠키를 가져오거나 설정하기. 사용자에게 질문을 건네거나 메시지 보여주기
+ 클라이언트 측에 데이터 저장하기(로컬 스토리지)

### 브라우저에서 할 수 없는 일

브라우저는 보안을 위해 자바스크립트의 기능에 제약을 걸어놓았다. 

이런 제약은 악성 웹페이지가 개인 정보에 접근하거나 사용자의 데이터를 손상하는 것을 막기 위해 만들어졌다.

- 웹페이지 내 스크립트는 디스크에 저장된 임의의 파일을 읽거나 쓰고, 복사하거나 실행할 때 제약을 받을 수 있습니다. 운영체제가 지원하는 기능을 브라우저가 직접 쓰지 못하게 막혀있기 때문입니다.

  모던 브라우저를 사용하면 파일을 다룰 순 있습니다. 하지만 접근은 제한되어 있습니다. 사용자가 브라우저 창에 파일을 ‘끌어다 두거나’ `<input>` 태그를 통해 파일을 선택할 때와 같이 특정 상황에서만 파일 접근을 허용합니다.

  카메라나 마이크 같은 디바이스와 상호 작용하려면 사용자의 명시적인 허가가 있어야 합니다. 자바스크립트가 활성화된 페이지라도 사용자 몰래 웹 카메라를 작동 시켜 수집한 정보를 [국가안보국(NSA)](https://en.wikipedia.org/wiki/National_Security_Agency)과 같은 곳에 몰래 전송할 수 없습니다.

- 브라우저 내 탭과 창은 대개 서로의 정보를 알 수 없습니다. 그런데 자바스크립트를 사용해 한 창에서 다른 창을 열 때는 예외가 적용됩니다. 하지만 이 경우에도 도메인이나 프로토콜, 포트가 다르다면 페이지에 접근할 수 없습니다.

  이런 제약사항을 '동일 출처 정책(Same Origin Policy)'이라 부릅니다. 이 정책을 피하려면 *두 페이지*는 데이터 교환에 동의해야 하고, 동의와 관련된 특수한 자바스크립트 코드를 포함하고 있어야 합니다. 자세한 사항은 추후 학습하도록 하겠습니다.

  다시 한번 강조하지만, 이런 제약사항은 사용자의 보안을 위해 만들어졌습니다. `http://anysite.com`에서 받아온 페이지가 `http://gmail.com`에서 받아온 페이지 상의 정보에 접근해 중요한 개인정보를 훔치는 걸 막기 위함입니다.

- 자바스크립트를 이용하면 페이지를 생성한 서버와 쉽게 정보를 주고받을 수 있습니다. 하지만 타 사이트나 도메인에서 데이터를 받아오는 건 불가능합니다. 가능하다 할지라도 원격 서버에서 명확히 승인을 해줘야 합니다(HTTP 헤더 등을 이용). 이 역시 보안을 위해 만들어진 제약사항입니다.

### 자바 스크립트만의 강점

- HTML/CSS와 완전히 통합할 수 있음
- 간단한 일은 간단하게 처리할 수 있게 해줌
- 모든 주요 브라우저에서 지원하고, 기본 언어로 사용됨

### 비교 연산자

`==` 

동등 연산자로 좌항과 우항을 비교해서 서로 값이 같다면 true 다르다면 false가 된다.

`===` 

일치 연산자로 좌항과 우항이 '정확'하게 같을 때 true 다르면 false가 된다. 여기서 정확하다는 말의 의미에 집중해야한다.

```html
<body>
    <script>
        alert(1 == "1");
        alert(1 === "1");
    </script>
</body>
```

위 결과는 차례대로 true 와 false가 나온다.

=== 는 정보가 같을 뿐만아니라 데이터의 형식도 모두 같아야 true가 나온다.

자바스크립트에서는 90% 정도 ===를 사용한다. 데이터 타입의 다름도 중요한 문제기 때문

