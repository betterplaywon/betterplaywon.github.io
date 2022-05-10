---
title: "Post: Tagged Literals"
categories:
  - Post Formats
tags:
  - JS
  - CODING
  - BASIC
---

<br>

구글링을 하다 우연히 재미있는 기능을 발견했다.

변형된 template literals인 tagged literals이다.

#  Tagged Literals

> Template literals의 표현식을 분해할 수 있는 기능

<br>

# 기본 사용법

> 함수 뒤에 백틱을 사용해 텍스트와 변수를 작성해주면 끝이다.

함수의 인자로 2개를 넣어주는데, 첫번째 인자는 백틱 내부의 순수 문자만 골라서

Array로 만들어놓은 인자, 두번째 인자는 백틱 내부의 변수를 담는 인자다.

만약 백틱 내부에 변수가 더 존재한다면 함수의 인자를 추가해주면 된다.

<br>

# 예시

```test01.js
const name = 'kang';
function ho (text, variable) {
console.log(text);
console.log(variable);
}

ho`Hi, ${name}. bye`;

// (2) ['Hi, ', '. bye', raw: Array(2)]
// kang
// 두 개의 결과가 출력된다.
```

# 응용하기

``` testResult.js
let nikeRunningKm = 0;
let nikeRunningLevel = 'Blue Label';

const example = (text,...variable) => {
  if(variable[0] === 0){
    variable[0] = '0 KM';
  }else {
    variable[0]
  }
  console.log(text[0]+variable[0]+', '+text[1]+variable[1]);
}

example`첫 러닝 거리: ${nikeRunningKm} 현재 러닝 레벨: ${nikeRunningLevel}`

// '첫 러닝 거리: 0 KM,  현재 러닝 레벨: Blue Label'
```

최근 나이키 런 블루 라벨을 달성한 기념으로 만들어 본 예제이다.

해당 거리가 0이라면 지정한 텍스트가 나오도록 설정,

해당 거리가 0이 아니라면 현재 러닝 레벨이 나오도록 설정했다.

현업에서 사용하기까지 시간이 조금 걸리겠지만,

함께 일하는 개발자 분들에게 꼭 공유해보고 싶은 내용이다.
