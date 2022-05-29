---
title: "Post: React 18 버전 업데이트에 따른 유용한 기능 3가지"
categories:
  - Post Formats
tags:
  - REACT
  - REDUX
  - CODING
  - BASIC
---

<br>

 3월 29일에 출시되어진 React 18 버전.
 
 좋은 기능들이 추가되었지만 그 중에서도 내가 생각했을 때
 
 유용한 기능이라고 생각되어진 3가지 기능에 대해 정리를 해보았다.
 
 <br>
 
 # 1. Batching, and Auto Batching
 
Batching이란 React가 더 나은 성능을 위해 여러 개의 state 업데이트를 하나의 리렌더링 (re-render)로 묶는 것을 의미한다.

<br>

## React 18V 이전의 batching 예시

<br>

 <img src='https://user-images.githubusercontent.com/78709765/170853947-5d999266-b9b6-41f0-9ed2-62b0d84f1546.png' width='700px'/>

<br>

Automatic batching이 존재하지 않던 `React 18V 이전`에는 `이벤트 핸들러 내부에서만 batched 업데이트`가 가능했다.

(기존에는 Promise의 내부나 timeout 혹은 native 이벤트 핸들러에서는 React에 의해 배칭 되지 않았다.)
 
하지만 React 18의 `createRoot`를 통해 모든 업데이트들은 출처와 무관하게 `자동으로 배칭`되게 된다.

이젠 timeout, promise, native 이벤트 핸들러와 `모든 여타 이벤트`는

`React에서 제공하는 이벤트와 동일하게 state 업데이트를 배칭`할 수 있다는 말이다.

결론적으로, 불필요한 렌더링을 최소화하고 `애플리케이션의 성능을 향상`시킬 수 있게 된 것이다.

<br>

## React 18V의 Auto batching 예시

<img src='https://user-images.githubusercontent.com/78709765/170854865-ae1bddfe-e8ba-4378-86b1-6aad5dcf7e04.png' width='700px'/>

<br>
<br>

# 2. useTransition

useTransition은 다음 화면으로 transition하기 전에 컨텐츠가 로드 될 때까지 대기함으로써

컴포넌트가 바람직하지 않은 로딩 상태를 피할 수 있게 해준다.

또한 컴포넌트가 더 중요한 업데이트를 즉시 렌더링 할 수 있도록

후속 렌더링까지 느린 데이터 가져오기를 지연시킬 수 있다.

<br>

## useTransition 사용 이유

브라우저는 single-threaded이기에 여러 번의 state 업데이트와 렌더링이 동시에 발생하면

렌더링이 전부 완료될 때 까지 사용자의 인터랙션은 차단된다.

이 때, useTransition은 사용자 인터랙션을 향상시켜줄 수 있다.

<br>

## useTransition의 구성

2개의 배열을 반환한다.

<br>

> const [ispending, startTransition] = useTransition();

<br>

startTransition: callback을 받는 함수

isPending: boolean 값, transition 완료를 알려줌
 
 <br>
 
## useTransition 예시

<br>

<img src='https://user-images.githubusercontent.com/78709765/170855937-d2780c8c-e208-4d3c-87ea-02cbe1675bf8.png' width='700px'/>

<br>
<br>

# 3. useDeferredValue

useDeferredValue를 사용하면, 급하지 않은 부분의 `재렌더링을 지연`할 수 있다.

`debounce, throttle과 비슷`하지만 timeout을 직접 지정할 필요 없이

리액트가 `다른 급한 작업이 완료 되는 즉시 실행`을 시킨다는 장점이 있다.

이 지연된 렌더링은 `인터럽트가 가능`하며, `사용자 입력을 차단하지 않는다`.

예를 들자면 input을 느리게 입력한다면 괜찮을 수도 있지만

일반 유저의 타자 속도일 경우 반드시 렌더링 성능 저하를 유발하는 코드이다.

(React 문서에서 이 현상을 '렌더링 차단(blocking)'이라 부른다.)

지금까지는 이러한 상황에서 debounce/throttle 을 이용해서 해결했지만 이젠 useDeferredValue를 통해 해결할 수 있게 되었다.

<br>

## useDefrredValue 예시

<img src='https://user-images.githubusercontent.com/78709765/170857495-60387f91-b9d7-4618-8852-1684dd05a1f5.png' width='700px'/>


<br>
<br>

# useTransition과 useDeferredValue, 어떤 상황에서 사용해야 할까

`상태 제어가 가능`할때는 useTransition를 사용,

`props에서 값에만 접근이 가능한 경우`엔 useDeferredValue를 사용하면 좋을 것 같다.

또한 두 메서드는 비슷한 작업을 수행하므로 상황에 맞게 둘 중 하나를 선택하여 성능 최적화를 시도하고

성능 최적화에는 다양한 방법이 있기 때문에 무조건 이 훅만 사용해야겠다며 한정된 생각에 매몰될 필요는 없어보인다.


 <br>
 <br>
 
 #### Reference
 
 [React 공식 블로그](https://reactjs.org/blog/2022/03/29/react-v18.html)
 
 [Auto Batching](https://nukw0n-dev.tistory.com/33)
 
 [Auto Batching](https://immigration9.github.io/react/2021/06/12/automatic-batching-react.html)
 
 [useTransition, useDeferredValue](https://www.youtube.com/watch?v=wZiOGxOhJNs&t=82s)
 
 [useDeferredValue](https://vroomfan.tistory.com/45)
 
 [useTransition, useDeferredValue](https://academind.com/tutorials/react-usetransition-vs-usedeferredvalue)
