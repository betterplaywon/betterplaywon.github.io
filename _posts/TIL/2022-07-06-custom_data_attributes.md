---
title: "Post: Custom Data Attributes"
categories:
  - Post Formats
tags:
  - TIL
  - CODING
  - BASIC
---

<br>

detail 태그와 summary 태그를 이용한 설명란 컴포넌트를 제작하며 value attribute가 필요했는데,

input 태그가 아니기에 다른 attribute가 필요했다.

마침 타이밍 좋게 동료 개발자 분이 말씀해 주신 custom data attributes를 사용해 볼 수 있겠다 여겨져

바로 적용했고, 이를 정리하고자 한다.

<br>
<br>

# Custom Data Attributes

기존의 HTML은 하나의 태그에 지정된 속성을 가질 수 있다.

지정된 속성 외에 다른 속성을 지정하는 것은 HTML 표준을 어기는 것과 같으나

이러한 문제를 해결할 수 있는 `Custom Data Attributes`가 존재한다.

<br>

## 특징

<br>

1. 속성의 시작은 무조건 `data-`로 시작해야 한다.

2. 하나의 태그에 사용 가능한 custom data attribute는 `원하는 만큼 사용`할 수 있다.

3. 브라우저는 cunstom data attribute를 만나면 `파싱하지 않고 넘어간다.` (= view에 영향을 미치지 않는다)

4. `JS와 CSS`에서 custom data attribute의 정보를 `활용 가능`하다.

<br>
<br>

## 사용 예시

<br>

```js
       <div>
        <details open={selectedFaq === '1'} data-detailsKey={'1'} onClick={handleDetail}>
          <summary>Q1</summary>
          <p>
           내용 OOO
          </p>
        </details>
        <details open={selectedFaq === '2'} data-detailsKey={'2'} onClick={handleDetail}>
          <summary>Q2</summary>
          <p>
          내용 OOO
          </p>
        </details>
        <details open={selectedFaq === '3'} data-detailsKey={'3'} onClick={handleDetail}>
          <summary>Q3</summary>
          <p>
           내용 OOO
          </p>
        </details>
      </div>
```

<br>

custom data attribute로 data-detailsKey를 만들었고

이를 이용해 state와 연관시킨 함수를 만들어 해당 태그들을 컨트롤했다.

<br>
<br>

#### Reference

[HTML5 Doctor - Custom Data Attributes](http://html5doctor.com/html5-custom-data-attributes/)
