---
layout: "post"
title: "IntelliJ create-react-app 문제"
date:   "2018-04-27 17:22"
categories: []
permalink: /2018/:year/:month/:day/:title/
tags: []
comments: true
---

문제 : IntelliJ에서 create-react-app을 생성 했을 때 yarn start를 통해 실행했을 때 문제  

터미널 상에서 create-react-app을 실행해서 만들었을 때는 문제를 발생 시키지 않음  

가설 : 터미널에서의 create-react-app과 IntelliJ에서의 create-react-app의 버전이 다르다.  
      npm의 설치 module을 확인했을 때 create-react-app이 없음에도 IntelliJ에서 프로젝트 코드가 생성 되었다   

해결책
  1. IntelliJ에서 빈 프로젝트를 생성 후 command에서 ../create-react-app 프로젝트명 으로 생성 한다
  2. 터미널에서 생성하고자 하는 위치로 이동하여 create-react-app 프로젝트명으로 생성 한다   
