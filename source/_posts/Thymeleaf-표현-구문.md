---
title: Thymeleaf - 표현 구문
date: 2020-02-02 17:56:34
tags: [thymeleaf]
categories: Thymeleaf
---

` Thymeleaf를 사용할 때 표현 구문을 잘 읽혀두면 더 쉽게 간결하게 코드를 짤 수 있다.`


## [Thymeleaf docs](https://www.thymeleaf.org/doc/tutorials/2.1/usingthymeleaf.html)

간단한 표현
- 변수 표현식 : ${...}
- 선택 변수 표현식 : *{...}
- 메시지 표현 : #{...}
- 링크 URL 표현식 : @{...}

리터럴
- 텍스트 리터럴 : 'one text', 'Another one!', ...
- 숫자 리터럴 : 0, 34, 3.0, 12.3, ...
- 부울 리터럴 : true,false
- 널 리터럴 : null
- 리터럴 토큰 : one, sometext, main, ...

텍스트 작업
- 문자열 연결 : +
- 리터럴 대체 : |The name is ${name}|

산술 연산
- 이진 연산자 : +, -, *, /,%
- 빼기 부호 (단항 연산자) : -
- 부울 연산 : true, false
- 이항 연산자 : and,or
- 부울 부정 (단항 연산자) : !,not

비교와 평등
- 비교기 : >, <, >=, <=( gt, lt, ge, le)
- 평등 연산자 : ==, !=( eq, ne)

조건부 연산자
- 그렇다면 : (if) ? (then)
- 그렇지 않은 경우 : (if) ? (then) : (else)
- 기본: (value) ?: (defaultvalue)

Thymeleaf docs에 따르면 위와같은 표현 구문들이 존재한다. 물론 모든 구문은 결합하고 중첩해서 사용가능하다.
` ex - 'User is of type ' + (${user.isAdmin()} ? 'Administrator' : (${user.type} ?: 'Unknown')) `

저렇게만 보면 저걸 언제 어떻게 쓰라는지 감이 잘 안온다...
구글링해서 얻은 예시들을 한번 보자.

### 1. 메시지 표현 : #{...}
` <p th:utext="#{home.welcome}">Welcome to our grocery store!</p> `
스프링의 메세지 태그를 대체한다고 생각하면 될 듯 하다.

`home.welcome=¡Bienvenido a nuestra tienda de comestibles! `
properties 파일 또는 DB에 위와 같이 저장해두고 불러와서 쓸 때 사용하는 표현방법이라고 생각하면 될 듯하다.

메세지에 변수가 필요할 경우 `home.welcome=¡Bienvenido a nuestra tienda de comestibles! {0}` 으로 저장해두고
` <p th:utext="#{home.welcome(${session.user.name})}"> ` 괄호안에 변수로 사용할 값을 넣으면 된다. 
변수가 여러개일 경우엔 쉼표(,)로 구분


### 2. 변수 표현식 : ${...}
기존에 쓰던 변수 표현 기능에 부가적 기능이 추가 되었다고 보면 될 것 같다.





### 3. 선택 변수 표현식 : *{...}




### 4. 링크 URL 표현식 : @{...}





