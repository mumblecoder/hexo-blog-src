---
title: selectKey 태그를 사용한 INSERT,UPDATE
date: 2019-12-27 11:40:43
tags: [sql, insert, update, selectKey]
categories: mybatis
---

` 뷰페이지에 최소의 정보만 넘겨주다보니 서버에서 할일이 많아졌다. 
DB를 여러번 다녀오면 코딩은 편하겠지만 효율상 좋지 않으니 한번에 처리하기 위해 selectKey를 사용해보았다.`

selectKey태그는 insert, update태그안에서 사용할 수 있다. 
insert 또는 update 전이나 후에 select 문을 사용할 수 있다.
전에 사용할 경우엔 조회한 값을 insert, update문에서 사용도 가능하다.

```xml
   <insert id="insertList" parameterType="File">
    	<selectKey keyProperty="fileSeq" order="BEFORE" resultType="int">
    		SELECT seq 
    		FROM edd 
    		WHERE transaction_seq = #{seq}
    	</selectKey>
        INSERT INTO edd_file( file_seq, real_name, file_name, create_dt, memo, uploader)
        VALUES ( #{fileSeq},#{realName}, #{fileName}, now(), #{memo}, #{uploader})
    </insert>
```

위 코드를 보면 insert문이 실행되기전에 selectKey안에 있는 select문이 먼저 실행된다.
selectKey태그안에는 여러 속성값이 있는데 그 중 내가 사용한것만 적어보면 
keyProperty = 결과값 저장 이름? / order = 실행 순서 / resultType = 결과값 속성? 이다.

위 코드의 경우엔 seq값으로 다른 테이블의 seq값을 조회하여 fileSeq라는 값으로 받고 insert문에서 fileSeq값을 사용하여 진행한다. 
아래 코드를 보면 여러개의 값을 받아서 쓸수도 있다.

```xml
<update id="updateUserInfo" parameterType="UserInfo">
    	<selectKey keyProperty="userSeq,name,createDt" resultType="UserInfo" order="BEFORE">
	    	SELECT user_seq, name, create_dt 
	    	FROM info
	    	WHERE seq = #{seq} 
    	</selectKey>
        UPDATE user_info
        SET purpose=#{purpose}, job=#{job}, source_of_funding=#{sourceOfFunding},
                home_address=#{homeAddress}, office_address=#{officeAddress}
        WHERE user_seq = #{userSeq} 
          AND name=#{name} 
          AND TO_DATE(#{createDt},'yyyy-mm-dd') = DATE_TRUNC('day',create_dt)
    </update>
```
