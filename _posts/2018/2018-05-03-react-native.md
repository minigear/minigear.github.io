---
layout: "post"
title: "TIL-react-native"
date:   "2018-05-03 13:55"
categories: [TIL (Today I Learned)]
permalink: /2018/:year/:month/:day/:title/
tags: [javascript]
comments: true
---

react-native: 결국 javascript로 작성한 코드를 ios용으로 object-c android용으로 java파일로
변환된다 이러한 작업을 react-native가 해준다  

react-native 장점  
- 화면을 css를 통해서 꾸밀 수 있다  
- 하나의 코드로 ios와 android 앱을 만들 수 있다. 단 OS별 차이점은 존재한다  
- 구동원리는 react와 동일하다, 하지만 더 엄격하다

https://facebook.github.io/react-native/docs/getting-started.html

1. react native cli 설치  
```
$ npm install -g react-native-cli
```
2. brew install watchman
3. IntelliJ에서 새로운 프로젝트 생성 - Static web - React Native
4. 실행
```
$ react-native run-ios
```
실행 이후 아래와 같은 에러가 발생 했다면 xcode가 설치되어 있지 않아서 이다.  
```
Found Xcode project kawai_todo.xcodeproj
dyld: Symbol not found: _OBJC_CLASS_$_SimProfileBundle
```

실행하였으나 에뮬레이터는 실행되나 정작 만든 앱이 실행되지 않고 터미널에 에러를 뱉어낸다면 watchman을 설치 해야한다  
