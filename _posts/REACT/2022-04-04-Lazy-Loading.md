---
title: "Post: Lazy Loading"
categories:
  - Post Formats
tags:
  - REACT
  - CODING
  - BASIC
---


# 1.웹 페이지의 성능 개선 중 하나

효율적으로 import를 하는 것으로도 성능 개선이 가능하다.<br>
모든 import를 한 번에 가져오는 것 보다 필요할 때만 가져와서<br>
import를 해줌으로서 resource 낭비를 줄이기 때문이다.<br>

그 방법으로 lazy loading이라는 것이 있다.<br>

쉬운 말로 해당 컴포넌트로 화면을 렌더링 할 때만 import를 해온다는 의미이다.<br>


## Lazy Loading 적용

Before:
![](https://images.velog.io/images/betterplaywon/post/58334b27-7a2c-4d43-aa8e-40addac12b0c/image.png)


After:
![](https://images.velog.io/images/betterplaywon/post/8cc17df0-904e-4615-a571-496ccc2f8cd2/image.png)

이러한 import 형식을 ES6 Dynamic import 방식이라고 한다.<br>

### ❗ 주의
import 순서에 따라 오류가 발생할 수 있다.<br>
이런 경우에는 Dynamic import를 import의 최하단으로 내려주면 해결이 된다.<br>


## 해당 컴포넌트가 전부 렌더링되지 않은 경우
인터넷 환경이 느리거나 컴퓨터 상태가 좋지 않은 경우에는 Detail 컴포넌트를<br>
띄우는 데 시간이 걸려 하얀 화면만 보고 있는 경우도 존재할 것이다.<br>
그런 경우에 대비해 로딩 화면을 미리 하나 만들어 놓을 수 있다.<br>

![](https://images.velog.io/images/betterplaywon/post/74f99bed-1484-4c4c-8a30-acdb408e42ec/image.png)

1. 선언 후 Suspense 태그로 해당하는 컴포넌트를 감싸준다.<br>

2. Suspense 태그에 속성으로 fallback을 사용해 로딩 전까지 나올 HTML을 작성해준다.<br>


