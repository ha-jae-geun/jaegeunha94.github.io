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


# 프로퍼티 플래그 변경
* Object.defineProperty(obj, propertyName, descriptor)
  * obj, propertyName: 설명자를 적용하고 싶은 객체와 객체 프로퍼티
  * descriptor: 적용하고자 하는 프로퍼티 설명자

```javascript
let user = {};

Object.defineProperty(user, "name", {
  value: "John"
});

let descriptor = Object.getOwnPropertyDescriptor(user, 'name');

alert( JSON.stringify(descriptor, null, 2 ) );
/*
{
  "value": "John",
  "writable": false,
  "enumerable": false,
  "configurable": false
}
 */
```

* defineProperty메서드는 객체에 해당 프로퍼티가 있으면 플래그를 원하는 대로 변경해줍니다. 프로퍼티가 없으면 인수로 넘겨받은 정보를 이용해 새로운 프로퍼티를 만듭니다. 이때 플래그 정보가 없으면 플래그 값은 자동으로 false가 됩니다.
  * ‘평범한 방식으로’ 객체 프로퍼티 user.name을 만들었을 때와 defineProperty를 이용해 프로퍼티를 만들었을 때의 가장 큰 차이점은 플래그에 있습니다. defineProperty를 사용해 프로퍼티를 만든 경우, descriptor에 플래그 값을 명시하지 않으면 플래그 값이 자동으로 false가 됩니다.  



## writable 플래그
```javascript
let user = {
  name: "John"
};

Object.defineProperty(user, "name", {
  writable: false
});

```
* user.name = "Pete"; // Error: Cannot assign to read only property 'name'
* 이제 defineProperty를 사용해 writable 플래그를 true로 변경하지 않는 한 그 누구도 객체의 이름을 변경할 수 없다.
* 에러는 엄격 모드에서만 발생합니다.



## enumerable 플래그

```javascript
let user = {
  name: "John",
  toString() {
    return this.name;
  }
};

//커스텀 toString은 for...in을 사용해 열거할 수 있습니다.
for (let key in user) alert(key); // name, toString
```

### enumberable 플래그 false
```javascript
let user = {
  name: "John",
  toString() {
    return this.name;
  }
};

Object.defineProperty(user, "toString", {
  enumerable: false
});

// 이제 for...in을 사용해 toString을 열거할 수 없게 되었습니다.
for (let key in user) alert(key); // name

열거가 불가능한 프로퍼티는 Object.keys에도 배제됩니다.
alert(Object.keys(user)); // name
```

* enumerable 플래그 값을 false로 설정하면 for..in 반복문에 나타나지 않게 할 수 있습니다.
