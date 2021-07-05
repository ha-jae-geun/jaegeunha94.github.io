---
layout: post
toc: true
title: "자바스크립트 변수와 스코프, 메모리"
categories: javascript
tags: [javascript]
author:
  - Jack
---


# Call By Value

```javascript
const test = 1;

function change(val) { // callee
    val = 10;
}
change(test); // caller
console.log(test); // 1 출력
```
* argument로 value(값)이 넘어온다. 이때 넘어올 때는 "복사된 값"이 넘어옵니다.
* 호출하는 자가 인자를 복사해서 넘겨줬기 때문에 호출된 자에서 받은 인자를 아무리 수정하더라도 caller는 영향받지 않습니다.
* 인자를 넘겨줄 때마다 메모리 공간을 할당하기 때문에 공간을 잡아먹는 단점 존재합니다.



# Call By Reference

```javascript
const me = {
  name : 'Jimmy'
};
function changeName(person) {
  person.name = 'Joo'
};
console.log(me); // { name : 'Jimmy' }
changeName(me);
console.log(me); // {name : 'Joo' }
```

* 매개변수 person에 인수로 넘겨진 me의 참조값이 전달. 따라서 me와 person는 같은 참조값을 가지고 있다.
* changeName함수 안에서 person.name을 바꾸면 me.name도 변한다.
* 하지만 자바스크립트에서 무조건 Call By Value로 작동하기 때문에 참조타입으로 넘겨도 값이 변하지 않는다.
* 참조 타입을 인자로 넘기면 참조 값에 대한 복사본이 넘어가기 때문에 기존의 개념과는 다르기 때문에 알고 있어야 한다.
* argument로 reference가 넘어온다. (reference : 값에 대한 참조 주소, 메모리 주소를 담고 있는 변수)
* reference를 넘기다 보니 해당 reference가 가리키는 값을 복사하지는 않는다.
* caller는 인자를 복사해서 넘긴 것이 아니라 참조값을 넘겼기 떄문에 callee가 받은 인자를 수정하면 caller도 영향을 받는다.
* 메모리 공간 할당의 문제를 해결했으나, 원본 데이터 값을 훼손할 수 있다.
