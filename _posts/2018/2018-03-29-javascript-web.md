---
layout: "post"
title: "javascript-web-BOM"
date:   "2018-03-29 13:53"
categories: [Dev]
permalink: /2018/:year/:month/:day/:title/
tags: [WEB, javascript]
comments: true
---

## HTML에서 javascript 로드하기

### inline
---
inline 방식은 태그에서 직접 자바스크립트를 기술하는 방식으로 정보와 제어가 섞이게 된다.

### script
---
<script></script> 태그를 만들어 자바스크립트를 삽입하는 방식 : 정보와 제어를 분리  

### javascript를 외부 파일로 분리
- script파일은 브라우저에 의해서 캐쉬되기가 쉽다 -> 데이터를 줄인다

### script 파일의 위치
script파일은 어디에 위치시키는 것이 좋은가 ?  
순차적으로
body태그 끝에 script를 위치시키는 것이 더 바람직 하다  
- head에 위치시키게 되면 스크립트를 모두 읽어 들일때 까지 웹브라우저는 기다리게 됨으로 사용자입장에서는 늦어지는 것으로 느끼게 된다
- 브라우저의 모든 element를 읽어 들이고 script를 바인딩 함으로 onload를 사용할 필요가 없다



```javascript
  var hw = document.getElementById('hw');
  hw.addEventListener('click', function(){
      alert('Hello world');
    })
```
window 전역객체의 onload를 설정 : 페이지를 모두 읽어들인 후 할당된 function을 실행 한다  

## Object Model
웹브라우저의 구성요소들은 하나하나가 객체화되어 있다. **자바스크립트로 이 객체를 제어해서 웹브라우저를 제어할 수 있게 된다.**  
![webbrowser object](http://learn.javascript.ru/article/browser-environment/windowObjects@2x.png)  

- DOM(Document Object Model): 문서를 제어하는 중요한 객체
- BOM(Browser Object Model): 브라우저를 조작 하는 객체
- javascript Core

## BOM(Browser Object Model)
---

### 전역객체 Window
모든 객체들은 window의 객체에 소속되어 있다  

### 사용자와 커뮤니케이션 하기
- alert : 경고창을 띄우고 이후 응답을 할때 까지 대기를 한다
- confirm : 사용자가 확인(true), 취소(false)를 리턴한다
- prompt : 입력창을 띄운다. 사용자가 입력한 값을 리턴한다.

### Location 객체 URL관리
#### 현재 윈도우의 URL 알아내기
- location.toString
- locaiton.href : 좀 더 선호하는 방식

#### URL Parsing
- locaiton.protocol
- location.host
- location.port
- locaiton.pathname
- locaiton.search
- locaiton.hash

#### URL 변경하기
- location.href 의 값을 바꾸고 싶은 url로 할당하면 해당 페이지로 이동 한다
- location.reload : 현재 페이지를 다시 읽어들인다

### Navigator 객체
- 브라우저의 정보를 제공하는 객체  
- 브라우저의 특성에 맞게 대응해야 할때 사용: 오래된 브라우저를 위해서

- appName
- appVersion
- userAgent : 브라우저가 서버측에 전송하는 USER-AGENT HTTP 헤더의 내용
- platform : 브라우저가 동작하는 운영체제

### 기능 테스트
기능을 지원하는 지 테스트 하는 것이다. 해당 기능이 없다면 false를 리턴 한다  
해당 기능 테스트를 통해 해당 기능을 지원하지 않는다면 사용자정의 함수로 해당 기능을 지원하도록 한다

### 창 제어
#### window.open : window.open(html파일)
  - 두번째 인자 : 창의 이름
  - _self : 현재창을 새로운 페이지로 이동 \<a>태그와 동일한 효과
  - _blank : 파일이름이 창의 이름이 된다
  - 창의 이름 : 이후 창을 열때마다 앞에 열렸던 창이 바뀐다
- window.close

#### 새 창의 접근
window함수를 실행 후 리턴하는 값을 객체로 받아 이 객체를 통해서 새 창을 조작 한다  
보안 상의 이유로 실제 서버에서만 동작하고, 같은 도메인의 창에 대해서만 조작이 가능 하다  

<input type='button' value='window open' onclick='openFunc()'>
<input type='button' value='window close' onclick='closeFunc()'>
<script>
var win;
function openFunc() {
  win = window.open('/2018/2018/03/29/til-2018-03-29/', 'ot');
}
</script>
<script>
function closeFunc() {
  win.close();
}
</script>

#### 팝업 차단
보안   
사용자의 명시적 행동에 의해서 window.open()을 할때에만 팝업 차단이 안되고 열릴 수 있다.
스크립트 안에서의 window.open은 팝업 차단이 된다
