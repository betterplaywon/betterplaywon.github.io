---
title: "Post: event target과 event  currenttarget"
categories:
  - Post Formats
tags:
  - JS
  - CODING
  - BASIC
---

함께 공부했던 개발자 분과 이야기를 나누다<br>
target과 currentTarget의 차이에 대해 알고있냐는 질문을 받았다.<br>
바로 답할 수 없었던 게 부끄러워 정리를 하게 되었다.<br>


# 예시
![image](https://user-images.githubusercontent.com/78709765/161971035-25f97893-be38-43cb-a706-a98bf09648ea.png)<br>
버튼을 클릭했을 떄와 텍스트를 클릭했을 때의 target과 currentTarget을 비교해봤다.<br>
<br>
![image](https://user-images.githubusercontent.com/78709765/161974053-007ad77d-8e3c-4b57-8f1f-bf0032dd3ba8.png)<br>

빨간 선을 기준으로 위가 텍스트를 클릭했을 때,<br>
아래가 버튼을 클릭했을 때이다.<br>

## click 이벤트의 대상에 따라 달라지는 결과
텍스트를 클릭했을 때
event.target이 텍스트, currentTarget이 버튼이고<br>
버튼을 클릭했을 때
event.target이 버튼, currentTarget이 버튼인 것을 확인할 수 있다<br>

## 알 수 있는 것
이벤트 동작의 대상에 따라 반응한다는 것이다.<br>
event.target은 이벤트가 발생한 요소를 반환,<br>
event.currentTarget은 이벤트를 달아놓은 요소를 반환한다.<br>

쉽게 이해하자면 event.target은 현재 어느 곳에서 이벤트가 발생했는지를,<br>
event.currentTarget은 이벤트가 달려있는 곳을 말해준다고 이해할 수 있다.

