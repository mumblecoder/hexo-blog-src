---
title: INSERT 후 INSERT된 seq값 가져와 사용하기
date: 2019-12-16 11:40:43
tags: [sql, insert, useGeneratedKeys]
categories: mybatis
---
<br>

`mybatis를 사용한 경우 insert시 *Mapper.xml 파일에 쿼리를 작성하여 쓴다.`


```xml
<insert id="insertLog" parameterType="Log">
  INSERT INTO log ( type, log)
  VALUES( #{type}, #{log})
</insert>
```
<br>

일반적으로 위와 같이 작성하여 사용하는데 seq값은 sequence를 사용하여 자동생성하여 넣기 때문에 seq 값이 필요하면 select 문을 사용하여 가져오곤 했다.

하지만 insert 태그안에 useGeneratedKeys, keyProperty 속성을 추가할 경우 쿼리를 또 쓸 필요없이 방금 생성되어 들어간 seq 값을 가져와 쓸 수 있다.

<br>

```xml
<insert id="insertLog" parameterType="Log" useGeneratedKeys="true" keyProperty="seq">
  INSERT INTO log ( type, log)
  VALUES( #{type}, #{log})
</insert>
```
<br>

위에 처럼 작성할 경우 Log 클래스에 seq 필드가 있다면 seq 필드에는 insert된 seq값이 자동으로 들어가게 된다.
그래서 getSeq() 메서드를 쓸 경우 방금 insert된 seq 값을 얻을 수 있다.

<br>

```java
  Log log = new Log();
  log.setType("comment");
  log.setLog("test");     //log 객체 안에는 type, log 값만 존재
    
  service.insertLog(log);
  
  int a = log.getSeq();    // insert 후에는 seq값이 자동 주입되어 변수 a로 받아 사용 가능하다.  
```
