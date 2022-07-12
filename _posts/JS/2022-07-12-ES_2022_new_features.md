---
title: "Post: JS ES 2022에서 생겨난 기능들"
categories:
  - Post Formats
tags:
  - JS
  - CODING
  - BASIC
---

<br>

# 1. Top Level Await

<br>

이전까지는 await를 사용하기 위해선 async 함수 내부에서 작성해줘야 했지만

ES2022 부터는 비동기화 없이 wait를 사용하여 다른 코드를 조건부 또는 동적으로 로드할 수 있다.

<br>

```js

// 이전에는 async 내부에서 await 작성이 필수

(async function() {
  await Promise.resolve(console.log('Complicated'));
  // Output: Complicated
}());
}


// 이젠 await만 따로 작성 가능!
await Promise.resolve(console.log('Simple!'));

```

<br>

# 2. Error Cause

<br>

이전에는 오류를 강제로 만들 때 오류 메시지를 작성하는 것 밖엔 할 수 없었지만

이젠 오류의 원인이 무엇인지 설명까지 가능하다.

```js

// 이전에는 단순히 오류 메시지만 남길 수 있었음
try {
} catch (error) {
  throw new Error("Occured Error");
}


// 지금은 그 이유에 대해서도 설명 가능
try {
} catch (error) {
  throw new Error('Occured Error', { cause: "Not string" });
}

```

<br>

# 3. .at()

<br>

기존에는 배열을 탐색할 때 양수로만 가능했지만

.at()을 사용함으로서 음수로도 배열을 탐색할 수 있게 되었다.

```js

[1,2,3,4,5].at(3)  // returns 4

[1,2,3,4,5].at(-2)   // returns 4

```

<br>

# 4. Class Fields

<br>

이해가 잘 되지 않았던 부분.

이전엔 불가능했던 private 메서드 및 속성을 가질 수 있게 되었고

속성을 초기화하기 위해 `constructor를 사용할 필요도 없다`.

`Private 메서드나 속성`을 만들려면 이름 앞에 `# 기호를 사용`하면 된다.

또한 `static 메서드도 사용`할 수 있게 되었다.

<br>

```js
// 이전에는 Private 메서드 사용이 안되었다.

class Message {
  constructor() { // 또한 속성 초기화를 위한 constructor 사용이 필요했다.
    this.text = "Hello";
  }
}


// ES 2022

class Message {
  #text = "Hello";
}
```
 
 <br>
 
```js
// 이전

class Message {
  //body
}  

Message.build(){
  //body
}

// ES 2022

class Message {
  static build(){ // 상황에 따라 #build()로 Private하게 만들어 줄 수도 있다.
   //body
  }
}


```
 
 
 
 

#### Reference

[ES 2022 new Features 01](https://dev.to/jasmin/whats-new-in-es2022-1de6v)

[ES 2022 new Features 02](https://javascript.plainenglish.io/4-best-new-es2022-features-6e73db339b21)

[ES 2022 new Features 03](https://dev.to/brayanarrieta/new-javascript-features-ecmascript-2022-with-examples-4nhg)
