---
title: "Post: 자료 구조"
categories:
  - Post Formats
tags:
  - TIL
  - CODING
  - BASIC
---

<br>

# Stack

<img src='https://blog.kakaocdn.net/dn/rUqtT/btqIBYGv5aZ/zVsMryjKUTqnN9Kwt5BBek/img.jpg' width='500px'/>

LIFO(Last In, First Out) 방식의 자료 구조

- 데이터가 쌓이며 가장 마지막에 push된 자료가 가장 먼저 pop 되는 구조를 지닌다.

- top으로 정한 곳으로만 접근 가능하다.
  
  => 새로 push되는 데이터는 top이 가리키는 최상단에 쌓이며, pop 되는 데이터 또한 최상단부터 처리된다. 
  
  <br>
  
  # Queue
  
  <img src='https://blog.kakaocdn.net/dn/Kri2r/btq2u3BF2GD/NXMEc74ZDvXAUA8TfKNNHK/img.png' width='600px'/>
  
FIFO(First In, First Out) 방식의 자료 구조
  
- 먼저 들어온 데이터가 먼저 나가게 되는 구조를 지닌다.

- 데이터가 들어오는 입구와 출구가 구분되어져있다.

  => 입구로 들어온 데이터는 출구로 나가진다.
  
<br>

# JS에서의 Stack과 Queue

array를 사용하면 Queue와 Stack 둘 다 다룰 수 있게 된다.

위의 자료구조를 통해 array의 처음이나 끝에 요소를 더하거나 빼는 데 사용할 수 있는데

이렇게 처음이나 끝에 요소를 더하거나 빼주는 연산을 제공하는 자료구조를

데큐(deque, Double Ended Queue)라고 부른다.

<br>

---

Reference

[자료구조 참조](https://ko.javascript.info/array)






