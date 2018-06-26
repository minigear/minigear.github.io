---
layout: "post"
title: "TIL 토이프로젝트 - spring react"
date:   "2018-06-19 14:13"
categories: [TIL (Today I Learned)]
permalink: /2018/:year/:month/:day/:title/
tags: [Spring, maven, webpack, 토이프로젝트]
comments: true
---

보통은 react + nodeJs 혹은 react + dJango를 쓰는 듯한다.  
react + spring을 찾아보니 https://github.com/spring-guides/tut-react-and-spring-data-rest
에 boiler code가 있어서 참고 하기로 하였다.  

maven에서 react를 사용할 수 있도록 제공하는 plug-in이 존재 한다  
pom.xml에 빌드에 frontend-maven-plugin을 추가해 준다  
```
<plugin>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-maven-plugin</artifactId>
</plugin>
```

개발하던 중 react를 위 코드를 참고하여 프로젝트에 추가하자 문제가 발생하였다   
증상: 서버측에서 fetch를 사용하여 json을 가져오는 코드를 추가하게 되면 반영이 안되는 것이었다  
원인: webpack 1.12.2 에서 es6 코드가 지원되지 않아 빌드과정에서 에러가 발생하였다  
해결: webpack의 버전을 올리기로 하였다  
   - package.json : webpack의 버전을 3.8.1 으로 수정
   - webpack.config.js : debug를 삭제 한다, loader를 babel에서 babel-loader로 변경   

> IntelliJ에서 maven 빌드 과정을 보고 싶다면 IntelliJ의 오른쪽 텝에서 Maven Projects를 선택 ->
Lifecycle에서 한단계씩 실행해 보면 빌드 과정 중 어떤 에러가 나오고 어떻게 조치를 해야하는 지 찾을 수
있다  

증상: state={} 에러 발생  
원인: state = {}는 es7 부터 지원 된다고 한다   
  [출처](https://github.com/react-toolbox/react-toolbox/issues/309)
해결: babel preset에 stage-0를 추가   

증상: stage-0를 추가하면 async function에서 에러가 발생한다  
원인: stage-0 프리셑에서 추가된 것을 지원하기 위해서는 별도의 polyfill이 필요하다  
해결: babel 기반의 폴리필을 추가하는 방법은 두 가지이다.  
- babel-polyfill을 사용하는 방법
  - babel-polyfill을 npm을 통해서 설치한다. => package.json에 추가 한다
  - webpack.config.js에 polyfill이 필요한 js에 추가한다
  ```javascript
   entry: ['babel-polyfill','./src/main/js/app.js'],
   ```
- babel-plugin-transform-runtime을 사용하는 방법
  - babel-runtime을 설치한다
  - babel-plugin-transform-runtime을 --save-dev로 설치한다
  - .babelrc에 아래와 같이 추가한다
  ```
    "plugins": [
      ["transform-runtime", {
        "polyfill": false,
      "regenerator": true
      }]
    ]
  ```

> polyfill : 웹 개발에서 기능을 지원하지 않는 웹브라우저 상의 기능을 구현하는 코드

참고 사이트 :  
    - babel-polyfill 설명: http://programmingsummaries.tistory.com/401  
    - stackoverflow  질문 및 답변 : https://stackoverflow.com/questions/33527653/babel-6-regeneratorruntime-is-not-defined  

위와 같이 설정을 해주면 create-react-app에서 처럼 동일한 형식의 es6 코드를 작성 할 수 있다  
