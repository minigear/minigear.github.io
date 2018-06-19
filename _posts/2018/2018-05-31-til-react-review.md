---
layout: "post"
title: "TIL react review 2018-05-31"
date:   "2018-05-31 09:47"
categories: []
permalink: /2018/:year/:month/:day/:title/
tags: []
comments: true
---
복기
1. component를 만들었을 때 include하는 css의 파일 경로를 제대로 설정하지 않으면 component가
export되지 않아 사용하는 측에서 찾을 수 없다고 에러를 발생 시킨다
2. stx에서 img 태그를 줄때는 alt를 설정해 줘야 한다 경고 발생한다   
3. component에서 넘겨받은 값의 type을 체크할 때 prop-types를 사용한다  
[propTypes 사용](https://reactjs.org/docs/typechecking-with-proptypes.html)  
설치
$ npm install --save prop-types

```javascript
import PropTypes from 'prop-types';

class MyComponent extends React.Component {
  render() {
    // This must be exactly one element or it will warn.
    const children = this.props.children;
    return (
      <div>
        {children}
      </div>
    );
  }
}

MyComponent.propTypes = {
  children: PropTypes.element.isRequired
};
```
4. state 사용하기
5. componentDidMount
6. fetch
7. dummy component: parameter를 넘길 때 {}객체화 시켜서 넘겨야 한다 
