---
layout: "post"
title: "TIL react-native bundle 서버 연결 에러"
date:   "2018-08-22 10:49"
categories: [TIL (Today I Learned)]
permalink: /2018/:year/:month/:day/:title/
tags: [React-native, React, Npm, Android]
comments: true
---

### 1. 현상 
 - react-native와 기존 app을 연결 하는 방법으로 개발 중 js 화면 수정 시 자동으로 화면이 갱신 되지 않음

### 2. 원인 
 -  번들서버는 잘 구동하고 있으나 연결이 되지 않음
 -  android studio의 logcat에서 아래와 같은 에러가 발생  
 ```
   CLEARTEXT communication to 10.0.2.2 not permitted by network security policy
```
 
### 3. 해결   
 - [참고 권한주는 방법](https://stackoverflow.com/questions/45940861/android-8-cleartext-http-traffic-not-permitted)
 -  AndroidManifest.xml파일 수정  
 ```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest ...>
    <uses-permission android:name="android.permission.INTERNET" />
    <application
        ...
        android:usesCleartextTraffic="true"
        ...>
        ...
    </application>
</manifest>
```
 
 #### 4. 기타 팁  
 현재 열여있는 port를 구동하는 프로세스 찾기  

sudo lsof -i :8081
