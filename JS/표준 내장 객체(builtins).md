# 표준 내장 객체

## String

### .length

문자의 길이(숫자)를 반환합니다.

```js
const str = 'Hello world!'
//           012345678901

console.log(str.length) // 12
```

### .includes()

대상 문자에 주어진 문자가 포함되어 있는지(불린) 확인합니다.

```js
const str = 'Hello world!'

console.log(str.includes('Hello')) // true
```

찾기 시작할 위치를 두 번째 인수로 추가할 수 있습니다.  
기본값은 `0`입니다.

```js
const str = 'Hello world!'
//           012345678901

console.log(str.includes('Hello', 1)) // false
```

### .indexOf()

대상 문자에서 주어진 문자와 일치하는 첫 번째 인덱스(숫자)를 반환합니다.  
일치하는 문자가 없으면 `-1`을 반환합니다.

```js
const str = 'Hello world!'
//           012345678901

console.log(str.indexOf('world')) // 6
console.log(str.indexOf('HEROPY')) // -1
```

### .match()

대상 문자에서 주어진 정규식(RegExp)과 일치하는 배열을 반환합니다.

```js
const str = 'Hello world!'

console.log(str.match(/^.*(?=\s)/gi)) // ['Hello']
```

### .padStart()

대상 문자의 길이(length)가 지정된 길이보다 작으면,  
주어진 문자를 지정된 길이가 될 때까지 **앞에** 붙여 새로운 문자를 반환합니다.

```js
const str = '1234567'

console.log(str.padStart(10, '0')) // '0001234567'
console.log(str) // '1234567'
```

### .padEnd()

대상 문자의 길이(length)가 지정된 길이보다 작으면,  
주어진 문자를 지정된 길이가 될 때까지 **끝에** 붙여 새로운 문자를 반환합니다.

```js
const str = '1234567'

console.log(str.padEnd(10, '0')) // '1234500000'
console.log(str) // '1234567'
```

### .replace()

대상 문자에서 패턴(문자, 정규식(= 정규 표현식))과 일치하는 부분을 교체한 새로운 문자를 반환합니다.

```js
const str = 'Hello, Hello?!'

console.log(str.replace('Hello', 'Hi')) // 'Hi, Hello?!'
console.log(str.replace(/Hello/g, 'Hi')) // 'Hi, Hi?!'
console.log(str) // 'Hello, Hello?!'
```

### .search()

대상 문자에서 정규식과 일치하는 첫 번째 인덱스(숫자)를 반환합니다.

```js
const str = 'Hello world!'
//           012345678901
// \s : 공백 문자
console.log(str.search(/\s/)) // 5
```

### .slice()

대상 문자의 일부를 추출해 새로운 문자를 반환합니다.  
두 번째 인수 **직전**까지 추출하고, 두 번째 인수를 생략하면 대상 문자의 끝까지 추출합니다.

```js
const str = 'Hello world!'
//           012345678901
//          -210987654321

console.log(str.slice(0, 5)) // 'Hello'
console.log(str.slice(6, -1)) // 'world'
console.log(str.slice(6)) // 'world!'
console.log(str) // 'Hello world!'
```

### .split()

대상 문자를 주어진 구분자로 나눠 **배열**로 반환합니다.

```js
const str = 'Apple, Banana, Cherry'

console.log(str.split(', ')) // ['Apple', 'Banana', 'Cherry']
```

```js
const str = 'Apple'

console.log(str.split('').reverse().join('')) // elppA
```

### .startsWith()

대상 문자가 주어진 문자로 시작하는지 여부를 반환합니다.  
탐색할 시작 위치를 지정할 수 있습니다.

```js
const str = 'Hello world!'

console.log(str.startsWith('Hello')) // true
console.log(str.startsWith('world')) // false
console.log(str.startsWith('world', 6)) // true
````

### .toLowerCase()

대상 문자를 영어 소문자로 변환해 새로운 문자로 반환합니다.

```js
const str = 'Apple, Banana, Cherry'

console.log(str.toLowerCase()) // 'apple, banana, cherry'
console.log(str) // 'Apple, Banana, Cherry'
```

### .toUpperCase()

대상 문자를 영어 대문자로 변환해 새로운 문자로 반환합니다.

```js
const str = 'Apple, Banana, Cherry'

console.log(str.toUpperCase()) // 'APPLE, BANANA, CHERRY'
console.log(str) // 'Apple, Banana, Cherry'
```

### .trim()

대상 문자의 앞뒤 공백 문자(space, tab 등)를 제거한 새로운 문자를 반환합니다.  
(문자 사이에 있는 공백은 없애지 않음)

```js
const str = '   Hello world!  '

console.log(str.trim()) // 'Hello world!'
console.log(str) // '   Hello world!  '
```


---
## Number

### .toFixed()

숫자를 지정된 고정 소수점 표기(자릿수)까지 표현하는 <u>문자</u>로 반환합니다.

```js
const num = 3.1415926535

console.log(num.toFixed(2)) // '3.14'
console.log(parseFloat(num.toFixed(2))) // 3.14
```

### .toLocaleString()

숫자를 현지 언어 형식의 문자로 반환합니다.

```js
const num = 1000000

console.log(num.toLocaleString()) // '1,000,000'

// 템플릿 리터럴
console.log(`${num.toLocaleString()}원`) // '1,000,000원'
```

### Number.isInteger()

숫자가 정수(integer)인지 확인합니다.  
정적 메소드입니다.  
많은 경우 `is`로 시작하는 메소드는 불린 데이터를 반환합니다.

```js
const num = 123
const pi = 3.14

console.log(Number.isInteger(num)) // true
console.log(Number.isInteger(pi)) // false
```

### Number.isNaN() 또는 isNaN() (isNaN()은 전역함수)

주어진 값이 `NaN`인지 확인합니다.  
`isNaN()`보다 더 엄격한 버전으로 ES6에 추가된 `Number.isNaN()` 사용을 권장합니다.  
(Number라는 네임스페이스(namespace 추가 됨), 이름으로 지정된 특정한 범위)

```js
const num1 = NaN // 숫자 데이터, 사용자들에게는 보여지면 안 됨
const num2 = 123
const str = 'Hello world'
const nul = null // 예약어

// 정적 메소드는 클래스의 보조 역할

console.log(Number.isNaN(num1)) // true
console.log(Number.isNaN(num2)) // false
console.log(Number.isNaN(str)) // false
console.log(Number.isNaN(nul)) // false
```

### Number.parseInt() 또는 parseInt()

주어진 값(숫자, 문자)을 파싱(분석)해 특정 진수(radix)의 정수로 반환합니다.  
`Number.parseInt()`는 ES6에서 전역 객체의 모듈화를 위해 추가됐습니다.  
10진수가 기본값이 아니기 때문에 꼭 명시하는 것이 좋습니다! (중요)  
기능 면에서 동일하기 때문에 둘 중 어느 것을 사용해도 무방합니다.

```js
const str = '3.1415926535'
const num = 3.1415926535

// 10진수 정수로 반환!
console.log(Number.parseInt(str, 10)) // 3
console.log(Number.parseInt(num, 10)) // 3
```

다음과 같은 경우 `NaN`를 반환합니다.

- 진수 값이 `2`보다 작거나 `36`보다 큰 경우
- 공백이 아닌 첫 문자를 숫자로 변환할 수 없는 경우

### Number.parseFloat() 또는 parseFloat()

주어진 값(숫자, 문자)을 파싱해 부동소수점 실수로 반환(숫자)합니다.  
`Number.parseFloat()`는 ES6에서 전역 객체의 모듈화를 위해 추가됐습니다.  

```js
const str = '3.1415926535'
const num = 3.1415926535

console.log(Number.parseFloat(str)) // 3.1415926535
console.log(Number.parseFloat(num)) // 3.1415926535
```


---
## Math

### Math.abs()

주어진 숫자의 절댓값을 반환합니다.

```js
console.log(Math.abs(2)) // 2
console.log(Math.abs(-2)) // 2
```

### Math.ceil()

주어진 숫자를 올림해 정수를 반환합니다.

```js
console.log(Math.ceil(3.1415926535)) // 4
```

### Math.floor()

주어진 숫자를 내림해 정수를 반환합니다.

```js
console.log(Math.floor(3.1415926535)) // 3
```

### Math.round()

주어진 숫자를 반올림해 정수를 반환합니다.

```js
const num1 = 3.141
const num2 = 3.768

console.log(Math.round(num1)) // 3
console.log(Math.round(num2)) // 4
```

### Math.max()

주어진 숫자 중 가장 큰 숫자를 반환합니다.

```js
console.log(Math.max(1, 22, 38, 192)) // 192
```

### Math.min()

주어진 숫자 중 가장 작은 숫자를 반환합니다.

```js
console.log(Math.min(1, 22, 38, 192)) // 1
```

### Math.pow()

주어진 숫자의 거듭제곱한 값을 반환합니다.

```js
console.log(Math.pow(4, 2)) // 16
console.log(Math.pow(7, 2)) // 49
console.log(Math.pow(10, 3)) // 1000
```

### Math.random()

`0` 이상 `1` 미만의 난수를 반환합니다.

```js
console.log(Math.random()) // 0.6903810349799351

// 특정 범위의 무작위 정수를 얻는 함수
// 0~9 사이 정수
function random(min = 0, max = 10) {
  return Math.floor(Math.random() * (max - min)) + min
}

console.log(random()) // 0~9
console.log(random(11, 20)) // 11~19
console.log(random(101, 1000)) // 101~999

//// 원리! ////
// const ran = Math.random()
// const max = 5
// const min = 1
// 
// console.log(ran) // 무작위 수 생성!
// console.log(ran * (max - min)) // 최댓값 만들기!
// console.log(Math.floor(ran * (max - min))) // 소수점 내림!
// console.log(Math.floor(ran * (max - min)) + min) // 최솟값 만들기!
```

---
## Date

### 개요
(E.g. moment js, day js)  
`new Date()`를 통해 반환되는 인스턴스를 '타임스탬프'(Timestamp)라고 합니다.

```js
const date = new Date()
console.log(date)
// 타임스탬프 - 'Wed Sep 28 2022 10:45:41 GMT+0900 (한국 표준시)'
```

```js
// 월(month)는 -1 처리됨
const d1 = new Date(2022, 11, 16, 12, 57, 30)
console.log(d1) // 'Fri Dec 16 2022 12:57:30 GMT+0900 (한국 표준시)'

const d2 = new Date('Fri Dec 16 2022 12:57:30 GMT+0900 (한국 표준시)')
console.log(d2) // 'Fri Dec 16 2022 12:57:30 GMT+0900 (한국 표준시)'
```

### .getFullYear()와 .setFullYear()

날짜 인스턴스의 '연도'를 반환하거나 지정합니다.

```js
const date = new Date()

console.log(date.getFullYear()) // 2022

date.setFullYear(2023)
console.log(date.getFullYear()) // 2023
console.log(date) // 'Thu Sep 28 2023 14:23:23 GMT+0900 (한국 표준시)'
```

### .getMonth()와 .setMonth()

날짜 인스턴스의 '월'을 반환하거나 지정합니다.  
0부터 시작(Zero-based numbering)합니다.

```js
const date = new Date()

console.log(date.getMonth()) // 8
console.log(date) // 'Wed Sep 28 2022 15:26:49 GMT+0900 (한국 표준시)'

date.setMonth(0)
console.log(date.getMonth()) // 0
console.log(date) // 'Fri Jan 28 2022 14:26:33 GMT+0900 (한국 표준시)'
```

### .getDate()와 .setDate()

날짜 인스턴스의 '일'을 반환하거나 지정합니다.

```js
const date = new Date()

console.log(date.getDate()) // 28
console.log(date) // 'Wed Sep 28 2022 15:35:14 GMT+0900 (한국 표준시)'

date.setDate(11)
console.log(date.getDate()) // 11
console.log(date) // 'Mon Sep 11 2022 12:03:40 GMT+0900 (한국 표준시)'
```

### .getHours()와 .setHours()

날짜 인스턴스의 '시간'을 반환하거나 지정합니다.

```js
const date = new Date()

console.log(date.getHours()) // 14
console.log(date) // 'Wed Dec 21 2022 14:23:51 GMT+0900 (한국 표준시)'

date.setHours(7)
console.log(date.getHours()) // 7
console.log(date) // 'Wed Dec 21 2022 07:23:51 GMT+0900 (한국 표준시)'
```

### .getMinutes()와 .setMinutes()

날짜 인스턴스의 '분'을 반환하거나 지정합니다.

```js
const date = new Date()

console.log(date.getMinutes()) // 25
console.log(date) // 'Wed Sep 28 2022 15:25:33 GMT+0900 (한국 표준시)'

date.setMinutes(2)
console.log(date.getMinutes()) // 2
console.log(date) // 'Wed Sep 28 2022 15:02:33 GMT+0900 (한국 표준시)'
```

### .getSeconds()와 .setSeconds()

날짜 인스턴스의 '초'를 반환하거나 지정합니다.

```js
const date = new Date()

console.log(date.getSeconds()) // 13
console.log(date) // 'Wed Sep 28 2022 15:50:13 GMT+0900 (한국 표준시)'

date.setSeconds(57)
console.log(date.getSeconds()) // 57
console.log(date) // 'Wed Sep 28 2022 15:50:57 GMT+0900 (한국 표준시)'
```

### .getDay()

날짜 인스턴스의 '요일'을 반환합니다.  
(일 : Date, 요일 : Day)

```js
const date = new Date()
const day = date.getDay()

console.log(day) // 3
console.log(getDayKo(day)) // '수요일'

function getDayKo(day) {
  switch (day) {
    case 0: return '일요일'
    case 1: return '월요일'
    case 2: return '화요일'
    case 3: return '수요일'
    case 4: return '목요일'
    case 5: return '금요일'
    case 6: return '토요일'
  }
}
```

### .getTime()와 .setTime()

`1970-01-01 00:00:00`(유닉스타임)부터 경과한,  
날짜 인스턴스의 '밀리초(ms)'로 반환하거나 지정합니다.

```js
const date = new Date()

console.log(date.getTime()) // 1664343325817
console.log(date) // 'Wed Sep 28 2022 15:58:05 GMT+0900 (한국 표준시)'

date.setTime(1700000000000)
console.log(date.getTime()) // 1700000000000
console.log(date) // 'Wed Nov 15 2023 07:13:20 GMT+0900 (한국 표준시)'
```

```js
Date.prototype.isAfter = function (date) {
  const a = this.getTime()
  const b = date.getTime()
  return a > b
}

const d1 = new Date('Sat Jan 01 2022 00:00:00 GMT+0900 (한국 표준시)')
const d2 = new Date('Sun Jan 01 2023 00:00:00 GMT+0900 (한국 표준시)')

console.log(d1.isAfter(d2)) // false
console.log(d2.isAfter(d1)) // true
```

### .toUTCString()

날짜 인스턴스의 협정 세계시(UTC)를 반환합니다.  
협정 세계시(UTC) 혹은 그리니치 평균시(GMT)는 영국 런던 기점, 뉴질랜드 웰링턴 종점의 기준시입니다.  
한국은 UTC 기준보다 9시간 빠릅니다.

```js
console.log(new Date())
// Tue Oct 25 2022 16:29:54 GMT+0900 (한국 표준시)

console.log(new Date().toUTCString())
// Tue, 25 Oct 2022 07:29:54 GMT
```

### .toISOString()

날짜 인스턴스의 협정 세계시(UTC)를 'ISO 8601' 포맷으로 반환합니다.  
'ISO 8601'는 날짜와 시간을 표현하는 국제 표준 규격입니다.

```js
console.log(new Date())
// Tue Oct 25 2022 16:29:54 GMT+0900 (한국 표준시)

console.log(new Date().toISOString())
// 2022-10-25T07:29:54.000Z
```

### Date.now()

유닉스 타임(UNIX Time)으로부터 메소드가 호출될 때의 경화한 시간을 '밀리초(ms)'로 반환합니다.  
유닉스 타임이란 1970년 1월 1일 00:00:00 UTC 로부터 현재까지의 누적된 초(seconds) 값을 의미한다.

```js
const time = new Date().getTime()
console.log(Date.now()) // 1664349597861
console.log(time)       // 1664349597861

setTimeout(() => {
  console.log(Date.now()) // 1664349598861
  console.log(time)       // 1664349597861
}, 1000)
```


---
## Array

### .length

배열의 길이(숫자)를 반환합니다.

```js
const arr = ['A', 'B', 'C']

console.log(arr.length) // 3
```

### .at()

대상 배열을 인덱싱합니다.  
음수 값을 사용하면 뒤에서부터 인덱싱합니다.

```js
const arr = ['A', 'B', 'C']

console.log(arr[0]) // 'A'
console.log(arr.at(0)) // 'A'

console.log(arr[arr.length - 1]) // 'C'
console.log(arr.at(-1)) // 'C'
```

### .concat()

대상 배열과 주어진 배열을 병합해 새로운 배열을 반환합니다.

```js
const arr1 = ['A', 'B', 'C']
const arr2 = ['D', 'E', 'F']
const arr3 = arr1.concat(arr2)
// 전개 연산자
// const arr3 = [...arr1, ...arr2]

console.log(arr1) // ['A', 'B', 'C']
console.log(arr2) // ['D', 'E', 'F']
console.log(arr3) // ['A', 'B', 'C', 'D', 'E', 'F']
```

### .every()

대상 배열의 모든 요소가 콜백 테스트를 통과(참(Truthy)을 반환)하는지 확인합니다.

```js
const arr = [1, 2, 3, 4]
const isValid = arr.every(item => item < 5)

console.log(isValid) // true
```

### .filter()

대상 배열에서 콜백 테스트를 통과하는 모든 요소로 새로운 배열을 만들어 반환합니다.  
만약 모든 요소가 테스트를 통과하지 못하면 빈 배열을 반환합니다.

```js
const numbers = [1, 20, 7, 9, 104, 0, 58]
const filteredNumbers = numbers.filter(number => number < 30)

// filter 메소드는 원본 데이터보다 개수가 작을 수 있다.
console.log(filteredNumbers) // [1, 20, 7, 9, 0]
```

```js
const users = [
  { name: 'Neo', age: 85 },
  { name: 'Amy', age: 22 },
  { name: 'Lewis', age: 11 }
]
const adults = users.filter(user => user.age >= 19)
console.log(adults) // [ Neo객체, Amy객체 ]
```

### .find()

대상 배열에서 콜백 테스트를 통과하는 첫 번째 요소를 반환합니다.  
최초로 테스트가 통과하면, 이후 콜백은 실행되지 않습니다.  
모든 테스트가 실패하면, `undefined`를 반환합니다.

```js
const arr = [5, 8, 130, 12, 44]
const foundItem = arr.find(item => item > 10)

console.log(foundItem) // 130
```

```js
const users = [
  { name: 'Neo', age: 85 },
  { name: 'Amy', age: 22 },
  { name: 'Lewis', age: 11 }
]
const foundUser = users.find(user => user.name === 'Amy')

console.log(foundUser) // { name: 'Amy', age: 22 }
```

### .findIndex()

대상 배열에서 콜백 테스트를 통과하는 첫 번째 요소의 인덱스를 반환합니다.
최초로 테스트가 통과하면, 이후 콜백은 실행되지 않습니다.  
모든 테스트가 실패하면, `-1`을 반환합니다.

```js
const arr = [5, 8, 130, 12, 44]
//           0  1  2    3   4

const index = arr.findIndex(item => item > 10)

console.log(index) // 2
```

### .flat()

대상 배열의 모든 하위 배열을 지정한 깊이(Depth)까지 이어붙인 새로운 배열을 반환합니다.
깊이의 기본값은 `1`입니다.

```js
const arr = [1, 2, [3, 4]]

console.log(arr.flat()) // [1, 2, 3, 4]
```

```js
const arr = [1, 2, [3, 4, [5, 6]]]

console.log(arr.flat()) // [1, 2, 3, 4, [5, 6]]
console.log(arr.flat(2)) // [1, 2, 3, 4, 5, 6]
```

```js
const arr = [1, 2, [3, 4, [5, 6, [7, 8]]]]

console.log(arr.flat()) // [1, 2, 3, 4, [5, 6, [7, 8]]]
console.log(arr.flat(2)) // [1, 2, 3, 4, 5, 6, [7, 8]]
console.log(arr.flat(Infinity)) // [1, 2, 3, 4, 5, 6, 7, 8]
```

### .forEach()

대상 배열의 길이만큼 주어진 콜백을 실행합니다.

```js
const arr = ['A', 'B', 'C']

arr.forEach(item => console.log(item))

for (let i = 0; i < arr.length; i += 1) {
  console.log(arr[i])
}

// 'A'
// 'B'
// 'C'
```

`.forEach()`는 중간에 반복을 멈출 수 없습니다.  
반복을 멈출 수 있어야 한다면, `for` 반복문을 사용해야 합니다.

```js
const arr = ['A', 'B', 'C']

for (let i = 0; i < arr.length; i += 1) {
  if (i > 1) {
    break
  }
  console.log(arr[i])
}
// 'A'
// 'B'
```

### .includes()

대상 배열이 특정 요소를 포함하고 있는지 확인합니다.  
주로 원시형 데이터를 찾는 용도로 쓰임.

```js
const arr = [1, 2, 3]

console.log(arr.includes(2)) // true
```

```js
const fruits = ['Apple', 'Banana', 'Cherry']

console.log(fruits.includes('Apple')) // true
console.log(fruits.includes('cherry')) // false
```

```js
const users = [
  { name: 'Neo', age: 85 },
  { name: 'Amy', age: 22 },
  { name: 'Lewis', age: 11 }
]
// 생성 위치가 다름
console.log(users.includes({ name: 'Neo', age: 85 })) // false

const neo = users[0]
console.log(users.includes(neo)) // true
```

### .join()

대상 배열의 모든 요소를 구분자로 연결한 문자를 반환합니다.

```js
const fruits = ['Apple', 'Banana', 'Cherry']

console.log(fruits.join()) // 'Apple,Banana,Cherry'
console.log(fruits.join(', ')) // 'Apple, Banana, Cherry'
console.log(fruits.join('/')) // 'Apple/Banana/Cherry'
```

### .map()

대상 배열의 길이만큼 주어진 콜백을 실행하고,  
콜백의 반환 값을 모아 새로운 배열을 반환합니다.  
map: 반복하다.

```js
const numbers = [1, 2, 3, 4]
const newNumbers = numbers.map(item => item * 2)

console.log(newNumbers) // [2, 4, 6, 8]
```

```js
const users = [
  { name: 'Neo', age: 85 },
  { name: 'Amy', age: 22 },
  { name: 'Lewis', age: 11 }
]
const newUsers = users.map(user => ({
  ...user,
  isValid: true,
  email: null
}))

console.log(newUsers)
```

### .pop()

대상 배열에서 마지막 요소를 제거하고 그 요소를 반환합니다.  
대상 배열 원본이 변경됩니다. (주의!)

```js
const fruits = ['Apple', 'Banana', 'Cherry']

console.log(fruits.pop()) // 'Cherry'
console.log(fruits) // ['Apple', 'Banana']
```

### .push() ※사용 빈도 多

대상 배열의 마지막에 하나 이상의 요소를 추가하고, 배열의 새로운 길이를 반환합니다.  
대상 배열 원본이 변경됩니다. (주의!)

```js
const fruits = ['Apple', 'Banana', 'Cherry']

const newLength = fruits.push('Orange')
console.log(newLength) // 4
console.log(fruits) // ['Apple', 'Banana', 'Cherry', 'Orange']

fruits.push('Mango', 'Strawberry')
console.log(fruits)
// ['Apple', 'Banana', 'Cherry', 'Orange', 'Mango', 'Strawberry']
```

### .reduce()

대상 배열의 길이만큼 주어진 콜백을 실행하고, 마지막에 호출되는 콜백의 반환 값을 반환합니다.  
각 콜백의 반환 값은 다음 콜백으로 전달됩니다.

```js
const numbers = [1, 2, 3]

// const result = numbers.reduce((acc, cur) => acc + cur, 0)
const result = numbers.reduce

// accmulator : 누적
((accumulator, currentValue) => {
  return accumulator + currentValue
}, 0)
// 0 + 1
// 1 + 2
// 3 + 3

console.log(result) // 6
```

```js
const users = [
  { name: 'Neo', age: 85 },
  { name: 'Amy', age: 22 },
  { name: 'Lewis', age: 11 }
]

// 총 나이 계산
const totalAge = users.reduce((acc, cur) => acc + cur.age, 0)
console.log(totalAge) // 118
console.log(`평균 나이: ${(totalAge / users.length).toFixed(1)}세`) // '평균 나이: 39.3세'

// 모든 이름 추출
const names = users
  .reduce((acc, cur) => {
    acc.push(cur.name)
    return acc
  }, [])
  .join(', ')
console.log(names) // 'Neo, Amy, Lewis'
```

### .reverse()

대상 배열의 순서를 반전합니다.  
대상 배열 원본이 변경됩니다. (주의!)

```js
const arr = ['A', 'B', 'C']
const reversed = arr.reverse()

console.log(reversed) // ['C', 'B', 'A']
console.log(arr) // ['C', 'B', 'A']
```

```js
const str = 'Hello~'
const reversedStr = str.split('').reverse().join('')

console.log(reversedStr) // '~olleH'
console.log(str) // 'Hello~'
```

### .shift()

대상 배열에서 첫 번째 요소를 제거하고, 제거된 요소를 반환합니다.  
대상 배열 원본이 변경됩니다.

```js
const arr = ['A', 'B', 'C']

console.log(arr.shift()) // 'A'
console.log(arr) // ['B', 'C']
```

### .slice()

대상 배열의 일부를 추출해 새로운 배열을 반환합니다.  
두 번째 인수 직전까지 추출하고, 두 번째 인수를 생략하면 대상 배열의 끝까지 추출합니다.

```js
const arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G']

console.log(arr.slice(0, 3)) // ['A', 'B', 'C']
console.log(arr.slice(4, -1)) // ['E', 'F']
console.log(arr.slice(4)) // ['E', 'F', 'G'] 
console.log(arr) // ['A', 'B', 'C', 'D', 'E', 'F', 'G']
```

### .some()

대상 배열의 어떤 요소라도 콜백 테스트를 통과하는지 확인합니다.

```js
const arr = [1, 2, 3, 4]
const isValid = arr.some(item => item > 3)

console.log(isValid) // true
```

### .sort()

대상 배열을 콜백의 반환 값에 따라 정렬합니다.  
콜백을 제공하지 않으면, 요소를 문자열로 변환하고 유니코드 코드 포인트 순서로 정렬합니다.  
대상 배열 원본이 변경됩니다.

**콜백의 반환 값:**
- 음수: `a`를 낮은 순서로 정렬
- `0`: 순서 변경 없음
- 양수: `b`를 낮은 순서로 정렬

```js
const numbers = [4, 17, 2, 103, 3, 1, 0]

numbers.sort()
console.log(numbers) // [0, 1, 103, 17, 2, 3, 4]

numbers.sort((a, b) => a - b)
console.log(numbers) // [0, 1, 2, 3, 4, 17, 103]

numbers.sort((a, b) => b - a)
console.log(numbers) // [103, 17, 4, 3, 2, 1, 0]
```

```js
const users = [
  { name: 'Neo', age: 85 },
  { name: 'Amy', age: 22 },
  { name: 'Lewis', age: 11 }
]

users.sort((a, b) => a.age - b.age)
console.log(users) // [ Lewis객체, Amy객체, Neo객체 ]

// users.sort((a, b) => b.age - a.age)
// console.log(users) // [ Neo객체, Amy객체, Lewis객체 ]
```

### .splice()

대상 배열에 요소를 추가하거나 삭제하거나 교체합니다.  
대상 배열 원본이 변경됩니다.

요소 추가

```js
const arr = ['A', 'B', 'C']
arr.splice(2, 0, 'X')

console.log(arr) // ['A', 'B', 'X', 'C']
```

요소 삭제

```js
const arr = ['A', 'B', 'C']
arr.splice(1, 1)

console.log(arr) // ['A', 'C']
```

요소 교체

```js
const arr = ['A', 'B', 'C']
arr.splice(1, 1, 'X')

console.log(arr) // ['A', 'X', 'C']
```

요소 추가 및 삭제

```js
const arr = ['A', 'B', 'C']
arr.splice(0, 0, 'X', 'Y', 'Z')

console.log(arr) // ['X', 'Y', 'Z', 'A', 'B', 'C']
```

### .unshift()

새로운 요소를 대상 배열의 맨 앞에 추가하고 새로운 배열의 길이를 반환합니다.
대상 배열 원본이 변경됩니다.

```js
const arr = ['A', 'B', 'C']

console.log(arr.unshift('X')) // 4
console.log(arr) // ['X', 'A', 'B', 'C']
```

### Array.from()

유사 배열(Array-like)을 실제 배열로 반환합니다.

```js
const arraylike = {
  0: 'A',
  1: 'B',
  2: 'C',
  length: 3
}

console.log(arraylike.constructor === Array) // false
console.log(arraylike.constructor === Object) // true

// arraylike.forEach(item => console.log(item)) // Error!
Array.from(arraylike).forEach(item => console.log(item))
// 'A'
// 'B'
// 'C'
```

### Array.isArray()

배열 데이터인지 확인합니다.

```js
const array = ['A', 'B', 'C']
const arraylike = {
  0: 'A',
  1: 'B',
  2: 'C',
  length: 3
}

console.log(Array.isArray(array)) // true
console.log(Array.isArray(arraylike)) // false
```


---
## Object

### Object.assign()

하나 이상의 출처(Source) 객체로부터 대상(Target) 객체로 속성을 복사하고 대상 객체를 반환합니다.

```js
const target = { a: 1, b: 2 }
const source1 = { b: 3, c: 4 }
const source2 = { c: 5, d: 6 }
const result = Object.assign(target, source1, source2)

console.log(target) // { a: 1, b: 3, c: 5, d: 6 }
console.log(result) // { a: 1, b: 3, c: 5, d: 6 }
```

새로운 객체를 반환하려면, 빈 객체를 대상으로 추가할 수 있습니다.

```js
const target = { a: 1, b: 2 }
const source1 = { b: 3, c: 4 }
const source2 = { c: 5, d: 6 }
const result = Object.assign({}, target, source1, source2)

console.log(target) // { a: 1, b: 2 }
console.log(result) // { a: 1, b: 3, c: 5, d: 6 }
```

전개 연산자를 사용할 수도 있습니다.

```js
const target = { a: 1, b: 2 }
const source1 = { b: 3, c: 4 }
const source2 = { c: 5, d: 6 }
const result = {
  ...target,
  ...source1,
  ...source2
}

console.log(target) // { a: 1, b: 2 }
console.log(result) // { a: 1, b: 3, c: 5, d: 6 }
```

### Object.entries()

주어진 객체의 각 속성과 값으로 하나의 배열 만들어 요소로 추가한 2차원 배열을 반환합니다.

```js
const user = {
  name: 'Heropy',
  age: 85,
  isValid: true,
  email: 'thesecon@gmail.com'
}

console.log(Object.entries(user))
// [
//   ['name', 'Heropy'], 
//   ['age', 85], 
//   ['isValid', true], 
//   ['email', 'thesecon@gmail.com']
// ]

for (const [key, value] of Object.entries(user)) {
  console.log(key, value)
}
// name Heropy
// age 85
// isValid true
// email thesecon@gmail.com
```

### Object.keys()

주어진 객체의 속성 이름을 나열한 배열을 반환합니다.

```js
const user = {
  name: 'Heropy',
  age: 85,
  isValid: true,
  email: 'thesecon@gmail.com'
}

console.log(Object.keys(user)) // ['name', 'age', 'isValid', 'email']
```

### Object.values()

주어진 객체의 속성 값을 나열한 배열을 반환합니다.

```js
const user = {
  name: 'Heropy',
  age: 85,
  isValid: true,
  email: 'thesecon@gmail.com'
}

console.log(Object.values(user))
// ['Heropy', 85, true, 'thesecon@gmail.com']
```

### Object.freeze()와 Object.isFrozen()

주어진 객체를 변경할 수 없도록 동결하거나, 동결 여부를 확인합니다.

```js
const user = {
  name: 'Heropy',
  age: 85
}

user.age = 44
console.log(user) // { name: 'Heropy', age: 44 }
console.log(Object.isFrozen(user)) // false

// 동결!
Object.freeze(user)

user.age = 22
user.email = 'thesecon@gmail.com'
console.log(user) // { name: 'Heropy', age: 44 }
console.log(Object.isFrozen(user)) // true
```

### Object.seal()과 Object.isSealed()

주어진 객체를 변경할 수 없도록 밀봉하거나, 밀봉 여부를 확인합니다.  
동결과 다른 점은 밀봉 후에도 속성의 값을 변경할 수 있습니다.

```js
const user = {
  name: 'Heropy',
  age: 85
}

user.age = 44
console.log(user) // { name: 'Heropy', age: 44 }
console.log(Object.isSealed(user)) // false

// 밀봉!
Object.seal(user)

user.age = 22 // 변경 가능!
user.email = 'thesecon@gmail.com'
console.log(user) // { name: 'Heropy', age: 22 } // 변경됨!
console.log(Object.isSealed(user)) // true
```

### Object.defineProperty()

주어진 객체에 속성을 추가하거나, 특성을 변경합니다.

`속성: 기본값` | 설명
---|---
`enumerable: false` | 속성의 열거 가능 여부
`configurable: false` | 속성의 수정(이미 존재할 때), 삭제 가능 여부
`writable: false` | 속성의 값 변경 가능 여부
`value: undefined` | 속성의 값
`get: undefined` | 속성의 Getter
`set: undefined` | 속성의 Setter

```js
const user = {}
Object.defineProperty(user, 'name', {
  value: 'Heropy'
})
console.log(user.name) // 'Heropy'

// 열거 불가!
for (const key in user) {
  console.log('key:', key) // 출력 없음!
}

// 수정 불가!
user.name = 'Neo'
console.log(user.name) // 'Heropy'

// 삭제 불가!
delete user.name
console.log(user.name) // 'Heropy'
```

```js
const user = {}
Object.defineProperty(user, 'name', {
  value: 'Heropy',
  configurable: true,
  writable: true,
  enumerable: true
})
console.log(user.name) // 'Heropy'

// 열거 불가!
for (const key in user) {
  console.log(key) // 'name'
}

// 수정 불가!
user.name = 'Neo'
console.log(user.name) // 'Neo'

// 삭제 불가!
delete user.name
console.log(user.name) // undefined
```

```js
const user = {
  _name: 'Heropy'
}
Object.defineProperty(user, 'name', {
  get() {
    return this._name
  },
  set(value) {
    this._name = value
    console.log(`이름이 ${value}로 바뀌었습니다!`)
  }
})

// Get!
console.log(user.name) // 'Heropy'

// Set!
user.name = 'Neo' // '이름이 Neo로 바뀌었습니다!'

for (let key in user) {
  console.log(key) // '_name'
}
```

### Object.defineProperties()

주어진 객체에 여러 속성을 추가하거나, 특성을 변경합니다.

```js
const user = {}
Object.defineProperties(user, {
  name: {
    enumerable: true,
    value: 'Heropy'
  },
  age: {
    enumerable: true,
    value: 85
  },
  email: {
    enumerable: true,
    configurable: true,
    writable: true,
    value: []
  },
  address: {
    value: '경기 수원시'
  }
})

console.log(user)
for (const key in user) {
  console.log(key)
}
// 'name'
// 'age'
// 'email'
```


---
## JSON

JSON(JavaScript Object Notation)는 데이터 전달을 위한 표준 데이터 포맷입니다.

- 문자, 숫자, 불린, Null, 객체, 배열만 사용
- 문자는 큰 따옴표만 사용
- 후행 쉼표 사용 불가
- `.json` 확장자 사용

### .stringify()

JavaScript 데이터를 JSON 문자로 변환합니다.

```js
console.log(JSON.stringify('Hello world!')) // '"Hello world!"'
console.log(JSON.stringify(123)) // '123'
console.log(JSON.stringify(false)) // 'false'
console.log(JSON.stringify(null)) // 'null'
console.log(JSON.stringify({ name: 'Heropy', age: 85 })) // '{"name":"Heropy","age":85}'
// console.log(JSON.stringify({ name: 'Heropy', age: 85 }, null, 2))
console.log(JSON.stringify([1, 2, 3])) // '[1,2,3]'
```

### .parse()

JSON 문자를 분석해 JavaScript 데이터로 변환합니다.

```js
console.log(JSON.parse('"Hello world!"')) // "Hello world!"
// console.log(JSON.parse('Hello world!'))
// console.log(JSON.parse("Hello world!"))
console.log(JSON.parse('123')) // 123
console.log(JSON.parse('false')) // false
console.log(JSON.parse('null')) // null
console.log(JSON.parse('{"name":"Heropy","age":85}')) // { name: 'Heropy', age: 85 }
console.log(JSON.parse('[1,2,3]')) // [1, 2, 3]
```