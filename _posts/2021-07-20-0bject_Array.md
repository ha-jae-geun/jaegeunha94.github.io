---
layout: post
toc: true
title: "실행 컨텍스트"
categories: javascript
tags: [javascript]
author:
  - Jack
---



# 프로퍼티 플래그
* 객체 프로퍼티는 값(value) 과 함께 플래그(flag)라 불리는 특별한 속성 세 가지를 갖습니다.
1. writable – true이면 값을 수정할 수 있습니다. 그렇지 않다면 읽기만 가능합니다.
2. enumerable – true이면 반복문을 사용해 나열할 수 있습니다. 그렇지 않다면 반복문을 사용해 나열할 수 없습니다.
3. configurable – true이면 프로퍼티 삭제나 플래그 수정이 가능합니다. 그렇지 않다면 프로퍼티 삭제와 플래그 수정이 불가능합니다.
* 프로퍼티 플래그는 특별한 경우가 아니고선 다룰 일이 없기 때문에 여기서 처음 소개하게 되었습니다. 지금까지 해왔던 '평범한 방식’으로 프로퍼티를 만들면 해당 프로퍼티의 플래그는 모두 true가 됩니다. 이렇게 true로 설정된 플래그는 언제든 수정할 수 있습니다.


```javascript
let user = {
  name: "John"
};

// bject.getOwnPropertyDescriptor(정보를 얻고자 하는 객체, 정보를 얻고자 하는 객체 내 프로퍼티)

let descriptor = Object.getOwnPropertyDescriptor(user, 'name');

alert( JSON.stringify(descriptor, null, 2 ) );
/* property descriptor:
{
  "value": "John",
  "writable": true,
  "enumerable": true,
  "configurable": true
}
*/
```
