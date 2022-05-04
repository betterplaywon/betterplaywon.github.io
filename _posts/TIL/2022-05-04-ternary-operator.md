---
title: "Post: 삼항 연산자"
categories:
  - Post Formats
tags:
  - TIL
  - CODING
  - BASIC
---

<br>

개인적으로 간단한 조건식을 입력할 때는 삼항 연산자를 즐겨 사용한다.<br>
하지만 조건이 길어진다면 if문이나 switch문을 사용해야 할 때가 훨씬 효율적이다.<br>
상황에 맞게 조건식을 사용할 줄 알아야 한다는 것이다.<br>

# eslint에서는 중첩 삼항 연산자에 대한 주의를 준다.

나는 중첩 삼항 연산자를 사용해보고 싶었고<br>
실제로 프로젝트에서 사용하여 기능을 구현시켜보았다.<br>
하지만 리뷰를 받으며 중첩 삼항 연산자는 가독성이 떨어진다는 동료 개발자 분들의 의견이 있었고<br>
무엇보다 중첩 삼항 연산자를 사용했을 때 발생하는 eslint의 주의가 있었다.<br>

.eslintrc
```
{
  "extends": ["react-app", "plugin:prettier/recommended"],
  "rules": {
    "no-var": "warn", // var 금지
    "no-multiple-empty-lines": "warn", // 여러 줄 공백 금지
    "no-nested-ternary": "warn", // 중첩 삼항 연산자 금지
    "no-console": "warn", // console.log() 금지
    "eqeqeq": "warn", // 일치 연산자 사용 필수
    "dot-notation": "warn", // 가능하다면 dot notation 사용
    "no-unused-vars": "warn", // 사용하지 않는 변수 금지
    "react/destructuring-assignment": "warn", // state, prop 등에 구조분해 할당 적용
    "react/jsx-pascal-case": "warn", // 컴포넌트 이름은 PascalCase로
    "react/no-direct-mutation-state": "warn", // state 직접 수정 금지
    "react/jsx-no-useless-fragment": "warn", // 불필요한 fragment 금지
    "react/no-unused-state": "warn", // 사용되지 않는 state
    "react/jsx-key": "warn", // 반복문으로 생성하는 요소에 key 강제
    "react/self-closing-comp": "warn", // 셀프 클로징 태그 가능하면 적용
    "react/jsx-curly-brace-presence": "warn", // jsx 내 불필요한 중괄호 금지
    "prettier/prettier": [
      "error",
      {
        "endOfLine": "auto",
        "singleQuote": true, // 홑따옴표로 지정
        "semi": false // 세미콜론제거
      }
    ]
  }
}
```
lint 설정 중 "no-nested-ternary": "warn"라는 부분에서 삼항 연산자를 통제해주고 있는데,<br>
이 점을 캐치하지 못해 주의를 받은 것이었다.<br>

기능을 구현하는 데 이상이 없는데 주의를 주는 것에 왜 신경을 쓰냐고 물을 수도 있지만<br>
최근 SEO 작업을 진행하며 알게 된 것은 자체적인 오류나 주의를 줄여야만 SEO 개선을<br>
할 수 있기 때문에 저런 주의도 세심히 관찰하며 프로젝트를 진행해야 한다.<br>


# 개인의 취향에 따른 선택

삼항 연산자는 분명 좋은 코드가 될 수 있지만,<br>
그보다 더 중요하게 여겨야 하는 것은 팀의 코드 스타일이다.<br>


