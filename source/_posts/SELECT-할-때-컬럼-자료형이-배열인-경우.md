---
title: SELECT 할 때 컬럼 자료형이 배열인 경우
date: 2019-12-24 17:22:28
tags: [mybatis, Array]
categories: mybatis
---

` DB에서 SELECT문으로 값을 가져오는데 컬럼 중 자료형이 integer[]이 있다. int[]로 받으면 될 줄 알았는데 null값이 들어온다. `

배열만 쓰면 왜이리 어려운건지...
mybatis에서는 자료형이 배열인 컬럼의 값을 바로 받을 수 있도록 지원되지 않는다고 한다.
그래서 SELECT 할 때 배열값을 문자열로 바꾸어서 문자로 받고 그 후 자바로 스플릿하여 써야 한다고 한다.
<br>
배열을 문자열로 바꾸어 조회하는건 간단하다.
```sql
 SELECT numbers::character varying
 FROM num
```
컬럼명뒤에 `::자료형 ` 을 적어주면 형변환하여 조회가 가능하다.

