---
layout: post
title:  "2017-08-25_TIL"
date:   2017-08-25 12:36:00 +0900
categories: [TIL (Today I Learned)]
permalink: /til/:year/:month/:day/:title/
tags: [Jekyll, 블로그]
comments: true
---


# 블로그 테마적용
테마 적용 방법
- 마음에 드는 테마를 github에서 zip파일 형태로 다운 받는다
- 압축을 풀고 기존에 있던 \_post를 제외하고 덮어 씌운다.
- 문제점 : 덮어 씌우고 jekyll build를 실행하였을 때 에러가 발생
- 해결 : 디렉토리내의 gem파일을 삭제 후 build한다.

폰트 변경
- \_scss/base/\_global.scss 파일을 수정

permalink : 퍼머링크(permalink)는 인터넷에서 특정 페이지에 영구적으로 할당된 URL 주소라고 한다
- 블로그 태그 적용 미적용의 차이점
 - 적용  : http://127.0.0.1:4000/til/2017/08/25/test/
 - 미적용 : http://127.0.0.1:4000/til%20(today%20i%20learned)/2017/08/25/test/

 작성한 글이 보이지 않는다
 - post의 date 일자가 현재 시간보다 미래이면 글이 보이지 않는다.
