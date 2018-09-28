---
layout: "post"
title: "TIL react-native Avatar icon 미표시 문제"
date:   "2018-08-30 10:49"
categories: [TIL (Today I Learned)]
permalink: /2018/:year/:month/:day/:title/
tags: [React-native, React, Npm, Android, react-native-elements]
comments: true
---

### 1. 현상 
 - react-native와 기존 app을 연결 하는 방법으로 개발 중 react-native-elements의 Avatar를 사용중 ICON이 정상적으로 출력되지 않음

### 2. 원인 
 -  icon을 정상적으로 가지고 오지 못함 
 
### 3. 해결   
- yarn add react-native-vector-icons  
- Android app 아래 build.gradle  아래 추가  
```gradle
apply from: "../../node_modules/react-native-vector-icons/fonts.gradle"
```

