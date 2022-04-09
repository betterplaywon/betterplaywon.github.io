---
title: "Post: Tagged Literals"
categories:
  - Post Formats
tags:
  - JS
  - CODING
  - BASIC
---

# Tagged Literals
> Template literals의 표현식을 분해할 수 있는 기능<br>


## 기본 사용법

> 함수 뒤에 백틱을 사용해 텍스트와 변수를 작성해주면 끝이다.

함수의 인자로 2개를 넣어주는데, 첫번째 인자는 백틱 내부의 순수 문자만 골라서<br>
<u>Array로 만들어놓은 인자</u>,  두번째 인자는 <u>백틱 내부의 변수를 담는 인자</u>다.<br>

만약 백틱 내부에 변수가 더 존재한다면 함수의 인자를 추가해주면 된다.<br>

## 예시
```
const name = 'kang';

function ho (text, variable) {
console.log(text);
console.log(variable);
}

ho`Hi, ${name}. bye`;

// (2) ['Hi, ', '. bye', raw: Array(2)]
// kang
// 두 개의 결과가 출력된다.

```

---

## 약간의 응용
![](https://images.velog.io/images/betterplaywon/post/9dbb7539-c0da-4938-ac60-bc00474f520f/image.png)

아주 간단한 조건문을 활용해 tagged literals에 응용을 해봤다.<br>

해당 거리가 0이라면 지정한 텍스트가 나오도록 설정,<br>
해당 거리가 0이 아니라면 뛴 만큼의 수치가 나오도록 설정했다.<br>

---
