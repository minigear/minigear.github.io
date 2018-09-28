---
layout: "post"
title: "TIL npm audit 문제 해결"
date:   "2018-08-07 13:29"
categories: [TIL (Today I Learned)]
permalink: /2018/:year/:month/:day/:title/
tags: [React-native, React, Npm]
comments: true
---

### 1. 현상 
 - react-native에서 참고할 코드를 로컬에 설치 후 구동 시키는 중 에러가 발생  

### 2. 원인 
 - package.json의 react-native버전 정보가 변경됨  
 - 터미널에서 npm audit fix를 실행 후 버전 정보가 자동으로 수정   
 
### 3. 해결   
 - npm audit를 실행 후 출력되는 내용을 바탕으로 package.json의 버전 정보를 수정  
 
 
