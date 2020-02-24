---
title: mybatis - useGeneratedKeys
date: 2020-01-20 17:30:08
tags: [mybatis, useGeneratedKeys]
categories: mybatis
---

` mybatis 쓰면서 useGeneratedKeys="true" keyProperty="seq" 속성을 자주 쓰는데 오늘 이거 관련한 오류를 발견했다.`

위 속성을 적용해놓으면 insert되어 자동 생성된 seq값을 파라미터로 넣은 객체안에 담아올 수 있다.

[useGeneratedKeys관련 포스팅](https://pyo1297.github.io/2019/12/16/INSERT-%ED%9B%84-INSERT%EB%90%9C-seq%EA%B0%92-%EA%B0%80%EC%A0%B8%EC%99%80-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0/)

항상 객체안에 seq값이 없을때만 사용해서 insert된 seq값이 담긴다고만 생각했지, 안에 seq값이 존재할 경우에 대해서 생각해본적이 없었다.

결론은 업데이트된다. 새 seq값으로. 

```java
int beforeSeq = obj.getSeq();
service.insert(obj);
int afterSeq = obj.getSeq();
```

위 코드를 실행하면 beforeSeq값과 afterSeq값은 다르다.
기존의 seq값도 필요하다면 별개로 저장할 것!
