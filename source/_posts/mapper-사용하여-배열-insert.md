---
title: mapper 사용하여 배열 insert
date: 2019-12-24 15:08:49
tags: [mybatis, Array, mapper]
categories: mybatis
---

` mapper.xml 파일에 insert 문을 작성해서 넣는데 DB에 insert를 하려는데 자료형이 int 배열인 칼럼에서 에러 발생 `

insert하려는 칼럼들의 자료형은 date(**timestamp**), country(**character varying**), user_seq(**integer[]**), amount(**double**)
parameter의 자료형은 date(**String**), country(**String**), userSeq(**int[]**), amount(**double**) 이다.
처음에는 아래처럼 xml을 작성했었다.

```xml
<insert id="insertEvent" parameterType="Event" >
  INSERT INTO event(date, country
    <if test="userSeq != null">, user_seq</if>
    <if test="amount != 0.0">, amount</if>
  )
  VALUES(TO_TIMESTAMP(#{date},'yyyy-MM-dd HH24:MI:SS'), #{country}
    <if test="userSeq != null">#{userSeq}</if>
    <if test="amount != 0.0">, #{amount}</if>
  )
</insert>
```

userSeq의 자료형이 int배열이라서 insert가 될 줄 알았는데 에러가 뜸
` java.lang.IllegalStateException: Type handler was null on parameter mapping for property `

그래서 아래 코딩으로 수정하였더니 insert 성공!

```xml
<insert id="insertEvent" parameterType="Event" >
  INSERT INTO event(date, country
    <if test="userSeq != null">, user_seq</if>
    <if test="amount != 0.0">, amount</if>
  )
  VALUES(TO_TIMESTAMP(#{date},'yyyy-MM-dd HH24:MI:SS'), #{country}
    <if test="userSeq != null">
      <foreach collection="userSeq" item="seq" separator="," open=",ARRAY[" close="]">
        #{seq}
      </foreach>
    </if>
    <if test="amount != 0.0">, #{amount}</if>
  )
</insert>
```

insert문에서 배열을 넣으려면 아래처럼 작성해야된대서 위와 같은 foreach문을 넣었다.

```sql
  INSERT INTO member (name, age, hobby)
  VALUES('park', 11, ARRAY['movie','sing','craft']);
```
