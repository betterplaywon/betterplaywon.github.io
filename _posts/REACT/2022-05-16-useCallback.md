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

결론적으로 컴포넌트 내에서 하위 컴포넌트로 보내는 props 가 바뀌지 않았으면

Virtual DOM 에 리렌더링 하지 않고 컴포넌트의 결과물을 재사용 하는 최적화 작업이 필요하다.

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

```js
//Result.js
import React, { useState } from 'react';
import SmartHome from './SmartHome';

const Result = () => {
  return (
    <div style={{ position: 'absolute', top: '50%', left: '50%' }}>
      <SmartHome />
    </div>
  );
};

export default Result;
```

```js
// Light.js
import React from 'react';

function Light({ room, on, toggle }) {
  console.log({ room, on });
  return (
    <div>
      <button onClick={toggle}>
        {room}
        {on ? '💡' : '⬛'}
      </button>
    </div>
  );
}

export default React.memo(Light);
```

```js
// SmartHome.js
import React, { useState, useCallback } from 'react';
import Light from './Light';

function SmartHome() {
  const [masterOn, setMasterOn] = useState(false);
  const [kitchenOn, setKitchenOn] = useState(false);
  const [bathOn, setBathOn] = useState(false);

  const toggleMaster = () => {
    setMasterOn(!masterOn);
  };
  const toggleKitchen = () => {
    setKitchenOn(!kitchenOn);
  };
  const toggleBath = () => {
    setBathOn(!bathOn);
  };

  return (
    <div>
      <Light room="침실" on={masterOn} toggle={toggleMaster}></Light>
      <Light room="주방" on={kitchenOn} toggle={toggleKitchen}></Light>
      <Light room="욕실" on={bathOn} toggle={toggleBath}></Light>
    </div>
  );
}

export default SmartHome;

```

<br>

#### useCallback 적용 전

<br>

<img src='https://user-images.githubusercontent.com/78709765/168551102-05780860-d570-4669-987d-5efe07bf6adc.png' width='600px'/>

<br>

Light.js 에서 react.memo를 적용해 불필요한 리렌더링을

막아주려는 시도를 했지만 react.memo는 제 역할을 수행하지 못했다.

그 이유는 `함수는 객체`이기 때문이다.

`리렌더링이 발생`하면 `해당 컴포넌트의 모든 객체들은 다시 생성`된다.

JS에서 객체는 Reference type으로

동일한 value를 지니더라도 `참조하는 주소가 다르다`면 `서로 다른 객체`로 여긴다.

컴포넌트는 리렌더링될 때마다 새로운 함수를 생성하며

Reac.memo는 상위 컴포넌트에서 넘겨받는 props가 변경되었다고 인지해

계속 리렌더링을 하는 것이다.

<br>
<br>

#### useCallback과 react.memo 적용 후

<br>

```js
import React, { useState, useCallback } from 'react';
import Light from './Light';

function SmartHome() {
  const [masterOn, setMasterOn] = useState(false);
  const [kitchenOn, setKitchenOn] = useState(false);
  const [bathOn, setBathOn] = useState(false);

  const toggleMaster = useCallback(() => {
    setMasterOn(!masterOn);
  }, [masterOn]);
  const toggleKitchen = useCallback(() => {
    setKitchenOn(!kitchenOn);
  }, [kitchenOn]);
  const toggleBath = useCallback(() => {
    setBathOn(!bathOn);
  }, [bathOn]);

  return (
    <div>
      <Light room="침실" on={masterOn} toggle={toggleMaster}></Light>
      <Light room="주방" on={kitchenOn} toggle={toggleKitchen}></Light>
      <Light room="욕실" on={bathOn} toggle={toggleBath}></Light>
    </div>
  );
}

export default SmartHome;

```

<br>

<img src='https://user-images.githubusercontent.com/78709765/168551572-8a07d062-1d3c-4fef-91ca-360132213403.png' width='600px'/>

<br>

주방 버튼을 클릭하면 주방에 대한 Light 컴포넌트만 리렌더링 된 것을 볼 수 있다.

useCallback을 사용함으로서 deps 배열 내부의 state가 변할 때에만 새로운 객체를 생성하게 되었고

state가 변하지 않는다면 동일한 객체를 전달해줌으로 불필요한 리렌더링을 방지할 수 있게 되었다.

 


<br>

#### Reference

[DaleSeo blog, useCallback](https://www.daleseo.com/react-hooks-use-callback/)

[useCallback 사용법 blog](https://cocoon1787.tistory.com/798)

[useCallback 간략 정리 blog](https://2ham-s.tistory.com/328)

[Velopert, useCallback](https://react.vlpt.us/basic/18-useCallback.html)

[ref blog](https://leego.tistory.com/entry/React-useCallback%EA%B3%BC-useMemo-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)
