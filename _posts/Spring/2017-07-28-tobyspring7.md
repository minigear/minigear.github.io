---
layout: post
title:  "Toby 스프링3 7장"
date:   2017-08-28 13:36:00 +0900
categories: [Spring]
permalink: /spring/:year/:month/:day/:title/
tags: [스프링, spring, Resource]
comments: true
---

### 7.3.3 리소스 추상화
기존 코드의 문제점 : query 정보를 담은 xml파일의 위치가 DAO classpath에 제한되어 있다.  
여기서 DAO classpath는 소스코드의 위치가 아닌 빌드된 위치 .clss 생성된 위치를 말한다.  
실습 할때는 빌드시 해당 sqlmap.xml이 삭제되어 Resources디렉토리로 옮기고 읽어들이도록 하였다.

자바에서는 다양한 위치에 존재하는 리소스에 대해 단일화된 접근 인터페이스를 제공해주는 클래스가 없다.

URL (java.net.URL) 의 경우 원격만 가능하고 리소스 파일의 존재여부를 미리 알수가 없다.

그래서 스프링에서는 Resource라는 추상화 interface를 제공한다.

##### Resource
(org.springframework.core.io)
Resource는 다른 서비스 추상화의 오브젝트와 달리, 빈이 아니라 값으로 취급된다.
property의 ref가 아닌 value로 밖에 등록할 수 없다.

value로 취급함으로 객체로 변환해줄 장치가 필요하다 이게 ResourceLoader 이다.

##### ResourceLoader
(org.springframework.core.io)
스프링에서는 리소스의 종류와 위치를 문자열로 지정하면 이를 Resource 객체로 변환하는 ResourceLoader를 제공한다.   

스프링의 ApplicationContext는 ResourceLoader를 상속받는다.   
스프링에서 제공하는 빈으로 등록가능한 클래스에 파일 지정이 가능하다면 거의 모두 Resource type이다.  

Resource 타입은 빈으로 등록하지 않고 <property>의 value를 사용해 문자열 값으로 넣으면 ApplicationContext가 ResourceLoader의 역할을 하여 값을 변환 하고 property에 값을 주입한다.
