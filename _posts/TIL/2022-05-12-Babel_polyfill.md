---
title: "Post: Babel과 polyfill"
categories:
  - Post Formats
tags:
  - TIL
  - CODING
  - BASIC
---

<br>

Transpile과 Compile을 공부하며 Babel을 접하게 되었다.

프로젝트 세팅을 할 때마다 Babel을 사용하긴 했었지만

약간의 개념만 갖춘 상태였고 polyfill과의 차이는 무엇인지,

현재 어떤 변화가 있는지 파악하기 위해 포스팅을 했다.

<br>

# Babel

> ECMAScript 2015+ 코드를 현재 및 이전 버전의 브라우저 또는 환경에서
> 
> 이전 버전과 호환되는 JavaScript 버전으로 변환하는 데 주로 사용되는 도구

<br>

babel은 ES6+ 코드를 브라우저에서 해석할 수 없기 때문에

브라우저의 환경과 호환되는 `JavaScript로 변환해주는 Transpile 역할을 수행`한다.

Chrome이나 Firefox 등의 브라우저에서는 ES6를 지원하기에 babel을 사용하지 않아도 되겠지만

ES6를 지원하지 않는 브라우저를 사용하는 유저가 존재할 수 있기에 babel이 필요하고,

새로운 버전의 ES가 출시된다면 babel을 통해 브라우저에 새 ES가 지원되지 않아도

사용해볼 수 있기에 babel을 사용해줘야 한다.

<br>

# Polyfill

>  구형 브라우저에서 사용되지 않았던 기술들에 대한 코드 정보를
>  
>  구형 브라우저에서 동작할 수 있게 돕는다

<br>

babel-polyfill은 ES6+에서 새롭게 추가된 Promise, WeakMap와 같은 내장객체나

Array.from, Object.assign와 같은 `정적 메소드`를 `구형 브라우저에서도 작동할 수 있도록 변환`해주는 도구다.

쉽게 말해 ES6+에서 새롭게 추가된 객체나 메소드들을 구형 브라우저에도 작동할 수 있도록 변환해준다는 것이다.

<br>

## Babel-Polyfill

> ES6+에서 새롭게 추가된 객체들을 구형 브라우저에서도 작동할 수 있도록 변환해주는 역할을 수행

babel에 기본적으로 babel-polyfill이 포함되어있지만

`Babel v7.4.0`부터 @babel/polyfill 패키지는 사용되지 않고

대신 ECMAScript 기능을 대체하는 `core-js/stable`,  제너레이터 함수 기능을 대체하는 `regenerator-runtime/runtime을 사용`한다.


<br>

Reference

[Babel ref](https://babeljs.io/docs/en/index.html)
[Babel-polyfill ref](https://babeljs.io/docs/en/babel-polyfill)
[polyfill ref](https://yamoo9.gitbook.io/webpack/react/create-your-own-react-app/configure-polyfills)

