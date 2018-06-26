---
layout: "post"
title: "TIL webpack"
date:   "2018-06-21 10:24"
categories: [TIL (Today I Learned)]
permalink: /2018/:year/:month/:day/:title/
tags: [webpack, npm]
comments: true
---

## 1. NPM
  1. 초기화 : package.json 파일 생성
    - npm init : 초기화
    - npm init -y : default 초기화
  2. 패키지 설치 및 업데이트  
  - 로컬 설치 : npm install package명   
      local 디렉토리의 node_modules 디렉토리에 설치된다. 로컬로 설치된 경우 코드에서 require로
      import 시킬 수 있다  
  - 글로벌 설치 : npm install package명 --global
  - \--save : 앱을 구동하기 위해 필요한 모듈 & 라이브러리 설치
  - \--save-dev : 앱 개발시 필요한 모듈& 라이브러리 설치  

## 2. Webpack
  - Entry
    - webpack 으로 묶은 모든 라이브러리들을 로딩할 시작점 설정
    - a, b, c 라이브러리를 모두 번들링한 bundle.js를 로딩한다
    - 1개 또는 2개 이상의 엔트리 포인트를 설정할 수 있다  
  - Output
    - entry에서 설정하고 묶은 파일의 결과값을 설정
  - Output Name Options
    - \[name]: 엔트리 명에 따른 output 파일명 생성
    - \[hash]: 특정 webpack build에 따른 output 파일명 생성
    - \[chunkhash]: 특정 webpack chunk에 따른 output 파일명 생성
  - 참고 api
    - path.join() : 해당 API가 동작하는 OS의 파일 구분자를 이용하여 파일의 위치를 조합한다.
    - path.resolve()
      - join()의 경우 그냥 문자열을 합치지만, resole는 오른쪽에서 왼쪽으로 파일 위치를 구성해가며 유효한 위치를 찾는다
      - 만약 결과 값이 유효하지 않으면 현재 디렉토리가 사용된다. 반환되는 위치 값은 항상 absolute URL이다
  - Weppack loader
    - 웹팩은 자바스크립트 파일만 처리가 가능하도록 되어 있다  
    - loader를 이용하여 다른 형태의 웹 자원들을 (img, css, ...) js로 변환하여 로딩 한다
