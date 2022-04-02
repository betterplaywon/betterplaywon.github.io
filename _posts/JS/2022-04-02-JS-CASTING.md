---
title: "Post: JS 형 변환"
categories:
  - Post Formats
tags:
  - JS
  - CODING
  - BASIC
---

# true / false인 이유
```
0 == '0'; // true
0 == [ ]; // true
'0' == []; // false

```
3개의 연산 결과가 true/false인 이유에 대해 알아보자

# 나의 생각

결론부터 말하면 Null과 undefined로 접근을 했고, 틀렸다.

## 1) 0 == '0'
원시 데이터 타입 중 num과 string을 비교하는 것.
자바스크립트가 알아서 해주는 거 아녔나? 라는 생각이 들었다.

문득 값이 없는 것은 undefined가 아닐까라는 생각이 들었고,<br>
undefined == undefined 로서 true가 된 것 같았다.<br>

## 2) 0 == [ ]
원시 데이터와 참조형 데이터를 비교하는 것.
빈 배열의 값은 결국 빈 문자열 ''을 의미하는 것이고, 존재하지 않는 것이니<br>
undefined라고 생각했다.

그래서 해당 항목도 true가 된 것 같다고 추측했다.


## 3) '0' == [ ]
여기서 나의 논리가 틀렸다는 것을 알 수 있었다.<br>
문자열 '0'도 undefined고, 빈 배열도 undefined라면 true가 되어야 하는데<br>
쌩뚱맞은 false가 정답이었다.

<br>

결과적으로는 Javascript의 형변환에 대해<br>
이해하고 있는지를 물어본 것이었다.<br>

---

# 연산자에 따른 형변환
> JavaScript는 연산자에 따라 형변환이 다르게 일어난다.<br>
또한 원시값인지, 참조값인지에 따라서도 다른 형변환이 일어난다.<br>

기본적으로 자동 자료 변환 시<br>
'+' 연산자는 문자열이 숫자보다 우선시 ( 문자열 > 숫자)<br>
나머지 사칙연산자는 숫자가 문자열보다 우선시 ( 문자열 < 숫자)<br>

## 1) + 연산자

```
3 + '3' // 문자 '33'이 도출된다.
```
이 것으로 알 수 있는 것은 number 3이 string 3으로 형변환이 되고<br>
문자열 두 개를 합친 새로운 하나의 문자열을 만들어 낸다.<br>

</br>

모든 문자열이 숫자로 변환 가능한 것은 아니다.<br>
하지만 모든 숫자는 문자열로 변환 가능하다.</br>
그렇기 때문에 <u>+ 연산에 문자열과 숫자가 연산될 때는<br>
숫자를 문자열로 변환 후에 연산을 한다.</u><br>

## -, /, * 연산자를 사용할 때

> -, /, * 연산자는 수학적 연산만을 지닌다.

```
3 - '1' // 2
3 * '2' // 6
3 / '3' // 1

'interview' - 'terview' // NaN
```

<u>연산에 사용되는 모든 값은 숫자로 변환 후에 연산</u>을 하게된다.<br>
다른 수학적 연산자 모두 동일하게 동작한다는 점도 꼭 알아두자.<br>
예외로, 숫자로 변환될 수 없는 값은 NaN 값을 지닌다.<br>

</br>

###  boolean을 더하는 경우
```
3 + true // 4
3 - false // 3
```
true는 1로, false는 0으로 변환이 가능하다.<br>
그렇기 때문에 숫자와 boolean을 연산을 할 때는<br>
boolean을 숫자로 변환 후에 연산을 진행한다.<br>

---

# 참조형 데이터의 형변환 
> 참조 데이터 또한 JavaScript에서 자동 형변환을 진행한다.<br>

## Array의 경우

```
[] + 1 // '1'
[] == 0 // 0
```

array는 toString() 메서드를 지니고 있다.<br>
이 함수는 각 원소를 ,로 구분하여 문자열로 만드는 함수이다.<br>
array를 string으로 바꾸고 연산을 하게 된다는 거다.<br>

```
[] + 3 => [].toString() + 3 => '' + 1 => '3'
```

</br>

## Object의 경우

> Object 또한 자동으로 원시값으로 형변환이 되어 연산된다.<br>

![](https://images.velog.io/images/betterplaywon/post/87ac114c-b6d5-4153-9fdf-c9019d85e531/image.png)

????????
배열은 예상을 했는데 Object의 결과가 너무 신기했다.<br>
object도 toString() 함수의 적용을 받을 수 있었고, Object가 Array형으로 변환되어<br>
[object object]10 이라는 결과가 나왔다.<br>
```
const obj = {};
obj + 10 => obj.toString() + 10 => '[object Object]' + 10 => '[object Object]1'
```

---

<br>

# == 연산에서의 형변환

참조값이 ==연산에 사용될 경우에는 참조값이<br>
toString() 연산을 통해 원시값으로 형변환되고, 이어지는 연산을 수행한다.<br>


## Truthy와 Falsy 
> 조건문에서 사용되는 값이 true냐 false를 나타내는 값.

### Falsy한 값
> undefined, null, NaN, 0 (숫자 리터럴) , -0, “” (빈 문자열), false
총 7가지 이다


Truthy한 값은 Falsy한 값을 제외한 모든 값이다.

### Truthy와 Falsy의 예외

> 주의할 점은 <u>빈 문자열은 false</u> 이지만 <u><br>
> 빈 배열, 빈 객체는 true</u>라는 것이다.<br>

예시
```
if([]) {
  console.log('k'); // [] 가 true이므로 console.log가 작동한다.
}

if(0) {
  console.log('k'); 0은 false이므로 console.log가 작동하지 않는다.
}
```

<br>
<br>

Reference
[연산자에 따른 형변환](https://codedragon.tistory.com/5589)<br>
[전체적인 형 변환 정리](https://velog.io/@yejinh/Javascript-%ED%98%95%EB%B3%80%ED%99%98)<br>
[자바스크립트에서 false로 간주되는 것들](https://studymake.tistory.com/484)<br>
