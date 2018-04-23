---
layout: "post"
title: "javascript-1"
date:   "2018-03-23 15:00"
categories: [Dev]
permalink: /2018/:year/:month/:day/:title/
tags: [javascript]
comments: true
---
javascript의 실행 환경
- 웹브라우저
- node.js
- 구글 스프레드시트


typeof 객체 : 데이터 타입  왜 데이터 타입을 숫자와 문자로만 설명했을 까 ?  
-> javascript의 데이터 타입 찾아보기  

문자열.length() : 문자열 길이  
문자열.indexof("문자") : 문자열에서의 문자 위치  

변수  
변수 선언 : var 변수명

주석 :
```javascript
  // 한줄 주석
  /*
    여러줄 주석
  */
```

## 조건문  
비교 연산자  
==  :  동등 연산자 타입이 아닌 의미하는 값이 같다면 같다고 취급한다  
=== :  일치 연산자 데이터 타입까지 엄격히 검사한다  

prompt : 입력창을 띄움 브라우저 환경  

논리연산자  
- && : AND  
- \|\| : OR


boolean 대체제  
- '' : 빈문자열은 false  
- 0 : false  
- undefined : false  
- null : false  
- NaN : false  

## 반복문(loop / iterate)
- while : 조건문이 false가 될때까지 반복
``` javascript
while(조건문) {
  반복 실행 코드
}
```
- for
``` javascript
  for() {

  }
```

i++ 과 ++i의 차이점 : i++은 해당 라인을 실행 후 덧셈 연산이 일어난다. ++i는 먼저 덧셈연산이 일어나고 해당 라인이 실행된다.  

### break와 continue
break : 해당 반복문을 중단하고 반복문을 탈출한다.  
continue : continue 이후 명령라인을 실행하지 않고 반복문 윗쪽으로가서  반복문을 실행한다.

## 함수 (function)
함수는 재사용성을 올려준다.  
javascript는 함수지향 언어이다.
``` javascript
function 함수명() {
  return ;
}
```

입력과 출력 :    
argument와 parameter의 차이점은 ?   
   - 매개변수 : parameter    
   - 인자 : argument 전달되는 값 자체    

익명 함수 : 정의와 호출을 같이 한다. 일회성 호출을 위해서 사용한다.   
``` javascript
(function () {

})();
```

## 배열
연관된 데이터를 모아서 통으로 관리하기 위한 데이터 타입니다.  
index는 0부터 시작 한다.  
``` javascript
  var test = ["test1", "test2", "test3"];
```

### 배열 조작
- 추가 : 배열.push(입력값);
- 여러개의 값을 입력할때 : 배열.concat(배열);
- 배열 앞쪽에 값을 추가하고 싶을 때 : 배열.unshift(입력값);
- 배열 중간에 값을 추가하고 싶을 때 : 배열.splice(index, howmany, 입력값, 입력값...);
- 제일 앞의 값을 제거 : 배열.shift();
- 제일 뒤의 값을 제거 : 배열.pop();
- 정렬
    - 배열.reverse();
    - 배열.sort();

## 객체(Object)
데이터를 담아내는 그릇  
 ```javascript
  Object {키: 값, 키: 값, 키: 값}
  var test = {};
  var test1 = new Object();
  오브젝트.키
  오브젝트[키]
 ```

### 객체조작
 반복문   
 ```javascript
 for(key in 배열) {
   key , 배열[key]
 }
 ```

 this : 함수가 속해있는 객체

## 모듈
자주 사용되는 코드를 별도의 파일로 분리
재 사용성을 높임  
필요한 로직만을 로드해서 메모리 낭비를 줄일 수 있다  
다운로드된 모듈을 다른곳에서 사용할 수 있어 네트워크 트래픽을 줄일 수 있다.

note: 기본적으로 javascript의              변수는 전역변수 이다. 전역변수임을 방지하기 위해서 클로저를 사용한다. 왜 클로저가 필요할 까 ? 모듈화를 만들게 되면 다른 사람의 모듈도 가져다 사용할 수 있다. 그럼으로 변수의 중복이 발생하여 버그를 발생할 수 있다. 이를 방지하기 위해서 클로저를 사용한다.  

### 모듈화
``` javascript
<script src="xxxx.js"></script>
```

## 라이브러리

## UI와 API 그리고 문서보는 법
API : Application Programming Interface   

레퍼런스와 튜토리얼  
  - 자바스크립트 자체의 API:
    - [ecma 레퍼런스](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
  - 자바스크립트가 동작하는 호스트환경의 API

## 정규표현식
[생활코딩-정규표현식][63175132]

  [63175132]: https://opentutorials.org/course/909/5142 "생활코딩-정규표현식"

### 컴파일
- 정규표현식 리터럴
```javascript
  var pattern = /a/;
```
- 정규표현식 객체 생성자
```javascript
  var pattern = new RegExp('a');
```

- 정규표현식의 작업들 : 추출, 치환, 테스트
- 정규표현식 메소드 실행
  - RegExp.exec(); 패턴에 맞는 문자열을 추출
  - RegExp.test(); 찾는 패턴이 있다면 true, 없다면 false

- 문자열 메소드 실행
  - match(pattern) : 추출
  - replace(pattern, '치환하고자하는 문자') : 치환

- 옵션
  - i : 대소문자를 구분하지 않는다.
```javascript
  var pattern = /a/i;
```
  - g : 검색된 모든 결과를 리턴한다.
```
  var patter = /a/g;
```

- 캡처 : 그룹을 지정하고 그룹을 가져와 사용하는 것을 캡쳐라 한다.
``` javascript
  var pattern = /(\w+)\s(\w+)/;
  var str = "coding everybody";
  var result = str.replace(pattern, "$2, $1");
```

- 치환
