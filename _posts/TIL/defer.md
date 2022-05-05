---
title: "Post: SEO에서의 defer"
categories:
  - Post Formats
tags:
  - TIL
  - CODING
  - BASIC
---

<br>

이전까지는 SEO에 대해 관심이 없었지만

기업 입장에서 서비스를 바라볼 때 필수로 신경써줘야 하는 부분이

바로 SEO라는 것을 알게 되었고, SEO 점수 개선에 대한 방법 중

defer를 통한 성능 개선이 가능하다는 점을 알게 되었다.

# Defer란

defer 는 '미루다, 연기하다' 라는 의미를 가진 단어로써

`html 및 css 보다 늦게 자바스크립트 구문을 호출하는 방법`이다.

HTML 파싱과 동시에 비동기로 JavaScript 파일을 로드한다는 것이다

=> **HTML 파싱이 완료된 후**, JavaScript 코드의 실행이 시작된다.
  
 <img src='https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbWt818%2Fbtq8uKiaQQW%2Fjm06m4WqDOOaQ8yAmSfVFk%2Fimg.png' width='800px'/>
  
  <br>
  
# defer 속성이 추가된 경우의 실행

defer 속성은 HTML 구문 분석이 완전히 완료되면 스크립트 파일을 실행하도록 브라우저에 지시한다.
  

  비동기적으로 로드된 스크립트와 마찬가지로, HTML 구문 분석이 실행되는 동안 파일을 다운로드 할 수 있다.

그러나 HTML 구문 분석이 완료되기 전에 스크립트 다운로드가 완료 되더라도 구문 분석이 완료 될 때까지

스크립트는 실행되지 않는다. 또한, **async와는 다르게 호출된 순서대로 실행된다.**
 
 <img src='https://blog.asamaru.net/res/img/post/2017/05/script-async-defer-3.png' width='700'/>
 
 `<script>` 엘리먼트에 `defer` 속성을 활용하면,

브라우저에서 자바스크립트 파일을 내려받는 시간을 최소화할 수 있게 된다.
  
 ```
 ex)
<script defer src="script.js">
 ```
  <br>
  
# defer 적용
  
  적용 전
  
  <img width="667" alt="defer 전" src="https://user-images.githubusercontent.com/78709765/166926772-566b2d51-bee2-4057-9adb-c2d032f0d9af.png">

  적용 후
  
  <img width="665" alt="defer 후" src="https://user-images.githubusercontent.com/78709765/166926796-2a353e9d-984b-43bb-82f8-6d2d6e8bdc38.png">

  <br>
  
완료 시점이 약 3초 정도 앞당겨진 것을 확인할 수 있다.

이는 JS 파일이 로드되는 시점이 당겨짐에 따라 유저가 서비스 기능을 사용하는 데에 있어

문제 없이 사용할 수 있는 방향으로 향상된다는 것으로 비춰진다.

최근에 프로젝트에서 parcel2로 마이그레이션하며 defer가 자동으로 추가되어져

내가 적용할 필요가 없었지만 이전 번들러인 parcel을 사용할 때 defer를 직접 입력해보며

성능 개선에 영향을 미치는 것을 직접 확인해 성능 개선이 주는 효과와 필요성을

깨달을 수 있는 좋은 경험이 되었다.
    
  
  <br>
  
  Reference
  
  <br>
  
  [defer 참고 blog 01](https://curryyou.tistory.com/342)
  
  [defer 참고 blog 02](https://ko.javascript.info/script-async-defer)
  
