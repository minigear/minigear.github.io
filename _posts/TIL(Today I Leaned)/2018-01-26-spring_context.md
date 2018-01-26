---
layout: post
title:  "2018-01-26_spring_context"
date:   2018-01-26 10:30:00 +0900
categories: [TIL (Today I Learned)]
permalink: /til/:year/:month/:day/:title/
tags: [Dev, Spring]    
comments: true
---
### 2018년 01월 26일.  
springboot로만 프로젝트를 생성하여 연습하다 보니 정작 spring을 직접 설정하여 만들어 보는 연습을 하다 보니 spring context 설정 부분을 좀 더 이해할 수 있게 되었다.  

연습을 목적으로 spring으로 web application을 만들고 있다. tomcat을 따로 설치하고 war로 배포하는 구조이다. context는 xml 파일로 구성하고 web.xml에 applicationcontext와 servletcontext를 등록하였다. applicationcontext와 servletcontext를 하나로 합쳐서 web.xml에 등록을 하였더니 junit으로 테스트를 만드는 과정에서 문제가 발생하였다.  
```
    <servlet>  
        <servlet-name>spring</servlet-name>  
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>  
        <init-param>. 
            <param-name>contextConfigLocation</param-name>  
            <param-value>WEB-INF/spring-servlet.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
```  
 junit의 contextloader에 servletcontext를 읽어들이자 context를 읽어들이는데 에러가 발생  
 applicationcontext와 serveltcontext를 분리하고 applicationcontext만을 Juit에서 읽어들이 도록 처리  

rest api로 처리 중 List를 반환했을 때 json으로 자동 형변환 되지 않아 에러가 발생 하였다.  
이 문제는 jackson-databind 라이브러리 추가하여 해결 
 

 
  

