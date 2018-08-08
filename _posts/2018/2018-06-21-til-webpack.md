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
  - Plugin 소개 : 플러그인은 파일별 커스텀 기능을 사용하기 위해서 사용한다
    - 플러그인과 로더의 차이 : 로더는 빌드과정에 관여하고 플러그인은 빌드 후 output 과정에 관여한다  
    - Provide plugin: 모든 모듈에서 사용할 수 있도록 해당 모듈을 변수로 변환 한다
    - Defined plugin:
      - webpack 번들링을 시작하는 시점에 사용 가능한 상수들을 정의.
      - 일반적으로 개발계&테스트계에 따라 다른 설정을 적용할 때 유
    - Manifest plugin: 번들링시 생성되는 코드(라이브러리)에 대한 정보를 json 파일로 저장하여 관리  
  - Webpack Resolve
    - Webpack의 모듈 번들링 관점에서 봤을 때, 모듈 간의 의존성을 고려하여 모듈을 로딩해야 한다
    - 모듈을 어떤 위치에서 어떻게 로딩할지를 정의한 것
    - webpack.config.js 에서 resolve - alias를 통하여 경로 명을 정의 하여 코드를 import할 때 경로명을 줄일 수 있다    
    ```javascript
    resolve: {
       alias: {
           Vendor: path.resolve(__dirname, './app/vendor/')
       }
    }
    ```  

    - webpack.config.js에서 plugin으로 ProvidePlugin를 사용하여 모듈을 직접 import하지 않고도 전역에서 사용할 수 있다  
    ```javascript
    plugins: [
      new webpack.ProvidePlugin({
        $: 'jquery'
      })
    ]
    ```  

## 3. Webpack 빌드를 위한 서버 구성  
  - webpack-dev-server : webpack 자체에서 제공하는 개발 서버이고 빠른 리로딩 기능 제공  
  - webpack-dev-middleware : 서버가 이미 구성된 경우에는 webpack을 미들웨어로 구성하여 서버와 연결  

### 3-1. Webpack Dev Server
  - 페이지 자동 고침을 제공하는 webpack 개발용 node.js 서버  

**설치 및 실행**  
  - dev-server 설치  
  ```
    $ npm install --save-dev webpack-dev-server
  ```

  - dev-server 실행
  ```
    $ node_modules/.bin/webpack-dev-server
  ```

  - package.json에 실행 명령어 등록
  ```
  "scripts": {
  "start:dev": "webpack-dev-server"
  }
  ```
  - package.json에 스크립트 추가했을 때의 실행 방법   
  ```
  $ npm run start:dev
  ```   
  참고: https://www.npmjs.com/package/webpack-dev-server  


### 3-3. Webpack 명령어
  - webpack: 웹팩 빌드 기본 명령어 (주로 개발용)
  - webpack -p : minification 기능이 들어간 빌드(주로 배포용)
  - webpack -watch(-w): 개발에서 빌드할 파일의 변화를 감지
    ```
    $ webpack --progress --watch
    ```
  - webpack -d : sourcemap 포함하여 빌드
  - webpack --dispaly-error-details: error 발생시 디버깅 정보를 상세히 출력
  - webpack --optimize-minimize --define process.env.NODE_ENV="'production'" : 배포용

개발자 도구 연동  
- 브라우저에서 webpack 으로 컴파일된 파일을 디버깅 하기 어렵다  
- sourcemap설정을 추가해주면 원래 파일 구조에서 디버깅이 가능해 진다  
```
  module.export= {
    ...
    devtool: "#inline-source-map"
  }
```

Gulp 연동  
- Gulp와 Webpack 모두 Node.js 기반이기 때문에 통합해서 사용하기 쉽다  
```
var gulp = require('gulp');
var webpack = require('webpack-stream');
var webpackConfig = require('./webpack.config.js');

gulp.task('default', function(){
  return gulp.src('src/entry.js').
  pipe(webpack(webpackConfig)).
  pipe(gulp.desc('dist/'));
  });
```

Hot Module Replacement  
- 웹 앱에서 사용하는 JS 모듈들을 갱싱할 때 화면의 새로고침 없이 뒷 단에서 변경 및 삭제 기능을 지원
- 공식 가이드에는 React 를 기준으로 사용법이 작성되어 있다  
