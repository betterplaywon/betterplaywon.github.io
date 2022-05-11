---
title: "Post: Tranpile과 Compile"
categories:
  - Post Formats
tags:
  - TIL
  - CODING
  - BASIC
---

babel 개념에 대해 공부하던 중 compile과 transpile에 대해 알게 되었다.

이전에는 단순히 `변환한다`라는 개념으로만 알고 있었는데,

둘의 차이는 무엇인지 알고싶어져 포스팅을 하게 되었다.

# Transpile

> 한 언어로 작성된 소스 코드를 `비슷한 수준의 추상화를 가진 다른 언어로 변환`하는 것

- ES6 문법 JS -> ES5 문법 JS (Babel)
- c++ -> c
- TypeScript -> JavaScript
- SCSS -> CSS

# Compile

> 한 언어로 작성된 소스 코드를 `다른언어(주로 저급 언어나 바이너리)로 변환`하는 것

- C -> assembly
- Java -> bytecode


<br>

Reference

[Compiling & Transpiling](https://www.freecodecamp.org/news/what-is-type-erasure-in-typescript/)

