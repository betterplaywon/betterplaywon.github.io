---
title: "Post: Web Socket"
categories:
  - Post Formats
tags:
  - TIL
  - CODING
  - BASIC
---

<br>

`회사 프로젝트를 진행 중`, `실시간으로 채팅`을 주고받을 수 있도록

`socket.io`를 사용한 기능에 수정이 필요했다.

나는 실시간 통신이 가능하다는 것 이외의 다른 점은 전혀 모르고 있었고,

웹소켓이 뭔지도 모르고 기능 오류를 수정할 수는 없기에

웹소켓에 대한 학습 내용을 정리하며 포스팅을 해야겠다는 생각이 들었다.

<br>

# WebSocket이 생겨난 이유

> 양방향 통신이 필요한 현대의 서비스에 대응하기 위함

<br>

`기존 HTTP 통신`은 요청에 대한 응답만 해주는 `단방향 통신`이었다.

한 번만 통신하고 종료되는 방식으로도 과거의 서비스는 운영이 가능했지만

`실시간 채팅이나 거래` 등 빠르게 이뤄지는 `현대의 서비스`는

기존의 HTTP 통신으로 운영하기엔 어려움이 있었다.

예를 들어 현대의 서비스 중 하나의 기능으로

3초마다 새로운 가격 정보를 서버로부터 가져와 유저에게 보여주려면

3초마다 서버에 http 요청을 보내고 받아야 하는데, 효율성이 무척 떨어진다.

이 효율성을 메꿔주기 위해 등장한 것이 WebSocket이다.

<br>

# 웹소켓 이전의 비슷한 기술

## 1. Polling

> http request를 서버로 계속 날려서 이벤트 내용을 전달받는 방식

<br>

- 클라이언트가 request를 지속적으로 보낸다 -> 클라이언트가 많아지면 서버의 부담이 증가한다.

- 위의 과정을 통해 `불필요한 request와 connection이 생성`되며
  
  http request connection을 맺고 끊는것 자체가 부담이 많은 방식이다.

- 실시간이라 부를 만 한 정도의 응답이 아니다.

<br>

## 2. Long Polling

> 서버 측에서 접속을 열어두는 시간을 길게하는 방식.

<br>

- 서버에 request를 보낸다 -> 서버에서 클라이언트로 전달할 event가 생겨 response를 받을 때 까지 연결이 종료되지 않는다.

- response를 받으면 `다시 request를 보내` 서버의 response를 기다린다.

- 대량의 request가 발생할 경우에는 polling 과 같이 서버의 부담이 증가한다.

<br>

## 3. Streaming

> 서버에 request를 보내고 끊기지 않은 연결상태에서 끊임없이 데이터 수신

<br>

- 서버에서 response를 보내고 다시 request를 안 보내도 연결되어있는 상태이니 웹 소켓과 비슷해 보일 수 있지만 아니다!
- 클라이언트에서 서버로의 데이터 송신이 어렵다.(하나의 TCP 포트를 사용하기 떄문)

<br>

## 4. Server-sent Event

> HTTP 통신을 종료하지 않고 유지 가능한 방식

<br>

- `지속적인 데이터 수신만 가능`하다(= 데이터 request가 불가하다)

<br>

### 이전 기술들의 공통점

WebSocket 등장 이전의 방법들은 모두 `HTTP를 통해 통신`을 하며

Request, Response 둘 다 `Header가 불필요하게 크다`는 공통점이 존재한다.

<br>

---

# WebSocket

> HTTP 기반으로 하면서 HTTP의 문제점을 해결하는 것을 목표로 나온 기술

<br>

이전 기술에서의 단점을 메꿔줄 수 있는 것이 바로 웹소켓이다.

- TCP 경로를 기반으로 양방향 통신이 가능하다.

```
user가 서버에 웹소켓을 사용한 http 요청을 보낸다

→ 서버에서 데이터를 받고 http 요청을 웹소켓으로 업그레이드 해줄 수 있다.

→ 양방향 통신이 가능해진다.
```

- 현재 인터넷 환경(HTML5)에서 많이 사용된다.

<br>

# Web Socket의 특징

## 1. 양방향 통신

- 데이터 송수신을 동시에 처리할 수 있는 통신 방법

- 클라이언트와 서버가 서로에게 원할 때 데이터를 주고받을 수 있다

<br>

## 2. 실시간 네트워킹

- 웹 환경에서 `연속된 데이터를 빠르게 노출` (ex. 주식, 채팅)

- 여러 단말기에 빠르게 데이터를 교환

<br>

# Web Socket 동작 방법

> 서버와 클라이언트간의 웹소켓 연결은 HTTP프로토콜을 통해 이루어진다.

<br>

<img src='https://t1.daumcdn.net/cfile/tistory/2672AD3954D72C121E' width='800px'/>

<br>

웹소켓으로 양방향 통신을 하기 위해서는 HTTP 통신으로 request 내부에 웹소켓 관련 데이터를 실어보내야 한다.

<br>

## 1. Client(= 웹소켓 핸드쉐이킹에 대한 요청)

연결 수립 과정은 HTTP 프로토콜을 사용한다.

HTTP 버전은 1.1 이상

반드시 GET 메서드를 사용해야 한다.

<br>

#### Host 

웹 소켓 서버의 주소

<br>

#### Upgrade

현재 클라이언트, 서버, 전송 프로토콜 연결에서 `다른 프로토콜로

업그레이드 또는 변경하기 위한 규칙`

(업그레이드가 웹 소켓이라면 다음 프로토콜부터는 웹소켓으로 진행하겠다는 의미이다)

<br>

#### Connection
upgrade 헤더 필드가 명시되었을 경우 송신자는

`반드시 upgrade 옵션을 지정한 Connection 헤더 필드도 전송`

(업그레이드와 커넥션을 지정해주지 않으면 클라이언트와 서버 연결이 안된다)

<br>

#### sec-Websocket-key

길이가 16바이트인 임의로 선택된 숫자를 `base64로 인코딩` 한 값.

<br>

#### Origin

클라이언트로 웹 브라우저를 사용하는 경우에 필수항목으로, `클라이언트의 주소를 의미`

<br>

#### Sec-Websocket-Protocol

클라이언트가 요청하는 여러 `서브 프로토콜`을 의미.

공백 문자로 구분되며 순서에 따라 우선권이 부여

서버에서 여러 프로토콜 혹은 프로토콜 버전을 나눠서 서비스할 경우 필요한 정보

<br>

## 2. 서버(= 웹 소켓 핸드쉐이킹에 대한 응답)

<br>

#### HTTP/ 1.1 101 Switching Protocols

101 Switching Protocols가 Response로 오면 웹소켓이 연결

Upgrade: Websocket

Connection: Upgrade

#### Sec-Websocket-Accept : af345345jbnsdfkjdewuj34kjdfdf= 

: 클라이언트로부터 받은 Sec-Websocket-Key를 사용하여 계산된 값

Sec-Websocket-Accept 부분이 클라이언트에서 계산한 값과 일치하지 않으면 연결 수립 X

<

## 3. 핸드쉐이크가 완료가 된 이후(= 통신이 완료된 이후)

- 이 때부터는 통신 프로토콜이 ws or wss로 변경된다.

(wss는 데이터 보안을 위해 SSL을 적용한 프로토콜)

- 주고 받는 데에 있어 `사용하는 단위는 Message`이다.

Message란 `여러 frame이 모여서 구성`하는 `하나의 논리적 메세지 단위`

frame : Communication에서 가장 작은 단위의 데이터. 작은 헤더 + payload로 구성되어있다.

- 웹소켓 통신에 사용되는 데이터는 `UTF8 인코딩`

ex) 0x00 ( 보내고 싶은 데이터를 사이에 넣고) 0xff 이런 식으로 데이터를 주고 받게 된다

ex) 0x00 ( UTF8 payload) 0xff

---

# 웹 소켓의 한계

HTML5 이전의 기술로 구현된 서비스에서는 어떻게 사용해야 할까.

바로 Socket.io, SockJS를 사용해 HTML5 이전의 기술로 구현된 서비스에서도

웹 소켓처럼 사용할 수 있다.

<br>

## Socket.io

> JS를 이용해 브라우저 종류에 상관없이 실시간 웹을 구현할 수 있게 도와주는 `라이브러리`

<br>

- 웹 소켓 연결 실패 시 fallback을 통해 다른 방식으로 해당 클라이언트와 연결을 시도함

- WebSocket, AJAX Long Polling, AJAX Multi part Streaming, IFrame, JSONP Polling을

  하나의 API로 추상화

- socket.io로 구성된 서버에게 소켓 연결을 하기 위해서는

  클라이언트측에서 반드시 socket.io-client 라이브러리를 이용해야 한다.

<br>

### Client 측 Socket.io

서버에서 처리해주는 socket.io보단 front에서 처리하는 socket.io에 대해 알아보겠다.

<br>

#### 1. 서버로의 메시지 송신(= 발신)

현재 접속되어 있는 서버로 `메시지를 송신(=발신)`하기 위해서는 `emit 메소드`를 사용한다.

<br>

<table border="1">
	<th>Parameter</th>
	<th>Description</th>
	<tr><!-- 첫번째 줄 시작 -->
	    <td>event name</td>
	    <td>이벤트 명(string)</td>
	</tr><!-- 첫번째 줄 끝 -->
	<tr><!-- 두번째 줄 시작 -->
	    <td>msg</td>
	    <td>송신 메시지(string or object)</td>
	</tr><!-- 두번째 줄 끝 -->
    </table>

<br>

```test.js
socket.emit("event_name", msg);
```

<br>
<br>

#### 2. 서버로부터의 메시지 수신

현재 접속되어 있는 서버로부터의 `메시지를 수신`하기 위해서는 `on 메소드`를 사용한다.

<table border="1">
	<th>Parameter</th>
	<th>Description</th>
	<tr><!-- 첫번째 줄 시작 -->
	    <td>event name</td>
	    <td>서버가 메시지 송신 시 지정한 이벤트 명(string)</td>
	</tr><!-- 첫번째 줄 끝 -->
	<tr><!-- 두번째 줄 시작 -->
	    <td>msg</td>
	    <td>이벤트 핸들러. 핸들러 함수의 인자에 서버가 송신한 메시지가 전달된다.</td>
	</tr><!-- 두번째 줄 끝 -->
    </table>


```test.js
socket.on("event_name", function(data) {
  console.log('Message from Server: ' + data);
});

```

<br>

## Namespace

socket.io는 서로 다른 엔드포인트(endpoint) 또는 경로(path)를 할당하는 의미로 socket에 namespace를 지정할 수 있다.

namespace를 특별히 지정하지 않은 경우 default namespace인 /를 사용하게 된다.

사용자 지정 namespace를 사용할 경우의 예제는 아래와 같다.


```test.js
// Server-side
const nsp = io.of('/my-namespace');

nsp.on('connection', function(socket){
  console.log('someone connected'):
});
nsp.emit('hi', 'everyone!');
```

```test.js
// Client-side
// 지정 namespace로 접속한다
const socket = io('/my-namespace');
```


<br>
<br>

### Reference

[MDN](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket)

[MDN](https://developer.mozilla.org/ko/docs/Web/API/WebSockets_API/Writing_WebSocket_servers)

[우아한 Tech WebSocket](https://www.youtube.com/watch?v=MPQHvwPxDUw)

[WebSocket ref blog 01](https://www.peterkimzz.com/websocket-vs-socket-io/)

[WebSocket ref blog 02](https://medium.com/@twizzledhongssiiiiiiii/%EA%B9%9C%EC%B0%8D%ED%95%9C-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EB%93%A4%EC%9D%84-%EC%9C%84%ED%95%9C-%EA%B0%84%EB%8B%A8%ED%95%9C-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%83%81%EC%8B%9D-2-2-http%EB%A5%BC-%EB%84%98%EC%96%B4%EC%84%9C-%EC%8B%A4%EC%8B%9C%EA%B0%84-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%82%B9websocket-c49125e1b5a0)

[Server Event를 Client로 보내는 4가지 방법](https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-Polling-Long-Polling-Server-Sent-Event-WebSocket-%EC%9A%94%EC%95%BD-%EC%A0%95%EB%A6%AC)

[Socket.io 예제](https://poiemaweb.com/nodejs-socketio)

[WebSocket 사용 방법 예제](https://walkingplow.tistory.com/87)
