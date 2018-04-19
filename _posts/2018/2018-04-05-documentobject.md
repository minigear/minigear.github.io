---
layout: "post"
title: "DocumentObject"
date:   "2018-04-05 11:05"
categories: [Dev]
permalink: /2018/:year/:month/:day/:title/
tags: [Web, javascript]
comments: true
---
## Document 객체
HTMLDocument 객체 : 문서전체를 가리키는 객체

### 주요 API
- createElement() : node 만들기
- createTextNode() : 텍스트 node 만들기

### 문서 정보 API
- title
- URL
- referrer
- lastModified

## Text 객체
> DOM에서 공백도 하나의 객체이다

- 값 API
  - nodeValue
  - data

- 조작 API
  - appendData(data) : 추가할 값을 parameter 로 넘긴다
  - deleteData(start, end) : 대상의 start위치에서 end위치까지 문자를 삭제한다
  - insertData(start, data) : start위치부터 data를 추가한다
  - replaceData(start, end, data) : start에서 end 사이의 문자를 없애고 data로 바꾼다
  - substringData(start, end) : start에서부터 end만큼 이동한 문자열을 반환한다

## 문서의 기하학적 특성
element의 위치와 크기를 얻는 방법

top : 위에서 부터 element 까지의 px
left :  좌측에서부터 element 까지의 px

offsetParent : 측정의 기준점이 누구였는가를 알고싶을때 사용

엘리먼트의 위치를 의미하는 top, right의 값을 통해서 기준이 그 부모가 아니라 body라는 것을 알 수 있다. 그리고 이를 명시적으로 확인할 수 있는 방법은 offsetParent 속성을 호출하는 것이다. 만약 부모 중 CSS position의 값이 static인 td, th, table 엘리먼트가 있다면 이 엘리먼트가 offsetParent가 된다

viewport

window.scrollTo(x, y) : 문서의 스크롤을 y만큼 움직여라

스크린의 크기
innerWidth : viewport 넓이
innerHeight : viewport 높이

screen.width : 사용자의 모니터 넓이
screen.height : 사용자 모니터의 높이
