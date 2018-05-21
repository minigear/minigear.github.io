---
layout: "post"
title: "github page custom domain ssl 설정"
date:   "2018-05-21 18:27"
categories: [TIL (Today I Learned)]
permalink: /2018/:year/:month/:day/:title/
tags: [blog, ssl]
comments: true
---
문제: github에 pages를 사용하여 블로를 만들었을 때 custom domain으로 연결하였을 시 ssl 적용 방법

해결: github 페이지의 설정으로 가서 custom domain을 삭제후 저장 다시 custom domain을 입력 후
저장 후 조금 있으면 ssl 적용 페이지 옵션이 선택 가능하게 바뀐다  
>추가: 아래 참조사이트에서 처럼 dns 설정에서 a type으로 하여 github의 ip 주소를 설정하지 않고 cname
type으로 설정하여도 정상적으로 ssl이 적용된다. sub domain으로 블로그주소를 설정하여서 그런지 a type으로 설정 시
github에서 cname type으로 변경하라고 경고 메일이 발송된다   

참조: [개발자스럽다](https://blog.gaerae.com/2018/05/github-pages-custom-domains-https.html)
