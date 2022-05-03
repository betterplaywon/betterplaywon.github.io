---
title: "Post: push와 replace의 차이점"
categories:
  - Post Formats
tags:
  - TIL
  - CODING
  - BASIC
---

<br>

라우팅 작업 중 history.push와 history.replace 중 하나를 선택할 필요가 있었다.<br>
둘의 차이를 몰라 무엇을 선택해야 할 지 몰라 개념을 정리하며 알게된 것과<br>
추가적인 개념을 공부하기 위해 포스팅했다.<br>

<br>

# 1. push

<br>

- history stack을 활용하여 현재 url 기록(= 라우팅 전 기록)이 라우팅 후에도 남는다.<br>
 
<br>

- jsx에서 사용할수 없고, 어떤 event 안의 함수에서 활용한다.<br>
 
<br>

- 하위(자식) 컴포넌트에서 history객체를 사용하려면,<br>
  props를 통해 부모 컴포넌트로부터 전달받아야 한다.<br>
  BrowerRouter와 Route를 사용한 경우,<br>
  라우팅된 페이지의 최상위 컴포넌트에는 props를 통해 history객체가 자동으로 전달된다.<br>
  
  <br>
  
# 2. replace
  
  <br>
  
  - 현재(= 라우팅 전 기록)의 URL이 이동후에는 남지 않는다.<br>

<br>

  - jsx에서 사용 가능하다.<br>

<br>

  - history 처럼 props로 남기지 않아도 자식 컴포넌트에서 다른 페이지로 라우팅이 가능하다.

<br>

  
