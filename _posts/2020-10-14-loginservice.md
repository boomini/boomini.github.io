i---
title: "Spring boot+Vue.js login프로그램 구현(1)"

categories:
 - Spring
 - Vuejs
 - Login
tags:
 - rest api 
 - springboot
 - vuejs
 - login
last_modified_at: 2020-10-14T21:06:00-05:00
---

spring boot로 Restful api를 구현하고 vuejs로 프론트앤드를 개발하여 로그인 서비스를 구현해주려고 한다.
## 로그인 구현을 위해 알아야하는 개념 
1. **서버**
[서버와 클라이언트 이해하기](https://boomini.github.io/server/first-server/)
[RestApi](https://boomini.github.io/server/restapi/)  
[로그인 인증방식](https://boomini.github.io/server/authentication/)  
jwt 토큰 인증방식

2. **Spring boot**
 - spring mvc 개념  
 - swagger 
 - db연결(나는 mariadb를 사용하여 구현할 것이다.)
 - mybatis : 쿼리문을 작성하기 쉽게 도와준다.
 - Spring security
 - jwt  
 - 로그 찍는 방법 (loggin.package의 의미)
 - 예외처리  


3. **Vue.js**
 - axios통신 : header에 어떻게 토큰을 넣을 것인지.
 - 어떻게 localstorage에 넣을지: 토큰을 뷰에서 로컬스토리지에 저장하여 로컬스토리지에 저장한 토큰을 가지고 헤더에 담아서 다른 서비스를 요청한다. 
 - 비동기 처리 방식의 문제점 해결.(promise)  

로그인 구현을 위한 서버를 구현하고 확인하기 위해 알아야 하는 개념들이다. 위에 적은 순서대로 로그인 서비스를 구현해보자!  
깃허브에서 이미 완성된 login사용자 관리 프로그램을 확인할 수 있다.[https://github.com/boomini/cms-login](https://github.com/boomini/cms-login)  
연습용으로 만든거여서 코드가 깔끔하지 못하고 필요하지 않은 기능이 추가되어 있거나 필요한 기능이 빠져있다..!!
