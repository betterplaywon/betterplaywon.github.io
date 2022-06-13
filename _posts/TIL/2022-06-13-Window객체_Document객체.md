---
title: "Post: Window 객체와 Document 객체"
categories:
  - Post Formats
tags:
  - TIL
  - CODING
  - BASIC
---

<br>

업무 도중 window 객체를 사용한 애니메이션을 구현해야 할 일이 발생하였고,

웹에서는 애니메이션이 동작하지만 모바일웹과 앱에서는 애니메이션이 동작하지 않았다.

결과적으로 document를 사용함으로서 해결하였지만 둘의 차이를 명확히 알고싶어져

포스팅을 하게 되었다.

<br>
<br>

# window 객체

> 브라우저 객체 모델의 최상위 객체

<br>

브라우저 객체 모델(BOM : Browser Object Model) 은 웹브라우저의 탭 혹은 창의 모델.

웹브라우저 객체 모델의 최상위 객체가 window 객체이다.

window 객체는 현재 웹브라우저의 창이나 탭을 표현한다.

window로 접근 가능.


<br>
<br>

# Document 객체

> 문서 객체 모델의 최상위 객체
 
<br>

문서 객체 모델(DOM : Document Object Model) 은 현재 웹페이지의 모델을 생성하며

이러한 문서 객체 모델의 최상위 객체가 document 객체이다.

document 객체는 전체 페이지를 표현한다.

document 객체는 window 객체의 속성이기도 하다.

<br>
<br>

# 헷갈렸던 부분

<br>

```js
// 문제 발생 코드 예시

window.addEventListener('load',function());
window.addEventListener('scroll',function());
```

<br>

웹에서는 window로 동작했지만 모바일웹과 앱(줄여서 모바일)에서는 window로 접근할 수 없었다.

선임 개발자분에게 여쭈어 `document를 통해 접근`하여 해결할 수 있을 거 같다는 말씀을 듣고 적용해 문제는 해결했지만

확실하게 왜 해결이 되었는지에 대해 이해하지 못했다.

그 이유로 추정되는 것이 `모바일에서는` 이벤트가 적용되는 태그 위에 `하나의 header 태그가 추가`되어졌다는 것이다.

한 `depth가 추가됨`에 따라 `기존 window`를 통해 작동하던 것이 어떠한 이유로 `동작하지 않게 되어졌다`는 것이지만

여전히 명확한 이유는 파악하지 못했다.

단지 위와 같은 문제가 발생한다면 window로 접근하는 것이 아닌

`분기 처리`를 통해 `window를 사용할 때와 document를 사용할 때로 구분`해야 한다는 점을 배운 상태다.

```js
// 문제 해결 코드 예시

if(모바일 환경일 때) {
document.getelementById('OOO').addEventListener('load',function());
document.getelementById('OOO').addEventListener('scroll',function());
} else{
window.addEventListener('load',function());
window.addEventListener('scroll',function());
}
```

<br>
















