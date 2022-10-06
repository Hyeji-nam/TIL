# 구문(Statements)

## if(조건문)

`if`, `else` 키워드를 사용해 구문을 작성할 수 있습니다.

```js
if (조건) {
  // 조건이 참(truthy)일 때 실행될 코드
}

if (조건) {
  // 조건이 참일 때 실행될 코드
} else {
  // 조건이 거짓(falsy)일 때 실행될 코드
}

if (조건1) {
  // 조건1이 참일 때 실행될 코드
} else if (조건2) {
  // 조건2가 참일 때 실행될 코드
} else if (조건3) {
  // 조건3이 참일 때 실행될 코드
} else {
  // 모든 조건이 거짓일 때 실행될 코드
}
```

If

```js
// 함수 선언
function isPositive(number) {
  if (number > 0) {
    return '양수'
  }
}

// 함수 호출
console.log(isPositive(1)) // '양수'
console.log(isPositive(10)) // '양수'
console.log(isPositive(-2)) // undefined (함수는 기본값으로 undefined를 반환(return))
```

If else

```js
function isPositive(number) {
  if (number > 0) {
    return '양수'
  } else {
    return '음수'
  }
}

console.log(isPositive(1)) // '양수'
console.log(isPositive(10)) // '양수'
console.log(isPositive(-2)) // '음수'
```

If else if

```js
function isPositive(number) {
  if (number > 0) {
    return '양수'
  } else if (number < 0) {
    return '음수'
  } else {
    return '0'
  }
}

console.log(isPositive(1)) // '양수'
console.log(isPositive(10)) // '양수'
console.log(isPositive(-2)) // '음수'
console.log(isPositive(0)) // '0'
```

## switch
if보다 작은 범위입니다. if 조건보다 조금 더 나은(직관적인) 문법을 제공합니다.<br/>
`switch`, `case`, `break`, `default` 키워드를 사용해 구문을 작성할 수 있습니다.
`break` 키워드는 Switch 조건문을 종료합니다.

```js
switch (조건) {
  case 값1:
    // 조건이 '값1'일 때 실행
    break
  case 값2:
    // 조건이 '값2'일 때 실행
    break
  default:
    // 조건이 '값1'도 '값2'도 아닐 때 실행
}
```

```js
function price(fruit) {
  switch (fruit) {
    case 'Apple':
      return 1000 // return : 종료 & 반환 ** 함수 안에서만 사용!
    case 'Banana':
      return 1500
    case 'Cherry':
      return 2000
    default: // else와 비슷
      return 0
  }
}

// 함수 호출
console.log(price('Apple')) // 1000
console.log(price('Cherry')) // 2000
console.log(price('Hello')) // 0
```

Switch 조건문은 **항상** If 조건문으로 대체할 수 있습니다.

```js
function price(fruit) {
  if (fruit === 'Apple') {
    return 1000
  } else if (fruit === 'Banana') {
    return 1500
  } else if (fruit === 'Cherry') {
    return 2000
  } else {
    return 0
  }
}
```

## for(반복문)

```js
for (초기화; 조건; 증감) {
  // 실행 코드
}
```

```js
// 'i = i + 1' = 'i += 1'
for (let i = 0; i < 10; i += 1) {
  console.log(i)
}
// 0
// 1
// 2
// ...
// 9
```

### break

`break` 키워드가 실행되면, <u>전체</u> 반복을 종료합니다.

```js
for (let i = 0; i < 10; i += 1) {
  if (i > 5) {
    break
  }
  console.log(i)
}
// 0
// 1
// 2
// 3
// 4
// 5
```

### continue

`continue` 키워드가 실행되면, 현재 반복을 종료하고 다음 반복으로 넘어갑니다.
> **break 전체 종료 / continue 현재 종료

```js
for (let i = 0; i < 10; i += 1) {
  if (i % 2 === 0) {
    continue
  }
  console.log(i)
}
// 1
// 3
// 5
// 7
// 9
```

## for of

Iterable object(**반복 가능한 객체**)를 반복.  
`Array`, `Map`, `Set`, `String`, `TypedArray` 등..

```js
const users = [
  {
    name: 'Heropy',
    age: 85
  },
  {
    name: 'Neo',
    age: 22
  },
  {
    name: 'Lewis',
    age: 34
  }
]
// of 앞은 변수
for (const user of users) {
  console.log(user)
}
// { name: 'Heropy', age: 85 }
// { name: 'Neo', age: 22 }
// { name: 'Lewis', age: 34 }
```

## for in

객체 데이터를 반복.
> for of : 배열 (or 문자) 반복 / for in: 객체 반복

```js
const user = {
  name: 'Heropy',
  age: 85,
  isValid: true,
  email: 'thesecon@gmail.com'
}

for (const key in user) {
  console.log(key, user[key])
}
// name Heropy
// age 85
// isValid true
// email thesecon@gmail.com
```

## while

조건이 참인 동안 반복 실행합니다.

```js
while (조건) {
  // 
}
```

```js
let n = 0
while (n < 4) {
  console.log(n)
  n += 1
}
// 0
// 1
// 2
// 3
```

## do while

조건이 참인 동안 반복 실행합니다.

```js
do {
  
} while (조건)
```

```js
let n = 0
do {
  console.log(n)
  n += 1
} while (n < 4)
// 0
// 1
// 2
// 3
```

`do` 구문이 실행된 후 조건이 평가되기 때문에 <u>조건이 거짓이라도 한 번은 실행됩니다.</u>

```js
let n = 0
do {
  console.log(n)
  n += 1
} while (false)
// 0
```