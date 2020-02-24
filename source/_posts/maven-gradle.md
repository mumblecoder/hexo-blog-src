---
title: Maven? Gradle?
date: 2020-02-22 17:46:34
tags: [maven, gradle]
categories: Tool
---

` 스프링부트 관련해서 검색하다보면 pom.xml이 아닌 gradle 예시 코드를 많이 보게된다. gradle이 뭔지조차 모르기에 찾아보기 시작했다.`

ant, maven, gradle은 빌드도구이다.
빌드도구는 **소스코드를 컴파일, 테스트, 정적분석등을 하여 실행가능한 애플리케이션으로 생성해주는 프로그램**으로
__라이브러리를 추가, 관리해주고 시간이 지남에 따라 라이브러리의 버전을 동기화__ 해주는 기능을 갖고있다.

먼저 gradle을 설명하기전에 기존 사용중인 pom.xml, 즉 Maven에 대해 먼저 알아보자

## 1. Maven
우리가 흔히 말하는 메이븐은 아파치 메이븐으로 아파치 앤트의 대안으로 나왔다.
아파치 앤트의 단점을 보완하고 부가기능을 추가하여 나왔다고 한다.
메이븐에 대해 정리해보자면
1. 우리가 사용하는 많은 라이브러리들을 관리해주는 도구이다
2. pom.xml을 이용한 정형화된 빌드 시스템
3. Repository에서 자동으로 필요한 라이브러리 파일을 불러와준다.
4. 라이브러리가 서로 종속할 경우 pom.xml 코드가 길고 복잡해진다.


## 2. Gradle
그래들은 JVM기반의 빌드도구로 ant와 maven의 단점을 보완해서 등장했다.
가장 큰 특징으로는 Groovy 언어를 기반으로 만들어졌다.
maven에 비해 늦게 출시된만큼 사용성이나 성능등에서 뛰어나다고 한다. (그러므로 빌드 속도도 빠르다.)
멀티프로젝트에 사용하기 좋고 코드의 길이도 짧고 가독성도 좋다. 
Groovy언어를 배우기만 한다면 안 쓸 이유가 없다고 한다.


## 3. 결론
기능상 성능상으론 Gradle이 좋지만 Maven의 사용이 여전히 많은건 익숙함 때문이다.
소규모의 프로젝트에서는 gradle을 굳이 배우지 않고 maven 을 사용해도 무방하지만 규모가 커질수록 gradle을 사용하는 것이 좋다.
결론은 gradle을 공부해서 사용해보자


### 참고자료 출처
[참고글1](https://bkim.tistory.com/13)
[참고글2](https://okky.tistory.com/179)
[참고글3](https://m.blog.naver.com/PostView.nhn?blogId=seatom&logNo=220881024126&proxyReferer=https%3A%2F%2Fwww.google.com%2F)
