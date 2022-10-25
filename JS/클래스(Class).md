# 클래스

## prototype

자바스크립트는 프로토타입 언어  
`array mdn` 구글 검색!

```js
// 인스턴스
const fruits = new Array('Apple', 'Banana', 'Cherry')

// 배열 인스턴스
// const fruits = ['Apple', 'Banana', 'Cherry'] (리터럴 방식)

console.log(fruits)
console.log(fruits.length) // 3
console.log(fruits.includes('Banana')) // true
console.log(fruits.includes('Orange')) // false

// heropy : 메소드
Array.prototype.heropy = function () {
  console.log(this)
  return this.map(item => item[0])
}

const newF = fruits.heropy()
console.log(newF)
```

```js
const heropy = {
  firstName: 'Heropy',
  lastName: 'Park',
  getFullName: function () {
    return `${this.firstName} ${this.lastName}`
  }
}
const neo = {
  firstName: 'Neo',
  lastName: 'Anderson'
}
console.log(heropy.getFullName())
console.log(heropy.getFullName.call(neo))
```

```js
// User : 클래스
function User(first, last) {
  this.firstName = first
  this.lastName = last
}
User.prototype.getFullName = function () {
  return `${this.firstName} ${this.lastName}`
}

const heropy = new User('Heropy', 'Park')
const neo = new User('Neo', 'Anderson')

console.log(heropy) // User {}
console.log(neo) // User {}
console.log(heropy.getFullName === neo.getFullName) // true
// 일치 연산자 (메모리 주소 비교)
```

## ES6 Classes

```js
class User {
  constructor(first, last) {
    this.firstName = first
    this.lastName = last
  }
  // 메소드 함수를 만들 때는 일반 함수로 만들기, 화살표 함수 X
  getFullName() {
    return `${this.firstName} ${this.lastName}`
  }
}

const heropy = new User('Heropy', 'Park')
const neo = new User('Neo', 'Anderson')

console.log(heropy)
console.log(neo)
console.log(heropy.getFullName === neo.getFullName) // true
```

### 화살표 함수 메소드

```js
class User {
  constructor(first, last) {
    this.firstName = first
    this.lastName = last
  }
  getFullName = () => {
    return `${this.firstName} ${this.lastName}`
  }
}

const heropy = new User('Heropy', 'Park')
const neo = new User('Neo', 'Anderson')

console.log(heropy)
console.log(neo)
console.log(heropy.getFullName === neo.getFullName) // false
```

## Getter, Setter

```js
class User {
  constructor(first, last) {
    this.firstName = first // 데이터
    this.lastName = last
  }
  // Getter
  get fullName() {
    return `${this.firstName} ${this.lastName}` // 계산된 데이터
  }
  // Setter(getter에 값을 할당하려고 할 때 사용)
  set fullName(value) {
    // ; : 문제가 생길 여지를 방지
    ;[this.firstName, this.lastName] = value.split(' ')
  }
}

const heropy = new User('Heropy', 'Park')
const neo = new User('Neo', 'Anderson')

console.log(heropy.fullName) // 'Heropy Park'
console.log(neo.fullName) // 'Neo Anderson'

heropy.fullName = 'Lewis Yang'
neo.fullName = 'Smith John'

console.log(heropy.firstName, heropy.lastName) // 'Lewis', 'Yang'
console.log(heropy.fullName) // 'Lewis Yang'

console.log(neo.firstName, neo.lastName) // 'Smith', 'John'
console.log(neo.fullName) // 'Smith John'
```

## 정적 메소드(Static methods)

정적 메소드는 주로 클래스의 유틸리티(보조) 함수를 만들 때 사용합니다.  
인스턴스와는 연결되지 않으며, 클래스 자체에서 호출해야 합니다.  
object는 거의 정적 메소드

`isArray mdn` 구글 검색!

```js
Array.isArray([1, 2, 3]) // true
Array.isArray({ a: 1 }) // false
```

```js
class User {
  constructor(first, last) {
    this.firstName = first
    this.lastName = last
  }
  getFullName() {
    return `${this.firstName} ${this.lastName}`
  }
  static isUser(user) {
    // if (user.firstName && user.lastName) return true
    // return false
    return !!user.firstName && !!user.lastName
  }
}

const heropy = new User('Heropy', 'Park')
const neo = new User('Neo', 'Anderson')
const lewis = {
  name: 'Lewis Yang',
  age: 85
}

console.log(heropy.getFullName())
console.log(neo.getFullName())
console.log(User.isUser(heropy)) // true
console.log(User.isUser(neo)) // true
console.log(User.isUser(lewis)) // false
```

프로토타입 기반의 정적 메소드

```js
function User(first, last) {
  this.firstName = first
  this.lastName = last
}
User.prototype.getFullName = function() {
  return `${this.firstName} ${this.lastName}`
}
User.isUser = function(user) {
  return !!user.firstName && !!user.lastName
}
```

## 상속(Inheritance)

```js
// 운송수단
class Vehicle {
  constructor(acceleration = 1) {
    this.speed = 0
    this.acceleration = acceleration
  }
  accelerate() {
    this.speed += this.acceleration
  }
  decelerate() {
    if (this.speed <= 0) {
      console.log('정지!')
      return
    }
    this.speed -= this.acceleration
  }
}


// 자전거
class Bicycle extends Vehicle {
  constructor(price = 100, acceleration) {
    super(acceleration)
    this.price = price
    this.wheel = 2
  }
}

const bicycle = new Bicycle(300)

bicycle.accelerate()
console.log(bicycle instanceof Bicycle) // true
console.log(bicycle instanceof Vehicle) // true
console.log(bicycle.constructor === Bicycle) // true
console.log(bicycle.constructor === Vehicle) // false


// 자동차
class Car extends Bicycle {
  constructor(license, price, acceleration) {
    super(price, acceleration)
    this.license = license
    this.wheel = 4
  }
  // 오버라이딩(Overriding)
  accelerate() {
    if (!this.license) {
      console.error('무면허!')
      return
    }
    this.speed += this.acceleration
    console.log('가속!', this.speed)
  }
}

const carA = new Car(true, 7000, 10)
const carB = new Car(false, 4000, 6)

carA.accelerate() // '가속!', 10
carB.accelerate() // '무면허!'
console.log(carA instanceof Car) // true
console.log(carA instanceof Bicycle) // true
console.log(carA instanceof Vehicle) // true
console.log(carA.constructor === Car) // true
console.log(carA.constructor === Bicycle) // false
console.log(carA.constructor === Vehicle) // false


// 보트
class Boat extends Vehicle {
  constructor(price, acceleration) {
    super(acceleration)
    this.price = price
    this.motor = 1
  }
}

const boat = new Boat(10000, 5)

console.log(boat instanceof Boat) // true
console.log(boat instanceof Vehicle) // true
console.log(boat instanceof Car) // false
console.log(boat instanceof Bicycle) // false
console.log(boat.constructor === Boat) // true
console.log(boat.constructor === Vehicle) // false
```

### 클래스와 프로토타입의 상속 비교

클래스 기반의 상속

```js
class User {
  constructor(name) {
    this.name = name
  }
  getName() {
    return this.name
  }
}

class Admin extends User {
  constructor(name) {
    super(name)
  }
}

const admin = new Admin('Heropy')
console.log(admin.getName()) // 'Heropy'
```

프로토타입 기반의 상속

```js
function User(name) {
  this.name = name
}
User.prototype.getName = function() {
  return this.name
}

function Admin(name) {
  User.call(this, name)
}
Admin.prototype = Object.create(User.prototype)
Admin.prototype.constructor = Admin

const admin = new Admin('Heropy')
console.log(admin.getName()) // 'Heropy'
```

### constructor, instanceof

```js
const fruits = ['Apple', 'Banana']
// const fruits = new Array('Apple', 'Banana')

console.log(fruits.constructor === Array)
console.log(fruits instanceof Array)
```

```js
class A {
  constructor() {}
}
class B extends A {
  constructor() {
    super()
  }
}
class C extends B {
  constructor() {
    super()
  }
}

const a = new A()
const b = new B()
const c = new C()

console.log(a instanceof A) // true
console.log(a instanceof B) // false
console.log(a instanceof C) // false

console.log(b instanceof A) // true
console.log(b instanceof B) // true
console.log(b instanceof C) // false

console.log(c instanceof A) // true
console.log(c instanceof B) // true
console.log(c instanceof C) // true

console.log(a.constructor === A) // true
console.log(a.constructor === B) // false
console.log(a.constructor === C) // false

console.log(b.constructor === A) // false
console.log(b.constructor === B) // true
console.log(b.constructor === C) // false

console.log(c.constructor === A) // false
console.log(c.constructor === B) // false
console.log(c.constructor === C) // true
```

## Fonty 예제

```js
class Fonty {
  #options
  constructor(selector, customOptions) {
    this.#options = {
      fontSize: '16px',
      fontStyle: 'normal',
      fontWeight: '400',
      fontFamily: 'sans-serif',
      lineHeight: '1.4'
    }

    // 언더바 : 밖에서 사용 금지
    this._allowedProperties = ['fontSize', 'fontStyle', 'fontWeight', 'fontFamily', 'lineHeight']
    this._selector = selector
    this.setStyle(customOptions)
  }
  setStyle(customOptions) {
    // 옵션 병합
    this._allowedProperties.forEach(name => {
      this.#options[name] = customOptions[name] || this.#options[name]
    })
    // 요소 검색
    this._els = document.querySelectorAll(this._selector)
    this._els.forEach(el => {
      Object.assign(el.style, this.#options)
    })
  }
  // Getter
  get options() {
    return this.#options
  }
  static getFamilies() {
    return ['serif', 'sans-serif', 'monospace', 'cursive']
  }
}

const f1 = new Fonty('.text1', {
  fontSize: '40px',
  fontWeight: '700'
})
const f2 = new Fonty('.text2', {
  fontSize: '30px',
  fontFamily: 'cursive',
  fontStyle: 'italic'
})

console.log(Fonty.getFamilies())

const h1El = document.querySelector('h1')
h1El.addEventListener('click', () => {
  f1.setStyle({
    fontSize: '24px',
    fontFamily: 'serif',
    lineHeight: 1
  })
  f2.setStyle({
    fontSize: '99px'
  })
  console.log(f2.options)
})
```