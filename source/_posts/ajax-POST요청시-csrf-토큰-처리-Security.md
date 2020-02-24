---
title: ajax POST요청시 _csrf 토큰 처리(Security)
date: 2020-02-05 09:37:58
tags: [security, _csrf, ajax]
categories: security
---

` security 설정으로 인해 ajax Post 요청 또는 form 태그 사용시 _csrf 토큰이 필요하다. 요청할때마다 매번 넣어주는것도 하나의 방법이지만 귀찮을게 보이므로 헤더에 설정하여 자동으로 값을 주도록 설정해보았다.`


**Spring Boot + Thymeleaf 사용 중 (Spring + Jsp일 경우와 코드의 큰 차이는 없다.)**

헤더 부분에 아래와 같이 meta태그를 넣어준다. (레이아웃의 헤더 부분에 넣어줘야 모든 페이지 자동 적용)
```html
  <meta name="_csrf" th:content="${_csrf.token}" />
	<meta name="_csrf_header" th:content="${_csrf.headerName}" />
```
meta태그안에 th:content라는 속성을 넣었는데 jsp라면 content로 쓰면 된다.
thymeleaf에서는 $ 또는 @ 등 표현구문이 다양한데 그런 구문들을 쓸라면 th:가 필수인듯 하다.
(저거때문에 token값 안넘어와서 삽질함)

그리고 아래와 같은 스크립트를 넣어준다. 위에 넣은 meta태그 데이터를 ajax POST 호출시 자동으로 값을 넘겨주는 필터 기능이다.
```html
<script>
	$.ajaxPrefilter(function(options, originalOptions, jqXHR) {
		var token = $("meta[name='_csrf']").attr("content");
		var header = $("meta[name='_csrf_header']").attr("content");      
		jqXHR.setRequestHeader(header, token);
	});
</script> 
```

그리고 위 코드들이 들어간 헤더를 포함한 페이지에서 ajax POST요청을 하면 잘 된다!
끝.
