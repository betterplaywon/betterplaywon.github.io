---
title: "Post: React Memo()"
categories:
  - Post Formats
tags:
  - REACT
  - CODING
  - BASIC
---

기본적으로 컴포넌트에 있는 <u>props나 state가 변경</u>되면<br>
<u>해당 props나 state를 사용하는 HTML을 전부 렌더링</u>한다.<br>

하지만 불필요하게 모든 state나 props에 대해 렌더링하는 것은 자원 낭비일 수 있다.<br>
이런 상황에 사용할 수 있는 것이 바로 memo이다.<br>

# react.memo
> props 데이터 변경이 안된 컴포넌트는 재렌더링을 막아달라는 의미

React.memo()로 래핑 될 때, React는 컴포넌트를 렌더링하고<br>
결과를 메모이징(Memoizing)한다. 그리고 다음 렌더링이 일어날 때 props가 같다면<br>
React는 메모이징(Memoizing)된 내용을 재사용한다.<br>

이 말의 의미는<br>
props로 데이터를 전달할 때, 내가 변경한 데이터만 렌더링이 일어나게 만들어주고<br>
변경하지 않은 데이터는 렌더링을 막아준다는 거다.<br>

## 예시

Sample이라는 상위 컴포넌트에서 FirstChild와 SecondChild라는 하위 컴포넌트에<br>
props로 데이터를 전달해주는 코드이다. 여기서 name이란 데이터만 변경을 주며<br>
렌더링을 관찰했다.<br>

### react.memo 사용 전의 rendering
![](https://images.velog.io/images/betterplaywon/post/8aef20a0-6167-4771-9ec7-176b12a72d21/image.png)

![](https://images.velog.io/images/betterplaywon/post/67e2d735-8715-45cf-93cd-5917bbd879ba/image.png)

memo를 사용해주지 않았을 경우에는 하위 컴포넌트 모두 재렌더링이 되는 것을 볼 수 있다.<br>


### react.memo를 사용 후의 rendering

![](https://images.velog.io/images/betterplaywon/post/fdb48ade-6a86-4a6c-a99a-9a2c94677b5c/image.png)

![](https://images.velog.io/images/betterplaywon/post/58ec7b12-324b-4a73-b2d7-7d3ad779c5ee/image.png)

memo를 사용했을 경우에는 변경된 name 이라는 데이터가 들어있는 component만<br>
렌더링이 되는 것을 볼 수 있다.<br>


# 결론

실시간으로 변경되는 데이터에 memo를 사용해줘 자원의 낭비를 막을 수 있다는 점에선<br>
훌륭한 기능임에 틀림없다.<br>

하지만 클래스형 컴포넌트를 사용할 때는 memo를 사용해주기보단<br>
PureComponent를 확장하여 사용하거나, shouldComponentUpdate() 메서드를<br>
구현하는 것이 적절하다는 것과 렌더링 최적화를 하지 않을 컴포넌트에<br>
React.memo 를 사용하면 불필요한 props 비교만 하게 된다는 점.<br>

꼭 필요하다고 생각되는 부분에만 사용을 해주도록 하자<br>


Reference<br>
[memo를 현명하게 사용하기](https://ui.toast.com/weekly-pick/ko_20190731)<br>
[velopert의 react.memo](https://react.vlpt.us/basic/19-React.memo.html)<br>
