---
title: "Post: MVC Design Pattern"
categories:
  - Post Formats
tags:
  - TIL
  - CODING
  - BASIC
---

개발 관련 정보를 찾다보면 꼭 한 번 씩은 MVC 패턴이라는 단어와 마주하게 된다.<br>
디자인 패턴이란 것은 무엇이며 특히, 오늘 알아볼 MVC 패턴이란 무엇인가에 대해 알아보고자 포스팅을 했다.

# 디자인 패턴이란?
기본적인 설명으로는 "소프트웨어를 설계할때 특정 부분에서 자주 발생하는<br>
고질적인 문제들이 또 발생했을때 재사용할 수 있도록 하는 훌륭한 해결책"<br>
<br>
이라 말하지만 저 말을 내 생각대로 풀어내자면<br>
협업을 진행하는 개발자들이 코드의 패턴을 제작해<br>
문제 해결과 코드의 효율성을 높이는 것이라고 본다.<br>

## MVC 패턴이란
개발을 할 때, 3가지 형태로 역할을 나누어 개발하는 방법론.<br>
Model-View-Controller 의 약자로 사용자가 Controller를 조작하면<br>
Controller는 Model을 통해서 데이터를 가져오고<br>
그 정보를 바탕으로 시각적인 표현을 담당하는 View를 제어해서 사용자에게 전달하게 된다.<br>
<br>


<img src='https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/327/1262.png' width='300px'/>

<br>

### Model
어플리케이션이 “무엇”을 할 것인지를 정의하며<br>
내부 비지니스 로직을 처리하기 위한 역할을 수행한다.<br>
<br>
모델은 컨트롤러가 호출을 하면 DB와 연동하여<br>
데이터와 연관된 비즈니스 로직을 처리하는 역할을 한다.(ex.CRUD)<br>
<br>

### View

View는 유저에게 보여주는 화면(UI)이라 볼 수 있다.<br>
컨트롤러의 명령에 따라 모델에서 도출된 데이터를<br>
사용자에게 화면으로 보여주는 일을 한다.<br>
<br>
MVC에서는 여러개의 View가 존재할 수 있으며<br>
Model에서 받은 데이터는 별도로 저장하지 않는다.<br>
<br>

### Controller
Controller는 Model과 View 사이에서<br>
Model이 데이터를 어떻게 처리할지 알려주는 역할을 담당한다.<br>
<br>
유저로부터 View에 요청 발생<br>
=> Controller는 해당 업무를 수행하는 Model을 호출<br>
=> Model이 해당 업무를 완료하면 다시 결과를 View에 전달하는 흐름을 가진다.<br>

<br>

## MVC 패턴의 5가지 규칙

> 1. Model은 Controller와 View에 의존하지 않아야 한다.

유저가 작동시키려는 데이터만 지닌 채로<br>
View나 Controller에서 다뤄지는 데이터에 대해서는 연관되지 않아야 한다.<br>
또한, 변경이 일어나면 변경 통지에 대한 처리방법을 구현해야만 한다.<br>

<br>

> 2. View는 Model에만 의존해야하고, Controller에는 의존하면 안된다

View 내부에서는 Model과 관련된 코드(객체의 메서드)가 있을 수 있지만,<br>
Controller 관련 코드가 있으면 안 된다.<br>

<br>

> 3. View 가 Model 로부터 데이터를 받을 때는, 사용자마다 다르게 보여주어야하는 데이터만 받아야 한다.

공통으로 보이는 부분은 View 코드로만 처리해주는 것이,<br>
서로 다르게 보이는 부분들은 Model에서 가져와서 보여주는 것이 바람직하다.<br>

<br>

> 4.Controller는 Model과 View에 의존해도 된다.

Controller는 Model과 View 사이에 위치해 명령을 교류하는 곳이므로<br>
Controller 내부에는 Model과 View 코드가 포함될 수 있다.<br>

<br>

> 5. View가 Model로부터 데이터를 받을 때, 반드시 Controller를 통해서 받아야 한다.

Model애서 바로 View를 호출하는 것 또한 안된다.<br>
Model은 로직을 구현하는 목표에 집중해야 하며,<br>
View는 Controller를 통해 받은 데이터만을 활용해 Model 코드를 사용해야 한다.<br>

<br>

## MVC의 한계
> MVC에서 Model과 View는 독립적이지만 의존성을 지닌다

Model과 View는 서로 데이터를 지니지 않아 독립적이라고 할 수 있지만<br>
Controller를 통해 데이터의 교류가 있으므로 의존성을 지니고 있다고 볼 수 있다.<br>
<br>
그렇기 때문에 핸들링하는 서비스나 프로그램이 덩치가 커지면 커질수록<br>
다수의 View와 Model이 Controller를 통해 연결되고,<br>
컨트롤러가 불필요하게 커지는 현상이 발생하게 된다.<br>
<br>
이를  Massive-View-Controller 현상이라고 하며<br>
보완하기 위해 MVP, MVVM, Flux, Redux등의 다양한 패턴들이 고안되었다.<br>


<br>

Reference<br>
[생활코딩 MVC 패턴](https://opentutorials.org/course/697/3828)<br>
[우아한 테크코스 - 제리의 MVC 패턴](https://www.youtube.com/watch?v=ogaXW6KPc8I)<br>
