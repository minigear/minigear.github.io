---
layout: "post"
title: "javascript-web-DOM"
date:   "2018-03-29 17:49"
categories: [Dev]
permalink: /2018/:year/:month/:day/:title/
tags: [javascript,WEB]
comments: true
---
## DOM

### 제어 대상을 찾기
 기본 흐름 : 제어할 객체를 찾고 객체를 제어 한다  

#### 브라우저의 객체를 찾기  

- document.getElementsByTagName : 태그의 이름을 가지고 객체들을 가져온다
- document.getElementsByClassName : class 이름을 가지고 객체들을 가져온다.
- document.getElementById : id로 객체를 조회하고 객체를 가지고 온다. 성능이 좋다.
- document.querySelector : css 선택자의 문법을 이용해서 객체를 조회하여 하나의 객체만 가져온다.
- document.querySelectorAll : css 선택자의 문법을 이용해서 객체를 조회하여 객체를 유사배열에 담아 가져온다.
  - css 선택자
    - '태그'
    - '.클래스이름'
    - '#아이디' : 문서에서 하나만 존재해야 한다

## jQuery
---
*jQuery는 DOM을 내부에 감추고 보다 쉽게 웹페이지를 조작할 수 있도록 돕는 도구이다*  

라이브러리도 결국은 javascript를 사용하여 dom bom을 조작하기 쉽게 해주는 도구에 불과함으로 javascript를 알고 있어야 한다.  

### jQuery의 사용

CDN 이란 ?
```javascript
  <script src='//code.jquery.com/jquery-1.11.0.min.js'><script>
```
위 구문에서 src 값중 '//'의미는 앞쪽에 http와 https 가 상황에 맞게 동작하도록 한다  

운영할 때는 min 버전(압축)을 사용하여 네트워크 대역폭을 줄인다  

*jQuery를 다운 받아 사용할 때 현재 디렉토리를 기준으로 설정한다.*  

### 제어 대상을 찾기(jQuery)
$()는 jQuery의 함수이다. 이 함수의 인자로 CSS의 선택자를 전달하면 jQuery는 jQuery 객체를 반환한다.
jQuery 객체를 리턴받아 method로 작업하구 다시 리턴 받은 객체를 method로 연결하여 chaining할 수 있다.  java에서 봤던 패턴이다  

``` javascript
$('li').css('color','red');
```

### HTMLElement
getElement* method가 반환하는 객체  
- HTMLElement : 객체가 하나만 리턴 된다면 HTMLElement를 반환 -> HTML{태그}Element
  - HTMLElement의 객체를 상속받은 태그객체를 리턴 한다(javascript에서도 Interface가 존재하는 가? )
- HTMLCollection : 복수개의 객체가 리턴한다면 HTMLCollection을 반환
- HTMLElement는 상속을 통해 공통의 속성들을 가지게 된다

```javascript
<script type="text/javascript">
  var target = document.getElementById('a');
  console.log(target.constructor.name);

  var target = document.getElementById('b');
  console.log(target.constructor.name);

  var target = document.getElementById('c');
  console.log(target.constructor.name);

  var target = document.getElementsByTagName('li');
  console.log(target.constructor.name);
</script>

```

### DOM Tree
![dom tree](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/904/2234.png)

### HTMLCollection
HTMLCollection은 리턴 결과가 복수인 경우에 사용하게 되는 객체다.   
HTMLCollection의 특이점 : 목록이 실시간으로 갱신된다.

참고 : console을 그룹으로 묶을 수 있다.  
```javascript
console.group('');
console.groupEnd();
```

### jQuery 객체
jQuery 함수의 리턴값으로 jQuery 함수를 이용해서 선택한 엘리먼트들에 대해서 처리할 작업을 프로퍼티로 가지고 있는 객체다   

#### 암시적 반복
DOM과 다르게 jQuery 객체의 메소드를 실행하면 선택된 엘리먼트 전체에 대해서 동시에 작업이 처리된다   

#### 체이닝

#### 조회

#### 조회 - map
jQuery의 객체에 map함수에 각 엘리먼트를 처리할 function(index, element) {} 를 지정해주면 각 엘리먼트가 읽어들일 때 마다 해당 함수가 호출되어 처리된다  
```javascript
  $("p").map(function(index, element){
    console.log(index, element);
  })
```

#### jQuery 객체 API
자주 사용되는 jQuery 함수는 리스트는 ?   

[jQuery API 설명](https://api.jquery.com)

---

### Element 객체
Element와 HTMLElement와의 관계는 ?   
- Element는 HTMLElement의 부모 객체이다  
- DOM은 HTML만을 관리하는 표준이 아니다  
- Node - Element - HTMLElement  

#### 주요기능(API)
---
#### 식별자
  문서내에서 특정한 엘리먼트를 식별하기 위한 용도로 사용되는 API

  Element.classList   
  Element.className   
  Element.id   
  Element.tagName   

#### 조회
  엘리먼트의 하위 엘리먼트를 조회하는 API   

  Element.getElementsByClassName   
  Element.getElementsByTagName   
  Element.querySelector   
  Element.querySelectorAll   

#### 속성
  엘리먼트의 속성을 알아내고 변경하는 API   

  Element.getAttribute(name)   
  Element.setAttribute(name, value)   
  Element.hasAttribute(name);   
  Element.removeAttribute(name);   

---

#### 식별자 API

- Element.tagName : 현재 엘리먼트의 tagName을 읽어 들인다 (읽기 전용)   
```javascript
document.getElementsByTagName('').tagName;
```
- Element.id : 문서에서 하나만 존재하는 id에 해당하는 element를 읽어들인다. 읽어들인 element.id를 통해서 해당 id값을 수정할 수 있다.
```javascript
  var sample = document.getElementById('originalId');
  sample.id = 'modifiedId';
```

- Element.className : 문서내에서 여러개의 엘리먼트를 그룹핑한 클래스를 가지고 온다.
- Element.classList : className보다 사용하기가 편리하다  
  - add('') : class를 추가한다
  - remove('') : class를 제거한다
  - toggle('') : class가 없다면 추가하고 있다면 제거한다

*HTML에서의 class : 하나의 element에 여러개의 class를 가지고 있을 수 있다.*
```html
  <li class ='class1 class2 class3'></li>
```

#### 조회 API
조회의 범위를 줄이기  document를 통해서 읽어들인 element에 .getElement*를 통해서 해당 엘리먼트의 하위 엘리먼트를 읽어들인다   

#### 속성 API
- Element.getAttribute(name) : element가 가지고 있는 속성을 읽어온다
- Element.setAttribute(name, value) : element의 속성값을 수정 한다
- Element.hasAttribute(name) : element에 속성이 있는지 확인 한다
- Element.removeAttribute(name) : element에서 속성을 삭제한다

속성과 프로퍼티
- 속성과 프로퍼티의 차이점 :
  - 프로퍼티 방식이 좀 더 속도가 빠르다.
  - attribute 방식으로 값을 가져올 때와 property 방식으로 가지온 값이 다를 수 있다.
  - property방식은 이름에 주의해야 한다

#### jQuery 속성 제어 API
jQuery 객체의 메소드 중 setAttribute, getAttribute에 대응되는 메소드는 attr이다. 또한 removeAttribute에 대응되는 메소드로는 removeAttr이 있다.   

##### attribute와 property
장점 : prop('이름') : 직접 property로 접근할 때보다 실수를 줄일 수 있다
```javascript
<a id="t1" href="./demo.html">opentutorials</a>
<input id="t2" type="checkbox" checked="checked" />
<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
// 현재 문서의 URL이 아래와 같다고 했을 때
// http://localhost/jQuery_attribute_api/demo2.html
var t1 = $('#t1');
console.log(t1.attr('href')); // ./demo.html
console.log(t1.prop('href')); // http://localhost/jQuery_attribute_api/demo.html

var t2 = $('#t2');
console.log(t2.attr('checked')); // checked
console.log(t2.prop('checked')); // true
</script>
```

#### jQuery 조회 범위 제한
```javascript
  $( ".marked", "#active").css( "background-color", "red" );
  $( "#active .marked").css( "background-color", "red" );
```
 - find();
 ```javascript
  $( "#active").find('.marked').css( "background-color", "red" );
 ```

## Node 객체
*모든 DOM 최상위 객체*  
> 사전적 의미 : 트리(tree) 구조에서 데이터의 상하위 계층을 나타내는 위치의 항목. 각 노드를 연결해 주는 것이 분기(分岐)이며, 루트(root)와 서브트리(subtree)로 구성됨.   

![Node 전체 객체 관계](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/904/2242.png)

### 관계
*Node의 관계 메서드를 사용할 때 주의점은 노드와 노드사이에 공백은 text 객체로 인식한다는 점이다*

- Node.childNodes
- Node.firstChild
- Node.lastChild
- Node.nextSibling
- Node.previousSibling
- Node.contains()
- Node.hasChildNodes()

### 값
Node 객체의 값을 제공하는 API

- Node.nodeValue   
- Node.textContent   

### 자식관리
Node 객체의 자식을 추가하는 방법에 대한 API

- Node.appendChild()
- Node.removeChild()

### 노드종류 API
노드 작업을 하게 되면 현재 선택된 노드가 어떤 타입인지를 판단해야 하는 경우가 있다. 이런 경우에 사용할 수 있는 API가 nodeType, nodeName이다.

- Node.nodeType
  node의 타입을 의미한다.
- Node.nodeName
  node의 이름 (태그명을 의미한다.)

```
  ELEMENT_NODE 1
  ATTRIBUTE_NODE 2
  TEXT_NODE 3
  CDATA_SECTION_NODE 4
  ENTITY_REFERENCE_NODE 5
  ENTITY_NODE 6
  PROCESSING_INSTRUCTION_NODE 7
  COMMENT_NODE 8
  DOCUMENT_NODE 9
  DOCUMENT_TYPE_NODE 10
  DOCUMENT_FRAGMENT_NODE 11
  NOTATION_NODE 12
  DOCUMENT_POSITION_DISCONNECTED 1
  DOCUMENT_POSITION_PRECEDING 2
  DOCUMENT_POSITION_FOLLOWING 4
  DOCUMENT_POSITION_CONTAINS 8
  DOCUMENT_POSITION_CONTAINED_BY 16
  DOCUMENT_POSITION_IMPLEMENTATION_SPECIFIC 32
```

#### 재귀함수
노드를 탐색하기 위하여 재귀함수를 사용한다   
> traverse
  1.〈장소를〉 가로지르다, 횡단하다, 넘다, 건너다

```javascript
	function traverse (target, callback){

		if(target.nodeType === Node.ELEMENT_NODE) {
			callback(target);

			var e = target.childNodes;
			for(var i=0; i<e.length; i++) {
				traverse(e[i], callback);
			}
		}

	}

	var c = document.getElementById('start');

	traverse(c, function(element) {
		console.log(element);
	})
```

> document의 body태그의 노드를 읽어들여 traverse함수에 전달한다.  
읽어들인 target(body)에서 ELEMENT 타입이면 콜백함수를 호출하여 인자값을 전달하고 콘솔에 출력한다. 타겟 노드 아래의 child nodes를 읽어들여 하나씩 traverse함수에 넣어서 동일한 작업을 반복 시킨다.  child node가 없을 때 까지 동일한 작업을 반복 한다.    

---

### 노드 변경 API

#### 노드추가
---
appendChild(child)  
노드의 마지막 자식으로 주어진 엘리먼트 추가  
insertBefore(newElement, referenceElement)  

document.createElement(tag_name)   
엘리먼트 노드를 추가한다.  
document.createTextNode(data)  
텍스트 노드를 추가한다.  

#### 노드 제거
삭제의 권한은 부모 node에게 있다.
target.parentNode.removeChild(target)


#### 노드 바꾸기
replaceChild(newChild, oldChild)

---
### jQuery 노드변경 API
#### 추가
- before : 태그 앞
- prepend : 태그 안 content 앞
- after : 태그 뒤
- append : 태그 안 content 뒤

#### 삭제
- remove : element 삭제
- empty : element가 가지고 있는 text 삭제

#### 변경

*객체 A를 객체B로 변경한다*
- replaceWith : 객체A.replaceWith(객체B)
- replaceAll : 객체B.replaceAll(객체A)

```javascript
$("#bt3").click(function() {
let m = document.createElement("div");
let t = document.createTextNode("hello world");
m.appendChild(t);

// $("#t3").replaceWith(m);
// $('<div>hello</div>').replceAll('#t3');
 $(m).replaceAll('#t1');

})
```

#### 복사
객체A.clone().replaceAll(객체B) : 객체A를 복사하여 객체B를 복사한 객체B로 교체한다   

#### 이동
객체A.append(객체B) : document에 있는 존재하는 엘리먼트가지고온 객체B를 객체A에 append하면 기존 위치에서 객체 A 뒤로 이동하게 된다

### 문자열로 노드 제어
- innerHTML
 문자열로 자식 노드를 만들 수 있는 기능을 제공한다. 또한 자식 노드의 값을 읽어올 수도 있다.
- outerHTML
자기자신을 포함한 하위 엘리먼트들

- innerText, outerText
값을 읽을 때는 HTML 코드를 제외한 문자열을 리턴하고, 값을 변경할 때는 HTML의 코드를 그대로 추가한다.

- insertAdjacentHTML(선택, 추가할 값)
  - 'beforebegin' : 선택 element 앞
  - 'afterbegin' : 선택 element의 하위 element의 첫번째 앞
  - 'beforeend' : 선택 element의 하위 element의 맨마지막 뒤
  - 'afterend' : 선택 element 뒤
