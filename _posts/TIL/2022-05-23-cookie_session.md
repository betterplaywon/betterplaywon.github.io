---
title: "Post: cookie & Session"
categories:
  - Post Formats
tags:
  - TIL
  - CODING
  - BASIC
---

<br>

인증과 인가를 공부하며 쿠키와 세션에 대해 정확히 짚고 넘어가야겠다는 생각이 들었다.

<br>

# 1. 쿠키와 세션의 사용 이유

> HTTP 프로토콜의 특징이자 약점을 보완하기 위해서 사용

<br>

 ## 1. Connectionless 프로토콜 (비연결지향)
    클라이언트가 서버에 요청(Request)을 했을 때,
    그 요청에 맞는 응답(Response)을 보낸 후 연결을 끊는 처리방식이다.
    - HTTP 1.1 버전에서 연결을 유지하고, 재활용 하는 기능이 Default 로 추가되었다.
    (keep-alive 값으로 변경 가능)

 ## 2. Stateless 프로토콜 (상태정보 유지 안함)
    클라이언트의 상태 정보를 가지지 않는 서버 처리 방식이다.
    클라이언트와 첫번째 통신에서 데이터를 주고 받았다 해도,
    두번째 통신에서 이전 데이터를 유지하지 않는다.


현실적으로는 데이터 유지가 필요한 경우가 많다.

정보가 유지되지 않으면, 매번 페이지를 이동할 때마다 로그인을 다시 하거나,

상품을 선택했는데 구매 페이지에서 선택한 상품의 정보가 없거나 하는 등의 일이 발생할 수 있다.

<br>

따라서, `Stateless 경우를 대처`하기 위해서 `쿠키와 세션을 사용`한다.

쿠키와 세션의 차이점은 크게 상태 정보의 저장 위치이다.

`쿠키는 '클라이언트(=로컬PC)'에 저장`하고, `세션은 '서버' 에 저장`한다.

서버와 클라이언트가 통신을 할 때 통신이 연속적으로 이어지지 않고 한 번 통신이 되면 끊어진다.

따라서 서버는 `클라이언트가 누구인지 계속 인증`을 해줘야 한다. 하지만 그것은 매우 귀찮고 번거로운 일이다. 

또한 웹페이지의 `로딩을 느리게 만드는 요인`이 되기도 한다. 그런 번거로움을 해결하는 방법이 바로 쿠키와 세션이다.

정리하면, `클라이언트와 정보 유지`를 하기 위해 사용하는 것이 `쿠키와 세션`이다.

<br>

# 2. 쿠키(= Cookie)

> HTTP의 일종으로 사용자가 어떠한 웹 사이트를 방문할 경우,
> 
> 그 사이트가 사용하고 있는 서버에서 사용자의 컴퓨터에 저장하는 작은 기록 정보 파일이다.
> 
> HTTP에서 클라이언트의 상태 정보를 클라이언트의 PC에 저장하였다가 필요시 정보를 참조하거나 재사용할 수 있다.

<br>

## 쿠키의 특징

1. 이름, 값, 만료일(저장기간), 경로 정보로 구성되어 있다.

2. 클라이언트에 총 300개의 쿠키를 저장할 수 있다.

3. 하나의 도메인 당 20개의 쿠키를 가질 수 있다.

4. 하나의 쿠키는 4KB(=4096byte)까지 저장 가능하다.

<br>

## 쿠키의 동작 순서

클라이언트가 페이지를 요청한다. (사용자가 웹사이트에 접근)

-> 웹 서버는 쿠키를 생성한다.

-> 생성한 쿠키에 정보를 담아 HTTP 화면을 돌려줄 때, 같이 클라이언트에게 돌려준다.

-> 넘겨받은 쿠키는 클라이언트가 가지고 있다가(로컬 PC에 저장) 다시 서버에 요청할 때 요청과 함께 쿠키를 전송한다.

-> 동일 사이트 재방문 시 클라이언트의 PC에 해당 쿠키가 있는 경우, 요청 페이지와 함께 쿠키를 전송한다.

<br>

### 사용 예시
```
방문 사이트에서 로그인 시, "아이디와 비밀번호를 저장하시겠습니까?"

팝업창을 통해 "오늘 이 창을 다시 보지 않기" 체크
```

<br>
<br>

# 3. 세션(= Session)

일정 시간 동안 같은 사용자(브라우저)로부터 들어오는

`일련의 요구를 하나의 상태`로 보고, 그 `상태를 유지`시키는 기술이다.

여기서 일정 시간은 방문자가 웹 브라우저를 통해 `웹 서버에 접속한 시점`부터

`웹 브라우저를 종료하여 연결을 끝내는 시점`을 말한다.

즉, 방문자가 웹 서버에 접속해 있는 상태를 하나의 단위로 보고 그것을 세션이라고 한다.

<br>

## 세션의 특징

1. 웹 서버에 웹 컨테이너의 상태를 유지하기 위한 정보를 저장한다.

2. 웹 서버의 저장되는 쿠키(=세션 쿠키)

3. 브라우저를 닫거나, 서버에서 세션을 삭제했을때만 삭제가 되므로,
   쿠키보다 비교적 보안이 좋다.
   
5. 저장 데이터에 제한이 없다.

6. 각 클라이언트 고유 Session ID를 부여한다.

   Session ID로 클라이언트를 구분하여 각 클라이언트 요구에 맞는 서비스 제공

<br>

## 세션의 동작 순서

클라이언트가 페이지에 요청한다. (사용자가 웹사이트에 접근)

-> 서버는 접근한 클라이언트의 Request-Header 필드인 Cookie를 확인하여, 클라이언트가 해당 session-id를 보냈는지 확인한다.

-> session-id가 존재하지 않는다면 서버는 session-id를 생성해 클라이언트에게 돌려준다.

-> 서버에서 클라이언트로 돌려준 session-id를 쿠키를 사용해 서버에 저장한다.

-> 클라이언트는 재접속 시, 이 쿠키를 이용해 session-id 값을 서버에 전달

<br>

### 사용 예시

```
화면을 이동해도 로그인이 풀리지 않고 로그아웃하기 전까지 유지
```

<br>
<br>

# 4. 쿠키와 세션의 차이

<br>

> 1. 사용자의 정보가 저장되는 위치가 다르다.

<br>

쿠키는 서버의 자원을 전혀 사용하지 않으며, `세션`은 `서버의 자원`을 사용한다.

<br>

> 2. 보안성

<br>

`보안 면에서 세션이 더 우수`하며, 쿠키는 클라이언트 로컬에 저장되기 때문에

변질되거나 request에서 스니핑 당할 우려가 있어서 보안에 취약하지만

세션은 쿠키를 이용해서 session-id만 저장하고 그것으로 구분하여 서버에서 처리하기 때문에 비교적 보안성이 높다.

<br>

> 3. 만료 기간과 유지

<br>

`쿠키`는 만료기간이 있지만 파일로 저장되기 때문에 `브라우저를 종료`해도 `정보가 유지`될 수 있다.

또한 만료기간을 따로 지정해 쿠키를 삭제할 때까지 유지할 수도 있다.

반면에 `세션`도 만료기간을 정할 수 있지만, `브라우저가 종료`되면 `만료기간에 상관없이 삭제`된다.

<br>

> 4. 속도

<br>

`속도 면`에서 `쿠키가 더 우수`하며,

쿠키는 쿠키에 정보가 있기 때문에 서버에 요청 시 속도가 빠르고

세션은 정보가 서버에 있기 때문에 처리가 요구되어 비교적 느린 속도를 낸다.



<br>

#### Reference

[쿠키와 세션의 특징, 차이](https://hahahoho5915.tistory.com/32)

[쿠키와 세션의 특징, 차이 02](https://devuna.tistory.com/23)

[쿠키와 세션의 특징, 차이 03](https://dev-coco.tistory.com/61)

[쿠키와 세션의 특징, 차이 04](https://brunch.co.kr/@jinyoungchoi95/1)

[쿠키와 세션의 특징, 차이 05](https://seoramyeon.tistory.com/48)

[쿠키와 세션의 특징, 차이 06](https://tecoble.techcourse.co.kr/post/2021-05-22-cookie-session-jwt/)
