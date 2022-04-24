---
title: "Post: Flux Pattern"
categories:
  - Post Formats
tags:
  - TIL
  - CODING
  - BASIC
---

MVC pattern을 공부하며 리액트에도 MVC 패턴이 적용되는건지 서칭하던 중<br>
Flux Pattern을 보고선 포스팅을 하게 됐다.

# Flux Pattern의 등장 계기

> MVC pattern의 단점을 보완한 새로운 pattern

<br>

MVC는 controller를 통해 model의 데이터를 조회, 갱신하고 view를 통해<br>
최종적으로 화면에 그려내는 패턴을 지녔다.<br>
<br>
규모가 작을 때는 상관이 없었지만, 크기가 큰 프로젝트를 진행 시 발생하는 문제점이 있었다.<br>
프로젝트의 사이즈가 커질수록 데이터의 흐름을 파악하는 것이 힘들다는 것이다.<br>

하나의 controller에 많은 view와 model이 연결되어져 컨트롤러의 크기가 커지게 되고<br>
model 업데이트 -> view 업데이트 -> 다른 model 업데이트 -> 다른 view 업데이트의 흐름처럼<br>
서로 영향을 미치는 <strong>양방향 데이터 흐름</strong>으로 수많은 버그가 발생하게 될 수 있다는 문제였다.<br>
<br>
<img src='https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FALrHe%2FbtqBTMSuHfN%2FZlW9i9ET34e90APgCRChk1%2Fimg.png' width='600px'/>

<br>

양방향 데이터 흐름으로 발생하는 문제를 해결하기 위해<br>
페이스북은 단방향 데이터 흐름인 flux를 만들어냈다.<br>

<br>

# Flux의 특징
> 지정된 데이터 방향 설정을 통해 단방향 데이터 흐름을 만들어낸다.

<br>

<img src='https://miro.medium.com/max/1400/0*1IFslbZI-7Id2rOE.png' width='600px'/>

<br>

## Flux 단어 설명

### 1. Action
> 이벤트 발생 시, 이벤트가 발생했다는 것을 Action 정보를 담는 객체로 만들어 Dispatcher에 전달하는 역할을 한다.

Dispatcher에서 콜백 함수가 실행 되면 Store가 업데이트 되게 되는데,<br>
이 콜백 함수를 실행 할 떼 데이터가 담겨 있는 객체가 인자로 전달 되어야 한다.<br>
이 전달 되는 객체를 Action이라고 한다.
<br>

### 2. Dispatcher
> Flux의 모든 데이터 흐름을 관리하는 허브 역할.

들어오는 Action 객체 정보를 받아 원하는 기능을 정하는 곳.<br>
if문이나 switch 문으로 들어오는 Action 객체를 보고,<br>
등록된 콜백 함수를 실행하여 Store에 데이터를 전달한다.<br>

<br>

### 3. Store
> 어플리케이션의 모든 상태 변경은 Store에 의해 결정.

Store를 Dispatcher와 연결해 Store에 접근할 수 있도록 callback 명령을 제공할 수 있다.<br>
또한 여기서 가지고 있는 상태에 View가 접근하고, 상태가 변경되면 View에서도 이를 반영한다.<br>


### 4. View
> 화면에 나타내는 것 이외에 자식 View로 데이터를 전달하는 Controlloer view의 역할도 수행.

Store에서 어떤 이벤트(변경 등)가 발생하면 View는 변경된 점을 가져오고, 이를 바탕으로 화면을 다시 랜더링한다.

#### * Controlloer view
변화된 상태나 Dispatcher 등을 제공하기 위해서 상위 View가 하위 View를 감싸는 형태로 존재.

<br>

Reference<br>
[Flux 만화 안내](https://bestalign.github.io/translation/cartoon-guide-to-flux/)<br>
[Flux 블로그](https://beomy.tistory.com/44)<br>

