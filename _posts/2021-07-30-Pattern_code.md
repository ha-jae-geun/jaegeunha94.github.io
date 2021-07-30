---
layout: post
toc: true
title: "Pattern_code"
categories: javascript
tags: [javascript]
author:
  - Jack
---

# 객체 리터럴에 의한 객체 생성 방식의 문제점
```javascript
const circle1 = {
  radius: 5,
  getDiameter() {
    return 2 * this.radius
  }
}

const circle2 = {
  radius: 5,
  getDiameter() {
    return 2 * this.radius
  }
}
```  


# 생성자 함수

```javascript
const test = new Test(1);
```



## 생성자 함수의 단점
```javascript
function Circle(radius) {
  this.getArea = function() {
    return Math.PI * this.radius ** 2;
  }
}

const circle1 = new Circle(1)
const circle2 = new Circle(2)

circle1.getArea == circle2.getArea // false

```



# 프로토타입 패턴

```javascript
function Circle(radius) {
  this.radius = radius;
}

Circle.prototype.getArea = function() {
  return Math.PI * this.radius ** 2
}

const circle1 = new Circle(1)
const circle2 = new Circle(2)

// 프로토타입 Circle.prototype으로 부터 getArea 메서드를 상속받는다.
// Circle 생성자 함수가 생성하는 모든 인스턴스는 하나의 getArea 메서드를 공유한다.

console.log(circle1.getArea === circle2.getArea); // true
```


# 프로토타입 패턴 주의할 점
```javascript
function Person() {}

Person.prototype = {
  friends : ["jaegeun", "test"]
}

var person1 = new Person();
var person2 = new Person();

person1.friends.push("Van")
console.log(person2.friends)

```  


## 해결
```javascript
function Person() {
  this.friends = ["jaegeun", "test"]
}

Person.prototype = {
  constructor: Person
}

var person1 = new Person();
var person2 = new Person();

console.log(person1.friends === person2.friends);
```



# ES5 프로토타입 패턴 
```javascript
var Circle = function (id, x, y) {
   this.id = id;
   this.move(x, y);
};
Circle.prototype.move = function (x, y) {
   this.x = x;
   this.y = y;
};
 
```  

## ES6 프로토타입 패턴
```javascript

class Circle {
  constructor (id, x, y) {
    this.id = id
    this.move(x, y)
  }
  move (x, y) {
    this.x = x
    this.y = y
  }
}
```


# 생성자 패턴과 프로토타입 패턴의 조합
  
```javascript
function Person(name, age, job) {
  this.name = name;
}

Person.prototype = {
  constructor: Person,
  sayName: function () {
    alert(this.name);
  }
}
```

# 프로토타입 프로퍼티 제거 예제
```javascript
function Person() {}

Person.prototype.name = 'jaegeun'

var person1 = new Person();

person1.name = "jg"

alert(person1.name)

delete person1.name;

alert(person1.name)

```

