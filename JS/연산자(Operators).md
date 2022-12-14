# 연산자(Operators)

연산자(operator)는 `+`, `-`, `*`, `=`, `===`, `!` 같은 기호로, 이는 더하기, 빼기, 곱하기, 할당, 비교, 부정 등의 의미를 가집니다. 

## 산술(Arithmetic)

```js
// 피연산자 연산자 피연산자
console.log(1 + 2)  // 3
console.log(5 - 7)  // -2
console.log(3 * 4)  // 12
console.log(10 / 2) // 5
console.log(7 % 5)  // 2
```

## 할당(Assignment)

```js
let a = 3

// a = a + 2
a += 2

// a = a - 2
a -= 2

// a = a * 2
a *= 2

// a = a / 2
a /= 2

// a = a % 2
a %= 2

console.log(a) // 5, 1, 6, 1.5, 1
```

## 증감(Increment & Decrement)

증감 연산자는 `1`을 더하거나 빼는 연산자입니다.

```js
// 증가 연산자
// ++ 기호가 뒤에 있는 경우,
let a = 3

console.log(a++) // 3
console.log(a) // 4


// ++ 기호가 앞에 있는 경우,
let a = 3

console.log(++a) // 4
console.log(a) // 4
```

```js
// 감소 연산자
// -- 기호가 뒤에 있는 경우,
let a = 3

console.log(a--) // 3
console.log(a) // 2


// -- 기호가 앞에 있는 경우,
let a = 3

console.log(--a) // 2
console.log(a) // 2
```

증감 연산자는 변수 앞뒤 위치에 따라 다른 결과가 만들어지기 때문에, 직관적으로 더하기할당(`+=`) 혹은 빼기할당(`-=`) 연산자를 사용하는 것도 좋습니다. 

```js
let a = 3

a += 1
console.log(a) // 4

a -= 1
console.log(a) // 3
```

## 부정(Negation)

참(Truthy)과 거짓(Falsy)의 반댓값을 불린(Boolean) 데이터로 반환합니다.

```js
console.log(!true) // false
console.log(!false) // true

// 중첩 사용
console.log(!0) // true
console.log(!!0) // false
console.log(!!!0) // true
console.log(!!!!0) // false

// Falsy
console.log(!null) // true
console.log(!NaN) // true
console.log(!undefined) // true
console.log(!'') // true

// Truthy
console.log(!{}) // false
console.log(![]) // false
console.log(!'A') // false
```

## 비교(Comparison)

```js
const a = 1
const b = 3

// 동등(형 변환!)
console.log(a == b) // false

// 부등(형 변환!)
console.log(a != b) // true

// 일치
console.log(a === b) // false

// 불일치
console.log(a !== b) // true

// 큼(greater than)
console.log(a > b) // false

// 크거나 같음
console.log(a >= b) // false

// 작음(less than)
console.log(a < b) // true

// 작거나 같음
console.log(a <= b) // true
```

## 논리(Logical)

```js
// AND 연산자
// 그리고 연산자는
// 제일 먼저 만나는 거짓 데이터를 반환
// 모두 참일 경우 마지막 데이터를 반환
const a = true
const b = false

if (a && b) {
  console.log('모두 참!') // 출력 X
}

console.log(a && b) // false
```

```js
// OR 연산자
const a = true
const b = false

if (a || b) {
  console.log('하나 이상 참!') // 출력 O
}

console.log(a || b) // true
```

AND 연산자는 왼쪽에서부터 가장 먼저 만나는 거짓(Falsy) 데이터를 반환합니다.  
끝까지 거짓이 없으면 가장 오른쪽의 마지막 참(Truthy) 데이터를 반환합니다.

```js
// AND 연산자
console.log(true && false) // false
console.log(1 && 0) // 0
console.log(1 && 2 && 0) // 0
console.log(1 && 0 && 2) // 0
console.log(0 && 1 && 2) // 0
console.log('A' && 'B' && '') // ''
console.log('A' && 'B' && 'C') // 'C'
```

OR 연산자는 왼쪽에서부터 가장 먼저 만나는 <u>참(Truthy) 데이터</u>를 반환합니다. 
끝까지 참이 없으면 가장 오른쪽의 마지막 거짓(Falsy) 데이터를 반환합니다.

```js
// OR 연산자
console.log(false || true) // true
console.log(0 || 1) // 1
console.log(false || 0 || {}) // {}
console.log(false || [] || null) // []
console.log(function () {} || undefined || '') // f () {}
console.log(false || 0 || NaN) // NaN
```

## Nullish 병합(Nullish Coalescing)

OR 연산자(`||`)는 왼쪽에서부터 거짓(Falsy)를 만나면 다음으로 넘어가지만, `0`이나 `''`(빈 문자) 값을 유효 값으로 사용하는 경우 원치 않는 결과가 발생할 수 있습니다.   
이때 연산자(`??`)를 사용하면, Nullish(`null`과 `undefined`)를 만났을 때만 다음으로 넘어가기 때문에 유용합니다.  

```js
const n = 0

// OR 연산자
const num1 = n || 7
console.log(num1) // 7

// Nullish 병합 연산자
const num2 = n ?? 7
console.log(num2) // 0
```

```js
console.log(null ?? 1) // 1
console.log(undefined ?? 2) // 2
console.log(null ?? undefined) // undefined
console.log(null ?? 1 ?? 2) // 1
console.log(false ?? 1 ?? 2) // false
console.log(0 ?? 1 ?? 2) // 0
```

## 삼항(Ternary) (중요!!)

```js
const a = 1

if (a < 2) {
  console.log('참!')
} else {
  console.log('거짓..')
}

// 조건 ? 값1 : 값2
console.log(a < 2 ? '참!' : '거짓..')
```

```js
// message: undefined(암시적)
function getAlert(message) {
  return message ? message : '메시지가 존재하지 않습니다!'
}

console.log(getAlert('안녕하세요~')) // '안녕하세요~'
console.log(getAlert()) // '메시지가 존재하지 않습니다!'
```

## 전개 연산자(Spread Operator) (사용 多)

배열이나 객체의 아이템이나 속성을 전개(확장)할 수 있습니다.  
얕은 복사에 유용합니다.

#### 배열 병합

```js
const a = [1, 2, 3]
const b = [4, 5, 6]
const c = a.concat(b)
// 배열 리터럴 방식
const d = [...a, ...b]

console.log(c) // [1, 2, 3, 4, 5, 6]
console.log(d) // [1, 2, 3, 4, 5, 6]
```

#### 객체 병합

```js
const a = { x: 1, y: 2 }
const b = { y: 3, z: 4 }
// a, b 객체의 내용을 병합해서 새로운 객체 생성
const c = Object.assign({}, a, b)
const d = { ...a, ...b }

console.log(c) // { x: 1, y: 3, z: 4 }
console.log(d) // { x: 1, y: 3, z: 4 }
```

#### 인수 전개

```js
const a = [1, 2, 3]
function fn(x, y, z) {
  console.log(x, y, z)
}
fn(...a)
// 1 2 3
```

#### 나머지 매개변수

```js
const a = [1, 2, 3, 4, 5, 6]
// ...rest : 나머지 매개변수
function fn(x, y, ...rest) {
  console.log(x, y, rest)
}
fn(...a)
// 1 2 [3, 4, 5, 6]
```

## 구조 분해 할당(Destructuring assignment)

배열이나 객체의 구조에 맞게 바로 개별 변수에 값을 할당하는 방법입니다.

### 배열 구조 분해(Array destructuring)

#### 기본

```js
// 배열 데이터는 순서가 존재, 객체는 X
const arr = [1, 2, 3]
const [a, b, c] = arr

console.log(a, b, c) 
// 1 2 3
```

#### 선언과 분리

```js
const arr = [1, 2, 3]
let a, b, c
[a, b, c] = arr

console.log(a, b, c) 
// 1 2 3
```

#### 기본값

```js
const arr = [, , 3]
// 기본값을 지정할 땐 '=' 사용
const [a = 0, b, c] = arr

console.log(a, b, c)
// 0 undefined 3
```

#### 변수 값 교환

```js
let a = 1
let b = 2
;[b, a] = [a, b]

console.log(a, b) 
// 2 1
```

#### 반환 값 무시

```js
const arr = [1, 2, 3]
const [,, c] = arr

console.log(c) 
// 3
```

#### 나머지 할당

```js
const arr = [1, 2, 3]
const [a, ...rest] = arr

console.log(a, rest) 
// 1 [2, 3]
```

### 객체 구조 분해(Object destructuring)

#### 기본

```js
const obj = { a: 1, b: 2, c: 3 }
const { a, b, c } = obj

console.log(a, b, c) 
// 1 2 3
```

#### 선언과 분리

```js
const obj = { a: 1, b: 2, c: 3 }
let a, b, c
({ a, b, c } = obj) // 소괄호 묶음!

console.log(a, b, c)
// 1 2 3
```

#### 기본값

```js
const obj = { c: 3 }
const { a = 0, b, c } = obj

console.log(a, b, c) 
// 0 undefined 3
```

#### 변수명 변경

```js
const obj = { a: 1, b: 2, c: 3 }
const { a: x, b: y, c: z } = obj

console.log(x, y, z) 
// 1 2 3
```

#### 기본값 + 변수명 변경

```js
const obj = { c: 3 }
const { a: x = 0, b: y, c: z } = obj

console.log(x, y, z) 
// 0 undefined 3
```

#### 나머지 할당

```js
const obj = { a: 1, b: 2, c: 3 }
const { a, ...rest } = obj

console.log(a, rest) 
// 1 { b: 2, c: 3 }
```

## 선택적 체이닝(Optional Chaining)

점 표기법에 `?`를 추가해 `?.`로 사용하면 객체 속성이 없는 경우도 에러 없이 접근할 수 있습니다.  
필요한 곳에서 사용하되, 추적이 어려워질 수 있으니 남용하지 않도록 주의해야 합니다.

```js
let user = null

console.log(user) // null
console.log(user?.name) // undefined
```

```js
const userA = {
  name: 'HEROPY',
  age: 85,
  address: {
    country: 'Korea',
    city: 'Seoul'
  }
}
const userB = {
  name: 'Neo',
  age: 22
}

function getCity(user) {
  return user.address?.city || '주소 없음.'
}

console.log(getCity(userA)) // 'Seoul'
console.log(getCity(userB)) // '주소 없음.'
```

