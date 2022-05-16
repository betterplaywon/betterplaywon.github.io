---
title: "Post: useCallback Hook"
categories:
  - Post Formats
tags:
  - REACT
  - CODING
  - BASIC
---

<br>

회사 프로젝트를 진행하며 useCallback hook을 사용해 기능을 구현한 것을 보며

사용 이유에 대해 궁금해졌고, useCallback을 사용함으로서 얻을 수 있는 것은

무엇인지 정리하기 위해 포스팅했다.

<br>

# useCallback

> 특정 함수를 새로 만들지 않고 재사용하고 싶을 때 사용하는 함수

<br>

함수는 컴포넌트가 리렌더링 될 때 마다 새로 생성된다.

한두 개의 함수 선언은 메모리나 리소스를 꽤나 잡아먹는 작업은 아니기에

새로 선언한다고 해서 성능 상 큰 문제가 되진 않는다.

하지만 함수가 많아진다는 가정이 필요하다.

함수 선언이 증가함에 따라 개발자의 예상보다 더한 메모리나 리소스를

소모하게 될 것이고, 결국 부담으로 자리잡게 될 수 있다.

<br>

결론적으로 컴포넌트에서 props 가 바뀌지 않았으면 Virtual DOM 에 리렌더링 하지 않고

컴포넌트의 결과물을 재사용 하는 최적화 작업이 필요하다.

이 최적화 작업을 하려면 함수를 재사용 하는 것은 필수이고,

여기서 useCallback의 사용이 필요하다.

<br>
<br>

# useCallback 사용법

> const memoizedCallback = useCallback(function, deps);

<br>

함수 내부에서 사용하는 상태 혹은 props 가 있다면 꼭 deps 배열에 포함해야한다.

만약 deps 배열 안에 함수에서 사용하는 값을 넣지 않게 된다면

함수 내에서 해당 값들을 참조할 때 가장 최신 값으로 참조 할 것이라고 보장 할 수 없기 때문이다

따라서, props 로 받아온 함수가 존재한다면 deps 배열에 포함시켜줘야한다.

<br>

# 사용 예시

[예시 blog](https://www.daleseo.com/react-hooks-use-callback/)




<br>

#### Reference

[DaleSeo blog, useCallback](https://www.daleseo.com/react-hooks-use-callback/)

[useCallback 사용법 blog](https://cocoon1787.tistory.com/798)

[useCallback 간략 정리 blog](https://2ham-s.tistory.com/328)

[Velopert, useCallback](https://react.vlpt.us/basic/18-useCallback.html)
