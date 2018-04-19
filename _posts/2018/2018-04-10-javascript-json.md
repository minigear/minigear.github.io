---
layout: "post"
title: "javascript-json"
date:   "2018-04-10 14:24"
categories: [Dev]
permalink: /2018/:year/:month/:day/:title/
tags: [javascript, json]
comments: true
---
## JSON(javascript Object Notation)
> notation : 기록, 메모  
> 이해하기 쉽고 용량도 작아 많이 사용 한다

http://www.json.org/json-ko.html

### JSON API
- JSON.parse() : 인자로 전달된 문자열을 자바스크립트 데이터로 변환
- JSON.stringify() : 인자로 전달된 자바스크립트 데이터를 문자열로 반환

### JSON 과 Ajax
- 서버에서 JSON으로 데이터 받기
    - 서버 쪽 spring일 때 cotroller의 응답처리 method에서 반환 타입 앞에 @ResponseBody를 붙여 주면 메시지 컨버터에서 변환하여 HttpServletResponse에 넣어준다
- 서버로 JSON 데이터 보내기
> http 방식은 POST로 하고 헤더의 content-type을 application/json으로 한다

```javascript
let handlerSendJson = function () {
        let xhr = new XMLHttpRequest();
        let url = "";
        xhr.open("POST", url);

        let _data = "nickname : minigear", "name : kim";
        let data = JSON.parse(_data);

        xhr.onreadystatechange = function() {
            if(xhr.readyState === 4 && xhr.status === 200 ) {

            }
        }

        xhr.setRequestHeader("Content-Type", "application/json");
        xhr.send(data);

    }
```
