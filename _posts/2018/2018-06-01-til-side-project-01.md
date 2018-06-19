---
layout: "post"
title: "TIL 토이프로젝트 01"
date:   "2018-06-01 13:32"
categories: [TIL (Today I Learned)]
permalink: /2018/:year/:month/:day/:title/
tags: [JAVA, 토이프로젝트]
comments: true
---
토이 프로젝트 : 책 제목을 검색하면 책 정보 및 빨간 책방 방송 중 해당 책을 다루었던 방송 URL을 반환 시킨다   

1. springboot로 백엔드  
2. react로 프론트엔드  

웹브라우저 상의 JavaScript에서 다른 도메인의 사이트를 html 크롤링하기 위해 fetch를 실행하게 되면 크로스 도메인 이슈가 발생한다
header에 no-cors 옵션을 주고 요청할 경우 응답에서 body의 값이 제한된다   
chrome 개발자 툴의 network 상에서 response에서 정상적인 html을 볼수 있으나 JavaScript에서는 null이 찍힌다  

웹브라우저 상에서 크롤링 하기위해서는 cors 이슈가 있음으로 서버측에서 크롤링 하기로 결정  

복기할겸 예전에 해봤던 springboot + h2 DB + JPA로 우선 rest api로 제공 하는 것으로 결정   

toString : JSON 스타일로 프린트 할때 아래와 같이 정의한다   
라이브러리 추가  
```maven
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-lang3</artifactId>
    <version>3.4</version>
</dependency>
```

```java
public String toString() {
       return ToStringBuilder.reflectionToString(this, ToStringStyle.JSON_STYLE);
   }
```

방송 회차 정보 추출 표현식 활용  
```JAVA
String broadcastingNumber =
                    tds.eq(0).text()
                            .replace("회", "")
                            .replace("\b", "")
                            .replaceAll("\\[(.*?)\\]","")
                            .trim();
```

h2 database 와 JPS 연결 설정   
application.properites  파일에 설정 추가
```properties
spring.datasource.url=jdbc:h2:mem:minigear;DB_CLOSE_DELAY=-1;DB_CLOSE_ON_EXIT=FALSE
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql = true

spring.mustache.expose-session-attributes=true
```

h2 db consle 접속 jvm에 임베디드로 기동됨으로 intelliJ에서 바로 접속할수 없다     
http://localhost:8080/h2-console/   

하지만 다른 방법도 존재한다 http://jojoldu.tistory.com/234     

JPA 에서 LIKE JPA repository interface 선언시 findByFirstnameLike method를 추가해주면 된다  

[Spring Data JPA - Reference Documentation](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#repositories.query-methods)
