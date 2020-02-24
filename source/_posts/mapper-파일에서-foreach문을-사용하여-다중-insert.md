---
title: mapper 파일에서 foreach문을 사용하여 다중 insert
date: 2019-12-16 13:05:58
tags: [mapper, foreach]
categories: mybatis
---


`반복되는 쿼리를 호출 할 경우 매번 sqlSession 객체를 생성하는게 시간을 많이 잡아먹어서 foreach문으로 한번에 처리하기로 했다.`

<br>

```xml
<insert id="insertEddScored" parameterType="Map">
	INSERT INTO score_board( seq, list_seq, score, result)
	VALUES 
	<foreach collection="scoredList" item="scored" separator=",">
  	(#{scored.seq}, #{scored.listSeq}, #{scored.score},  #{scored.result})
	</foreach>	
</insert>
```

<br>

` collection = 반복할 파라미터 이름, item = 반복문에서 사용할 변수명, separator = 반복문 구분자 `

위와같은 쿼리로 mapper 파일에 작성해두면 sqlSession 객체를 한번만 생성할 수 있고 다중 insert가 가능하다.<br>
실제 날아가는 쿼리는 아래처럼 된다.<br>

```sql
INSERT INTO score_board( seq, list_seq, score, result)
VALUES (100, 1, 10,  true),
      (101, 2, 20,  true),
      (102, 2, 10,  false),
      ...
```

<br>

foreach문을 사용함으로 소요시간은 많이 줄었는데 한번에 긴 쿼리를 보내는게 좋은건지는 잘 모르겠다.
<br>
foreach문을 사용한 또 다른 예시는 아래와 같다.
<br>

```xml
<update id="minusUserScore" parameterType="Scoring">
	<foreach collection="seqs" item="seq" separator=";">
		UPDATE result
		SET score = score + #{temp}, update_dt = now()
		WHERE user_seq = #{seq}
	</foreach>
</update>
```

<br>
UPDATE문을 통째로 반복해야해서 separator값에 세미콜론을 넣었다.<br>
반복하는 상황에 맞게 separator값을 잘 줘야 에러없이 진행된다.<br>
  
