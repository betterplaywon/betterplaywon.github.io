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

라우팅 작업 중 enlfh history.push와 history.replace 중 하나를 선택할 필요가 있었다.<br>
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
  
  - 현재의 url 기록이 이동 후 남지 않는다.<br>

<br>

  - jsx에서 사용 가능하다.<br>

<br>

  - history 처럼 props로 남기지 않아도 자식 컴포넌트에서 다른 페이지로 라우팅이 가능하다.

<br>

### * push와 replace를 하나로, useNavigate
React Router dom V6로 업그레이드 되며 기존의 useHistory 대신<br>
useNavigate를 사용할 수 있게 되었다.<br>
개인적인 생각으로는 push와 replace로 역할을 명확히 보여줄 수 있는 것이 낫지 않을까라는 생긱이다<br>



<br>

# 3. Redirect
> 브라우저에게 다른 URL을 지시할 수 있는 것

-현재의 url 기록이 이동 후 남지 않는다.<br>

<br>

-react-router-dom의 Redirect를 import 해온다.<br>

<br>

-jsx에서 사용한다. state 삼항연산자로 주로 사용한다.<br>

<br>

-history 처럼 props로 남기지 않아도 자식 컴포넌트에서 다른 페이지로 이동 가능하다.<br>

<br>

# 4. Link
- react-router-dom의 Link를 import해온 후 사용된다.<br>

<br>

- react-router-dom 에서 제공하는 Link 컴포넌트는 DOM 에서 a 태그로 변환.<br>

<br>

- 현재 경로가 history 객체에 남는다<br>

<br>

*현재 url 기록을 남기지 않으려면 <Link to ="/이동경로" replace={true />로 작성)<br>

<br>

 ### * a 태그와 Link 차이
a : 외부 프로젝트로 이동하는 경우<br>
Link : 프로젝트 내에서 페이지 전환하는 경우<br>

