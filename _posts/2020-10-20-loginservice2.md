---
title: "Spring boot+Vue.js login구현(2)-mariadb, mybatis 연동"

categories:
 - Login
tags:
 - rest api 
 - springboot
 - mybatis
 - login
last_modified_at: 2020-10-20T21:06:00-05:00
---

api의 디비 연동을 위해 mariadb를 사용하고 sql문을 쉽게 작성하기 위해 mybatis를 사용해줄 것이다.


우선, spring boot 프로젝트를 위해 [spring initialize](https://start.spring.io/)를 이용해 spring boot 프로젝트를 만들어 준다.  
![](https://boomini.github.io/assets/img/spring-init.PNG){: .align-center}

