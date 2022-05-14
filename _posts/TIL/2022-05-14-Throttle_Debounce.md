---
title: "Post: Throttle & Debounce"
categories:
  - Post Formats
tags:
  - TIL
  - CODING
  - BASIC
---

<br>

업무 중 카카오 맵과 관련된 코드를 보며 뜯어보던 중 Throttle과 Debounce를 사용해

기능이 구현되어져 있는 것을 보게 되었다.

왜 사용하는지, 사용함으로서 얻는 효과는 무엇인지, 사용 방법은 무엇인지 알고싶어져 포스팅하게 되었다.

<br>

# Throttle & Debounce의 사용 이유

> 연산을 반복적으로 실행하는 것에 제한을 두어 통제할 수 있는 수준으로 이벤트를 발생시키기 위한 방식

<br>

Lodash 라이브러리를 import 하여 사용할 수 있는 함수.

검색 기능이나 스크롤 이벤트와 같이 짧은 순간에 많은 콜백이 발생하는 이벤트를 컨트롤하기 위해 사용되며

불필요한 서버 리퀘스트와 불필요한 DOM 렌더링을 방지할 수 있기에 성능 개선에 도움이 된다.

<br>

# Throttle

> _.throttle(func, [wait=0], [options={}])

<br>

throttle은 콜백 함수(func)를 일정 시간(wait) 내에 최대 한 번만 호출한다.

`자주 사용되는 예시) 스크롤 이벤트, 드래그 이벤트`

<br>

```js
//간단한 예제

import React, {useEffect, useCallback, UseState} from "react";
import {throttle} from "lodash";

const App = () => {
  const [value, setValue] = useState(0);
  const throttled = useCallback(
  throttle((newValue) => console.log(newValue), 3000));
  
  useEffect(() => throttled(value), [value]);
  
  const changeValue = () => {
  setValue(value+1);
  }
  
  return <button onClick={ changeValue }>{value}</button>
}

```

<br> 
<br>

# Debounce

> _.debounce(func, [wait=0], [options={}])

<br> 

debounce는 이벤트가 끝난 뒤에 설정해둔 시간(wait)이 지나야 콜백(func)이 실행 된다

`자주 사용되는 예시) 사용자의 연속적인 타이핑이 이뤄지는 검색 기능`

<br>


```js
//간단한 예제

import React, {useEffect, useCallback, UseState} from "react";
import {debounce} from "lodash";

const App = () => {
  const [value, setValue] = useState(0);
  const debounced = useCallback(
  debounce((newValue) => console.log(newValue), 5000));
  
  useEffect(() => debounced(value), [value]);
  
  const changeValue = () => {
  setValue(value+1);
  }
  
  return <button onClick={ changeValue }>{value}</button>
}

```
---

<br>
<br>

# 느낀 점

debounce는 이벤트가 종료된 후 시작되고

throttle은 이벤트가 시작되면 일정 주기로 실행한다는 것이다.

상황에 맞게 사용할 수 있도록 프로젝트 경험을 쌓아야겠다.

<br>
<br>

#### Reference

<br>

[Lodash 공식 문서](https://lodash.com/docs/4.17.15)

[ref Blog 01](http://yoonbumtae.com/?p=2102)

[ref Blog 02](https://velog.io/@edie_ko/React-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-%EC%84%B1%EB%8A%A5-%ED%96%A5%EC%83%81-%EC%8B%9C%ED%82%A4%EA%B8%B0-feat.-Lodash-throttle-debounce)

[ref Blog 03](https://gusrb3164.github.io/web/2021/06/09/throttle,debounce/)

[ref Blog 04](https://developer-talk.tistory.com/263)

[ref Blog 05](https://thisblogfor.me/web/throttle_debounce/)
