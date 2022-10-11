# 함수

## 함수 데이터와 함수 호출

```js
function hello() {
  return 'Hello~'
}
console.log(hello) // ƒ hello() { return 'Hello~' }
console.log(hello()) // 'Hello~'
```

## 선언과 표현

### 함수 선언문(Declaration)

함수 선언문(Function declaration)은 `function` 키워드로 시작해 함수 이름을 필수로 지정하는 기명 함수입니다.

```js
function hello() {
  console.log('Hello~')
}
```

### 함수 표현식(Expression)

함수 표현식(Function expression)은 변수에 함수를 할당하는 것을 말합니다.

```js
const hello = function() {
  console.log('Hello~')
}
```

기명 함수 선언과 **동시에** 변수에 할당하면 표현식입니다.  
함수 선언의 이름은 제거됩니다.

```js
const exp = function dec() {}
exp() // OK!
dec() // Error..
```

### 호이스팅

호이스팅(Hoisting)은 선언부를 유효범위 최상위로 끌어올리는 현상을 말합니다.

- 함수 선언문은 호이스팅 O
- 함수 표현식은 호이스팅 X

```js
hello1()
hello2() // Error!

// 함수 선언문
function hello1() {
  console.log('Hello~1')
}

// 함수 표현식
const hello2 = function() {
  console.log('Hello~2')
}
```

## 반환 및 종료

`return` 키워드로 함수 안에서 밖으로 데이터를 반환할 수 있습니다.

```js
function hello() {
  return 'Hello~'
}
console.log(hello()) // 'Hello~'
```

`return` 키워드는 함수를 종료하기 때문에 그 이하 명령은 실행되지 않습니다.

```js
function hello() {
  return 'Hello~' // 함수 종료
  console.log('Wow!') // 동작하지 않음!
}
console.log(hello()) // 'Hello~'
```

`return` 키워드를 사용하지 않거나 반환 데이터를 생략하면, `undefined`가 반환됩니다.

```js
function hello1() {
  
}
function hello2() {
  return
}

console.log(hello1()) // undefined
console.log(hello2()) // undefined
```

```js
function plus(num) {
  if (!num) {
    console.log('숫자를 입력해주세요!')
    return 0
  }
  return num + 1
}

console.log(plus(2)) // 3
console.log(plus(7)) // 8
console.log(plus()) // undefined
```

## 매개변수 패턴(Parameter pattern)

기본값(Default value)

```js
function sum(a, b = 1) {
  return a + b
}
console.log(sum(2)) // 3
```

구조 분해 할당(Destructuring assignment)

```js
const user = {
  name: 'HEROPY',
  age: 85,
  // email: 'theseco@gmail.com'
}

function getName({ name }) {
  return name
}
function getEmail({ email = '이메일이 없습니다.' }) {
  return email
}

console.log(getName(user)) // 'HEROPY'
console.log(getEmail(user)) // '이메일이 없습니다.'
```

```js
const fruits = ['Apple', 'Banana', 'Cherry']
const numbers = [1, 2, 3, 4, 5, 6, 7]

function getSecondItem([,b]) {
  return b
}
console.log(getSecondItem(fruits)) // 'Banana'
console.log(getSecondItem(numbers)) // 2
```

나머지 매개변수(Rest parameter)

```js
function sum(...rest) {
  console.log(rest) // [1, 2, 3, 4, 5, 6, 7, 8]
  return rest.reduce((acc, cur) => acc + cur)
}

const res = sum(1, 2, 3, 4, 5, 6, 7, 8)
console.log(res) // 36
```

arguments 객체

`arguments` 객체는 모든 함수 내에서 이용 가능한 지역 변수로, 함수의 모든 인수를 참조할 수 있습니다.

```js
function sum() {
  let res = 0
  for (const item of arguments) {
    res += item
  }
  return res
}

const res = sum(1, 2, 3, 4, 5, 6, 7, 8)
console.log(res) // 36
```

## 화살표 함수(Arrow function)

단순하고 간결한 문법으로 함수를 사용할 수 있습니다.  
화살표 함수는 기본적으로 익명이며 표현식입니다.

```js
// 함수 표현
const sum = function(a, b) {
  return a + b
}

// 화살표 함수
const sum = (a, b) => a + b
```

```js
const log = function (c) {
  console.log(c)
}

const log = c => console.log(c)
```

```js
const a = () => {} // 매개변수가 없을 경우
const b = x => {} // 매개변수 1개는 소괄호 생략 가능
const c = (x, y) => {} // 매개변수가 없거가 2개 이상은 소괄호를 생략 불가
const d = x => { return x * x } 
const e = x => x * x // 함수가 `return`으로 시작하면 `{}`와 `return` 생략 가능
const f = x => { // 함수가 `return`으로 시작하지 않으면 생략 불가
  console.log(x * x)
  return x * x
}
const g = () => { return { a: 1 } }
const h = () => ({ a: 1 }) // 객체 데이터는 `{}` 기호를 사용하기 때문에 소괄호로 묶어야 함
const i = () => { return [1, 2, 3] }
const j = () => [1, 2, 3]
```

## 즉시실행함수(IIFE)

즉시실행함수(IIFE, Immediately-Invoked Function Expression)는 함수를 정의와 동시에 바로 실행하는 문법입니다.  
전역 범위의 변수 오염을 방지하거나 함수 외부에서 내부 변수에 접근하는 것을 차단하는 목적 등으로 활용할 수 있습니다.

```js
const a = 7

// 함수 정의(표현)
const double = () => {
  console.log(a * 2)
}
// 함수 실행(호출)
double()

// 함수 정의 및 실행
;(() => {
  console.log(a * 2)
})()
```

사용 가능한 패턴은 다음과 같습니다.  
화살표 함수는 한 가지 패턴만 사용 가능합니다.

```js
;(() => {})()        // (F)()
;(function () {})()  // (F)()
;(function () {}())  // (F())
;!function () {}()   // !F()
;+function () {}()   // +F()
```

외부에서는 즉시실행함수 내부 변수에 접근할 수 없습니다.

```js
const a = 7

;(() => {
  const b = 3
  console.log(a, b)
})()

console.log(a, b) // Error!
```

외부 변수를 다른 이름으로 사용할 수 있습니다.  
이 방식은 난독화 코드를 만들 때 사용하기도 합니다.

```js
;((a, b) => {
  console.log(a.innerWidth)
  console.log(b.body)
})(window, document)
```

## 콜백(Callback)

콜백(Callback)이란, 함수의 인수(값)로 사용되는 함수를 말합니다.

```js
const a = callback => {
  callback()
  console.log('A')
}
const b = () => {
  console.log('B')
}

a(b)
// 'B'
// 'A'
```

```js
function sum(a, b, callback) {
  // 1초 후 실행
  setTimeout(() => {
    callback(a + b)
  }, 1000)
}
sum(3, 7, function(value) {
  console.log(value) // 10
})
```

다음은 콜백을 활용한 이미지 로드 예제입니다.

```html
<div class="container">
  <h1>Loading...</h1>
</div>
```

```js
const loadImage = (url, cb) => {
  const imgEl = document.createElement('img')
  imgEl.src = url
  imgEl.addEventListener('load', () => {
    setTimeout(() => {
      cb(imgEl)
    }, 1000)
  })
}

const containerEl = document.querySelector('.container')
loadImage('https://www.gstatic.com/webp/gallery/4.jpg', imgEl => {
  containerEl.innerHTML = ''
  containerEl.append(imgEl)
})
```

## 재귀(Recursive)

재귀란 하나의 함수에서 자기 자신을 다시 호출해 실행하는 방법을 말합니다.

```js
let i = 0
const a = () => {
  console.log('A')
  i += 1
  if (i < 4) {
    a()
  }
}

a()
```

```js
const userA = { name: 'A', parent: null }
const userB = { name: 'B', parent: userA }
const userC = { name: 'C', parent: userB }
const userD = { name: 'D', parent: userC }

const getRootUser = user => {
  if (user.parent) {
    return getRootUser(user.parent)
  }
  return user
}

console.log(getRootUser(userD))
```

## 호출 스케줄링(Scheduling a function call)

```js
const hello = () => {
  console.log('Hello~')
}

const timeout = setTimeout(hello, 3000)
// const timeout = setInterval(hello, 1000)
const btnEl = document.querySelector('h1')

btnEl.addEventListener('click', () => {
  console.log('Clear!')
  clearTimeout(timeout)
  // clearInterval(timeout)
})
```

## this

`this`는 '일반 함수'와 '화살표 함수'에 따라 다르게 정의됩니다.  
<strong>일반 함수</strong>는 호출 위치에서 정의되고,  
<strong>화살표 함수</strong>는 this가 자신이 선언된 렉시컬(함수) 범위에서 정의됩니다.

```js
function user() {
  this.firstName = 'Neo'
  this.lastName = 'Anderson'
  
  return {
    firstName: 'Heropy',
    lastName: 'Park',
    age: 85,
    getFullName: function () {
      return `${this.firstName} ${this.lastName}`
    } 
  }
}

const u = user()
console.log(u.getFullName())
```

```js
let newC
let newD

// 객체 리터럴 선언!
const literal = {
  a: 1,
  b: 2,
  // 일반 함수는 호출 위치에서 따라 this 정의!
  c: function () {
    console.log(this.a)
  },
  // 화살표 함수는 this가 자신이 선언된 렉시컬(함수) 범위에서 this 정의!
  d: () => {
    console.log(this.a)
  }
}
literal.c() // 1
literal.d() // undefined
newC = literal.c
newD = literal.d
newC() // undefined
newD() // undefined
newC.call(literal) // 1
newD.call(literal) // undefined

// 인스턴스 생성!
const instance = new function () {
  this.a = 3
  this.b = 4
  // 일반 함수는 호출 위치에서 따라 this 정의!
  this.c = function () {
    console.log(this.a)
  }
  // 화살표 함수는 this가 자신이 선언된 렉시컬(함수) 범위에서 this 정의!
  this.d = () => {
    console.log(this.a)
  }
}
instance.c() // 3
instance.d() // 3
newC = instance.c
newD = instance.d
newC() // undefined
newD() // 3
newC.call(instance) // 3
newD.call(instance) // 3
```

```js
const timer = {
  title: 'TIMER!',
  timeout() {
    console.log(this.title)
    setTimeout(function () {
      console.log(this.title)
    }, 1000)
  }
}

timer.timeout()
```

### apply/call/bind

```js
const heropy = {
  name: 'Heropy'
}
const amy = {
  name: 'Amy',
  getName(age) {
    return `${this.name} is ${age}`
  }
}

// call
console.log(
  amy.getName.call(heropy, 85)
)
// apply
console.log(
  amy.getName.apply(heropy, [85])
)
// bind
const heropysGetName = amy.getName.bind(heropy)
console.log(heropysGetName(85))
```

## Function 클래스

`Function` 클래스로 함수를 생성할 수도 있습니다.

```js
const sum = new Function('a', 'b', `
  console.log(a)
  console.log(b)
  return a + b
`)
console.log(sum)
console.log(sum(1, 2))
```

```js
const str = 'console.log(123)' // 서버에서 동적으로 전달받은 문자열(코드 형태)
const fn = new Function(str)
fn()
```