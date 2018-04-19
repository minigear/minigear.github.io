---
layout: "post"
title: "javascript-network"
date:   "2018-04-09 17:27"
categories: [Dev]
permalink: /2018/:year/:month/:day/:title/
tags: [javascript, web]
comments: true
---

## 네트워크 통신

### Ajax
Ajax는 웹브라우저와 웹서버가 내부적으로 데이터 통신을 하게 된다. 그리고 변경된 결과를 웹페이지에 프로그래밍적으로 반영함으로써 웹페이지의 로딩 없이 서비스를 사용할 수 있게 한다.  

 Asynchronous javascript and xml   
비동기적으로 javascript를 사용하여 데이터를 주고 받는다  


#### XMLHttpRequest
```javascript
  let xhr = new XMLHttpRequest();
  let url = '';
  
  xhr.open('GET', url);
  xhr.onreadystatechange = function() {
    //상태정보 변경되었을 때 처리 핸들러
    if(xhr.readyState === 4 && xhr.status === 200){
      xhr.responseText;
    }
  }
  xhr.send();
```

#### POST
```javascript
let xhr = new XMLHttpRequest();
let url = '';

xhr.open('POST', url);
xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
xhr.send(data);
```
