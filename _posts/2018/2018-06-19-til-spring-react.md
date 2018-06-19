---
layout: "post"
title: "TIL Spring react"
date:   "2018-06-19 14:13"
categories: [TIL (Today I Learned)]
permalink: /2018/:year/:month/:day/:title/
tags: [Spring, maven, Webpack, 토이프로젝트]
comments: true
---

보통은 react + nodeJs 혹은 react + dJango를 쓰는 듯한다.  
react + spring을 찾아보니 https://github.com/spring-guides/tut-react-and-spring-data-rest
에 boiler code가 있어서 참고 하기로 하였다.  

maven에서 react를 사용할 수 있도록 제공하는 plug-in이 존재 한다  
pom.xml에 빌드에 frontend-maven-plugin을 추가해 준다  
```
<plugin>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-maven-plugin</artifactId>
</plugin>
```

개발하던 중 react를 위 코드를 참고하여 프로젝트에 추가하자 문제가 발생하였다   
증상: 서버측에서 fetch를 사용하여 json을 가져오는 코드를 추가하게 되면 반영이 안되는 것이었다  
원인: webpack 1.12.2 에서 es6 코드가 지원되지 않아 빌드과정에서 에러가 발생하였다  
해결: webpack의 버전을 올리기로 하였다  
   - package.json : webpack의 버전을 3.8.1 으로 수정
   - webpack.config.js : debug를 삭제 한다, loader를 babel에서 babel-loader로 변경   

> IntelliJ에서 maven 빌드 과정을 보고 싶다면 IntelliJ의 오른쪽 텝에서 Maven Projects를 선택 ->
Lifecycle에서 한단계씩 실행해 보면 빌드 과정 중 어떤 에러가 나오고 어떻게 조치를 해야하는 지 찾을 수
있다  
