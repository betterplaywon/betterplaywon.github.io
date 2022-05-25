---
title: "Post: Redux의 키워드"
categories:
  - Post Formats
tags:
  - REACT
  - REDUX
  - CODING
  - BASIC
---

<br>

리덕스를 구성하는 기본 개념을 다시 한 번 상기시키기 위해 정리를 해보았다.

<br>
<br>

# 액션 (Action)

`상태에 어떠한 변화가 필요할 때` 액션을 발생시킨다.

`액션`은 `하나의 객체`로 표현되어진다.

<br>

```js
{
  type: "TOGGLE_VALUE"
}
액션 객체는 type 필드를 필수적으로 가지고 있어야하고 그 외의 값들은 마음대로 넣는 게 가능하다.

{
  type: "ADD_TODO",
  data: {
    id: 0,
    text: "리덕스 배우기"
  }
}
{
  type: "CHANGE_INPUT",
  text: "안녕하세요"
}
```
<br>

# 액션 생성함수 (Action Creator)

액션을 만드는 함수.

파라미터를 받아와서 액션 객체 형태로 만들어준다.

<br>

```js
export function addTodo(data) {
  return {
    type: "ADD_TODO",
    data
  };
}

// arrow function으로도 만들 수 있다.
export const changeInput = text => ({ 
  type: "CHANGE_INPUT",
  text
});
```
<br>

## 액션 생성함수를 만들어서 사용하는 이유

나중에 컴포넌트에서 더욱 쉽게 액션을 발생시킬 수 있어서이다.

그래서 보통 함수 앞에 export 키워드를 붙여서 다른 파일에서 불러와서 사용한다.

리덕스를 사용 할 때 액션 생성함수를 사용하는것이 필수적이진 않지만

매번 직접 액션을 발생시킬 때 마다 액션 객체를 작성하기란 번거롭기 때문에 액션 생성 함수를 만들어 사용하는 것이 편하다.

<br>

# 리듀서 (Reducer)

변화를 일으키는 함수.

리듀서는 두가지의 파라미터를 받아온다.

```js
function reducer(state, action) {
  // 상태 업데이트 로직
  return alteredState;
}
```

리듀서는, 현재의 상태와, 전달 받은 액션을 참고하여 새로운 상태를 만들어서 반환한다.

### ex) 카운터를 위한 리듀서를 작성해봤을 때

```js
function counter(state, action) {
  switch (action.type) {
    case 'INCREASE':
      return state + 1;
    case 'DECREASE':
      return state - 1;
    default:
      return state;
  }
}
```

useReducer 에선 일반적으로 default: 부분에 throw new Error('Unhandled Action')과 같이

에러를 발생시키도록 처리하는게 일반적인 반면 리덕스의 리듀서에서는 기존 state를 그대로 반환하도록 작성해야한다.

리덕스를 사용 할 때에는 여러개의 리듀서를 만들고 이를 합쳐서

루트 리듀서 (Root Reducer)를 만들 수 있다.

(루트 리듀서 안의 작은 리듀서들은 서브 리듀서라고 부른다.)

<br>

# 스토어 (Store)

`리덕스`에서는 `한 애플리케이션당 하나의 스토어`를 만들게 된다.

스토어 안에는 현재의 앱 상태와 리듀서가 들어가있고, 추가적으로 몇가지 내장 함수들이 존재한다.

<br>

# 디스패치 (dispatch)
스토어의 내장함수 중 하나. 액션을 발생 시키는 것이라고 볼 수 있다.

dispatch 라는 함수에는 액션을 파라미터로 전달한다.

<br>

> dispatch(action)

<br>

그렇게 호출을 하면, `스토어는 리듀서 함수를 실행`시켜서

해당 액션을 처리하는 로직이 있다면 `액션을 참고하여 새로운 상태`를 만들어줍니다.

<br>

# 구독 (subscribe)
스토어의 내장함수 중 하나.

함수 형태의 값을 파라미터로 받아온다.

subscribe 함수에 특정 함수를 전달해주면, 액션이 디스패치 되었을 때 마다 전달해준 함수가 호출된다.

실제로 리액트에서 리덕스를 사용하게 될 때 보통 이 함수를 직접 사용하는 일은 드물다.

하지만 react-redux 라는 라이브러리에서 제공하는 `connect 함수` 또는 `useSelector Hook` 을 사용하여 `리덕스 스토어의 상태에 구독`한다.

<br>
<br>

#### Reference

[Velopert React basic](https://react.vlpt.us/redux/01-keywords.html)
