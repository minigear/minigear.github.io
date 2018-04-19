---
layout: "post"
title: "javascript-OOP"
date:   "2018-03-27 17:38"
categories: [Dev]
permalink: /2018/:year/:month/:day/:title/
tags: [javascript]
comments: true
---

## 객체 지향 프로그래밍
---
- 객체란 : 성격이 비슷한 기능과 상태를 묶어놓은 것으로 재활용이 가능하게 한것이다.

### 문법과 설계
- 문법
- 설계 : 추상화 -> 현실의 복잡함을 관심사만 골라내어 단순화 시키는 것

- 부품화 : 재활용성, javascript의 method

- 은닉화, 캡슐화 : 사용자에게 안쪽을 감추고 사용법만 노출하여 사용하도록 한다.

- 인터페이스 : 설계시 규격을 만들어 규격에 맞으면 부품을 바꾸어 쓸수 있게 하는 것

## 생성자와 new
---
### 객체
*prototype-based Programming*  
객체 만들기  
```javascript
  var o1 = {};
  o1.name = 'no_name';
  o1.introduce = function() {return name;}

  var o2 = {
    'name' : 'no_name',
    'introduce' : function() {
      return 'My name is '+name;
    }
  }
```

### 생성자
---
**생성자 : 객체를 만드는 역할을 하는 함수**  
```javascript
  function Person() {}
  var p = new Person();
```

java는 class 내에 생성자가 있다. 그러나 javascript는 함수만 존재한다.
생성자를 통해서 객체를 초기화 하고 만든다

```javascript
  function Person(name) {
    this.name = name;
    this.introduce = function() {
      return 'My name is ' + this.name;
    }
  }

  var p = new Person('no_name');
```

## 전역객체
---
**전역객체(Global Object)는 특수한 객체다. 모든 객체는 이 전역객체의 프로퍼티이다.**  
전역객체에 모든 객체들은 프로퍼티이다
웹브라우저 기반의 javascript는 window가 전역객체이다.   
node.js 기반은 Global이 전역객체이다.


## this
---
*함수 안에서 사용되는 약속된 변수이며 값은 함수를 어떻게 호출하였느냐에 따라 달라진다.*  

#### 메소드의 호출
---
*this는 함수를 호출한 객체를 가르킨다.*  

#### 생성자의 호출
---
생성자 안에서의 this는 생성자를 통해서 만든 객체를 가르킨다.

#### apply, call
---
*함수 리터럴 : 생성자를 통해서 함수를 만드는 것은 불편함으로 함수를 간단하게 만드는 문법*  
```javascript
  var sum = new Function('x','y','return x+y;');
```
- function은 객체로 다른 객체에 유연하게 붙여서 사용할 수 있다
- this는 apply를 통해서 호출하는 객체를 가르킨다.  

## 상속(inheritance)
---
자식의 객체는 부모의 객체를 *재활용* 하면서 추가 기능이나 기존 기능을 수정하여 사용한다.

prototype : 상속하거나 받고자 하는 객체를 할당한다   

## prototype(원형)
---
function에 new를 붙이면 객체를 반환하는 생성자가 된다.  
객체를 만들 때 그 객체가 가지고 있어야 하는 method 혹은 property 를 가질수 있도록 하기위해 생성자를 사용 한다.
객체의 원형 prototype는 java의 class와 같은 느낌이다. 즉 붕어빵 틀...   

prototype chain : 각 함수의 prototype으로 연결되어 속성을 이어진것
해당 객체에 찾는 값이 없다면 해당 객체의 생성자의 prototype에서 찾게 된다.

주의 : 객채를 상속할 때 prototype에는 상속받고자하는 객체의 생성자로 new를 붙여 객체를 붙여 넣는다

## 표준 내장 객체의 확장
---
*standard Built-in Object : 자바스크립트가 기본적으로 가지고 있는 객체*  

  - Object
  - Function
  - Array
  - String
  - Boolean
  - Number
  - Math
  - Date
  - RegExp

*표준 내장 객체 + 호스트환경 객체 + 사용자정의 객체*  

### 배열의 확장
---
*내장 객체의 확장 : 내장객체의 prototype에 새로운 기능 function을 추가한다.*  

랜덤 값 얻기
```javascript
  Math.floor((Math.random() * (얻고자하는값의 범위)))
```
floor 최대정수 반환

## Object
---
*Object 객체 : 아무것도 상속받지 않은 순수한 객체. 기본적인 저장단위*   
- 모든 객체는 Object를 상속받는다
- Object.method : Object.method 형태로 사용
- Object.prototype.method : 생성된 객체에서 사용, 모든 객체들이 상속받은 공통의 method

- Object 객체의 기능 확장 : Object의 prototype에 function을 추가한다  
- Object 객체의 기능 확장의 위험성 : Object 객체를 확장하게 되면 모든 객체에 영향을 미친다

- o.hasOwnProperty(name) : 상속받은 property가 아닌 직접 정의된 property를 체크하는 함수

## 데이터 타입
---
*원시 데이터 타입 과 객체 데이터 타입*  

### 원시 데이터 타입
- 숫자 -> Number
- 문자열 -> String
- 불리언 -> Boolean
- null -> X
- undefined -> X

### 레퍼 객체
'.' : Object access Operator  

wrapper Object : 원시데이터 타입을 객체로 감싸는 역할을 하는 객체 자동 객체화  

```javascript
  var str = 'coding';
  str.prop = 'everybody';
  console.log(str.prop); // undefined
```

## 참조
---
### 복제
전자화된 시스템에서 복제는 현실에서의 복사보다 비용이 적게 발생 한다.  
값 자체를 동일하게 메모리에 할당하는 것  

### 참조
복제와 참조의 차이점 : 참조는 윈도우의 바로가기의 개념과 비슷하다.  
객체값을 가리키는 변수를 다른 변수에 할당하게 되면 해당 변수도 그 객체를 가리키게된다.  

### 함수와 참조
함수에 원시데이터를 넘겼을 때 : 함수내에서 해당 값을 변경해도 영향이 없다     
함수에 객체를 넘겼을 때 : 함수 안에서 넘겨받은 객체의 property 값을 변경하게 되면 객체의 값도 변경되게 된다
