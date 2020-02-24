---
title: SpringBoot - thymeleaf 세팅
date: 2020-01-31 12:25:29
tags: [template, thymeleaf, springboot]
categories: Thymeleaf
---

` 이번에 2개의 프로젝트를 만들어 진행해야하는데 그 중 하나가 SpringBoot + thymeleaf 이다. `

지금까지는 jsp만 사용해봤는데 이번 프로젝트는 타임리프를 사용해야한다.

그 이유로는 
1. thymeleaf가 더 빠르고 html로만 이루어져서 적용하기도 편하다.
2. boot에는 thymeleaf가 더 잘맞는다
3. 참고하는 프로젝트가 그렇게 되어있다 

thymeleaf를 사용하기위해 pom.xml에 아래와 같은 코드를 추가하였다.

```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
		
<dependency>
	<groupId>nz.net.ultraq.thymeleaf</groupId>
	<artifactId>thymeleaf-layout-dialect</artifactId>
</dependency>
```
1. spring-boot-starter-thymeleaf : 타임리프 사용을 위해서 추가
2. thymeleaf-layout-dialect : 타임리프로 레이아웃 기능을 사용하기 위해 추가

구글링으로 알아볼땐 1번만 추가하면 내장되있어서 레이아웃 기능까지 쓸 수 있다고 했는데 계속 안되서 결국 2번도 추가하니 레이아웃 기능을 쓸 수 있었다.

application.yml 에는 아래와 같이 추가하였다.
```yml
  thymeleaf:
    view-names: admin/*   #해당 루트로 호출되는 뷰에만 적용 
    prefix: classpath:/templates/  #jsp설정에서 /WEB-INF/views 설정과 동일
    check-template-location: true
    suffix: .html   #jsp설정에서 .jsp 설정과 동일
    mode: HTML5
    cache: false     #default = true 이지만 false로 해놓으면 변동사항을 바로바로 확인가능하다
```

현재로는 관리자 페이지에는 thymeleaf를, 그 외에는 jsp를 사용할 생각이라서 view-names를 설정하였다. 전체 적용할라면 안쓰면 된다.

### 이제 뷰를 만들어 볼 차례

기존 jsp 사용할때는 webapp > WEB-INF > views 안에 jsp페이지를 넣었다.
하지만 thymeleaf 사용시엔 위치가 다르다.
**src/main/resources 안에 templates 폴더를 만든 후 그 안에 html 파일들을 넣어야 한다.** 
` 내경우에는 view-names를 admin/*으로 설정해놔서 templates 폴더안에 admin폴더를 만들고 그 안에 html 파일들을 넣었다. `

![](/images/20200131-post.png)


```java
@GetMapping("/dashboard")
  public ModelAndView getMain(String lang) {
  
    ModelAndView mav = new ModelAndView("admin/dashboard");
    //new ModelAndView("dashboard"); 로 할 경우 view-names에 해당하지 않아서 thymeleaf 적용 안됨.
    return mav;
}

```

이렇게 세팅하고 컨트롤러에서 호출하면 페이지가 잘 보인다.



