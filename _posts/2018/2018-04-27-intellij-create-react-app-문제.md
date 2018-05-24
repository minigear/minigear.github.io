---
layout: "post"
title: "TIL-IntelliJ create-react-app 문제"
date:   "2018-04-27 17:22"
categories: [TIL (Today I Learned)]
permalink: /2018/:year/:month/:day/:title/
tags: [create-react-app]
comments: true
---

문제 : IntelliJ에서 create-react-app을 생성 했을 때 yarn start를 통해 실행했을 때 문제  
```
Error: Cannot find module '../scripts/start'
```

터미널 상에서 create-react-app을 실행해서 만들었을 때는 문제를 발생 시키지 않음  

해결책
  1. IntelliJ로 react app을 만들고 터미널에서 yarn을 실행
  ```
    yarn install v1.6.0
    warning ../../../package.json: No license field
    [1/4] 🔍  Resolving packages...
    [2/4] 🚚  Fetching packages...
    [3/4] 🔗  Linking dependencies...
    [4/4] 📃  Building fresh packages...
    success Saved lockfile.
  ```
  2. yarn start를 해주면 정상 동작 한다
