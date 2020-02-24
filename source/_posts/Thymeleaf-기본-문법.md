---
title: Thymeleaf 기본 문법
date: 2020-01-31 13:25:29
tags: [thymeleaf, th]
categories: Thymeleaf
---


## 타임리프를 적용했으니 사용을 해보자

먼저 쓰려는 html 파일 상단에 아래와 같이 설정을 해야 타임리프 사용가능

```html
<html xmlns:th="http://www.thymeleaf.org">
```

이제 평소와 똑같이 코드를 작성하되 th를 활용하여 작성해보자

## 1. th:text : 태그안에 들어갈 text 값 설정

```html	
<span th:text="${temp}"></span>
```

## 2. th:value : 태그안에 들어갈 value 값 설정

```html	
<input type="hidden" id="test" th:value="${temp}"/>
```

## 3. th:if, th:unless : if, else 구문

```html
<th:block th:if="${temp != null && temp2 > 0}">
    <input type="hidden" id="tag" th:value="${temp}"/>
</th:block>
<th:block th:unless="${temp == null || temp2 < 0}">
    <input type="hidden" id="tag" value="0"/>
</th:block>  
```

## 4. th:utext : 태그가 포함된 값을 넣을때 사용. (태그로 인식함)
```html
<th:block th:utext="${htmlText}"></th:block>
```

## 5. th:with : 변수 정의
```html
<th:block th:with="context=${@environment.getProperty('app.interface.url')}"></th:block>
```

## 6. th:switch , th:case : switch, case 구문 (case="*" : default)
```html
<div th:switch="${temp}">
    <p th:case="1" class="normal">
       ...
    </p>
    <p th:case="2" class="hard">
       ...
    </p>
    <p th:case="*" class="default">
        ...
    </p>
</div>
```

## 7. th:fragment : 영역 설정? include 기능, layout 설정시 꼭 필요하다
```html
<th:block th:fragment="adminNavbar">
  ...
</th:block>
```
위 코드를 작성해두면 다른 페이지에서 아래 코드를 작성하여 include 가능
```html
<th:block th:replace="fragments/admin-navbar :: adminNavbar"></th:block>
<!-- th:replace="파일경로명 :: fragment설정이름" 해당파일경로는 templates/fragments/admin-navbar.html 이다.-->
```
fragment로 설정해놓은 코드는 th:replace, th:insert, th:include 로 가져와 쓸 수 있다.
위 3가지에 대해서는 layout 설정 글에서 좀 더 자세히 쓰는걸로

그외에 #lists, #maps 등 유틸 사용이 가능하고 *{}, @{} 등 다양한 표기법? 식? 이 많다.
프로젝트 진행하면서 찬찬히 익혀보는걸로...

참조 사이트
[타임리프 유용 팁](https://eblo.tistory.com/56?category=737346)
[타임리프 기본 문법](https://eblo.tistory.com/55?category=737346)
[타임리프 문법 정리](https://shlee0882.tistory.com/134)

끝!
