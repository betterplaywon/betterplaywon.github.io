---
title: "Post: Module"
categories:
  - Post Formats
tags:
  - TIL
  - CODING
  - BASIC
---

# Module이란

> 프로그램을 구성하는 구성요소의 일부

개발하는 애플리케이션의 크기가 커지면 확장성과 유지보수 측면에서 파일을 여러 개로 분리하는 시점이 온다.

이때 분리된 파일 각각을 '모듈'이라고 부른다.

# 모듈화의 장점

1. 프로그램의 효율적인 관리 및 성능 향상

2. 전체적인 소프트웨어의 복잡도 감소

3. 기능 분리의 가능, 인터페이스의 단순화

4. 오류의 영향력을 최소화

5. 모듈의 재사용 가능으로 개발과 유지보수가 용이


## JS에서의 모듈

JS에서 export와 import를 통해 모듈을 로드할 수 있다.

export 지시자를 변수나 함수 앞에 붙이면 외부 모듈에서 해당 변수나 함수에 접근할 수 있고(모듈 내보내기),

```Test.js
export function Test() {
console.log('export 예제문');
}
```


import 지시자를 사용하면 외부 모듈의 기능을 가져올 수 있다(모듈 가져오기)

```TestResult.js
import Test from './Test';

Test();
```

모듈은 특수한 키워드나 기능과 함께 사용되므로 `<script type="module">` 같은 속성을 설정해

해당 스크립트가 모듈이란 걸 브라우저가 알 수 있게 해줘야 한다.

```index.html
<!doctype html>
<script type="module">
  import {sayHi} from './say.js';

  document.body.innerHTML = sayHi('John');
</script>
```
주의할 점은 모듈은 로컬 파일에서 동작하지 않고, HTTP 또는 HTTPS 프로토콜을 통해서만 동작한다는 거다.

로컬에서 `file://` 프로토콜을 사용해 웹페이지를 열면 `import`, `export` 지시자가 동작하지 않는데

예시를 실행하려면 Visual Studio Code 에디터의 경우 Live Server Extension을 사용해주면 된다.

---

# 빌드 툴(= 번들링 툴)

브라우저 환경에서 모듈을 '단독’으로 사용하는 경우는 드물다.

웹팩(Webpack)이나 파슬(Parcel)과 같은 툴을 사용해 모듈을 묶어

프로덕션 서버에 올리는 방식을 사용하는데 이를 `번들링`이라 한다.

번들러를 사용하면 모듈 분해에 있어 통제 가능하다.

추가적으로 경로가 없는 모듈이나 CSS, HTML 포맷의 모듈을 사용할 수 있게 해준다는 장점도 존재한다.

## 빌드 툴의 사용 결과

빌드 툴을 사용하면 스크립트들은 하나 혹은 여러 개의 파일로 번들링된다.

이때 번들링 전 스크립트에 있던 import, export문은 특별한 번들러 함수로 대체된다.

번들링 과정이 끝나면 기존 스크립트에서 import, export가 사라지기 때문에 type="module"이 필요 없어지고

따라서 번들링 과정을 거친 스크립트는 일반 스크립트처럼 취급할 수 있다.

<br>

# Parcel

> 빠르고 설정이 필요 없는 웹 애플리케이션 번들러

## Parcel의 장점
1. 기존의 빌드 툴이었던 weback에 비해 빠르고 자세한 에러 메시지를 제공한다.

2. zero-configuration : 설정이 필요없음

3. 동적 import()문을 사용해서 출력 번들을 분할. 초기 로드시 필요한 것들만 로드할 수 있음

4. 파일시스템 캐시 : 재시작 후에도 빠른 리빌드
최초 빌드 후, 두 번째 빌드부터 빌드 속도가 빨라짐
<img src='https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbAYcNe%2FbtrnZmMeiN0%2FMJJ5nVprxzvauYP9661DNK%2Fimg.png' width='600px'/>

<br>

Reference

[Modern JS](https://ko.javascript.info/modules-intro#ref-650)

[Bundler blog](https://kangdanne.tistory.com/190)

[Parcel.org](https://parceljs.org/getting-started/library/)
