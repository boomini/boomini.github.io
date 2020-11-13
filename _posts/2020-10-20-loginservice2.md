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
![](https://boomini.github.io/assets/img/spring-init.PNG)  

의존성 설정은 나중에 추가 할 수 있다. 위와 같이 세팅하고 압축 파일을 생성 한 뒤 압축을 해제 하여 해당 디렉토리를 IDE에서 열어서 사용하면 된다.  
####SqlSessionFactory

####커넥션풀(Connection Pool)이란?  
: 풀(Pool)속에 데이터베이스와의 연결(커넥션)들을 미리 만들어 두고 데이터베이스에 접근시 풀에 남아있는 커넥션 중 하나를 받아와서 사용한 뒤 반환하는 기법.  


사용이유 : 웹 애플리케이션은 다수의 사용자가 데이터베이스에 접근해야 하는 상황에 사용자들이 요청할 때마다 연결을 만들고 해제하는 과정을 진행하게 되면 비효율적이다. 그래서 커넥션풀을 이용하여 미리 여러 연결을 만들어놓고 필요한 사용자가 요청시 미리 만들어 놓은 연결을 주는 형식으로 효과적으로 DB연결 및 지원사용을 할 수 있다.

####ApplicationContext BeanFactory
ApplicationContext : 오브젝트 생성, 관계설정, 만들어지는 방식, 자동생성, 후처리등 
####References
[https://goddaehee.tistory.com/205](https://goddaehee.tistory.com/205)
[https://mybatis.org/spring/ko/index.html](https://mybatis.org/spring/ko/index.html)
