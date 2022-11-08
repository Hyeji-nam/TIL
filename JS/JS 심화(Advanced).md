# 불변성 & 가변성 

불변성(Immutability)은 생성된 데이터가 메모리에서 변경되지 않고,    
가변성(Mutability)은 생성된 데이터가 메모리에서 변경될 수 있음을 의미합니다.

자바스크립트 원시형(문자, 숫자, 불린, null, undefined, 심볼, BigInt)은 불변성을 가지고 있고,  
참조형(배열, 객체, 함수)은 가변성을 가지고 있습니다.

```html
<div class="container">
  <div class="item">
    <div>M1</div>
    <textarea></textarea>
  </div>
  <div class="item">
    <div>M2</div>
    <textarea></textarea>
  </div>
  <div class="item">
    <div>M3</div>
    <textarea></textarea>
  </div>
  <div class="item">
    <div>M4</div>
    <textarea></textarea>
  </div>
  <div class="item">
    <div>M5</div>
    <textarea></textarea>
  </div>
  <div class="item">
    <div>M6</div>
    <textarea></textarea>
  </div>
</div>
```

```css
.container {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}
```

원시형

```js
let a = 1
let b = a

b = 2

console.log(b) // 2
console.log(a) // 1
```

객체

```js
let a = { x: 1 }
let b = a

b.x = 2

console.log(b.x) // 2
console.log(a.x) // 2
```

배열

```js
let a = [1, 2, 3]
let b = a

b[0] = 4

console.log(b) // [4, 2, 3]
console.log(a) // [4, 2, 3]
```

함수

```js
let a = () => 1
let b = a

b.x = 2

console.log(b.x) // 2
console.log(a.x) // 2 
```


---
# 얕은 복사 & 깊은 복사

참조형은 가변성으로 인해, 데이터를 복사할 때 주의가 필요합니다.

- 얕은 복사(Shallow Copy) - 참조형의 1차원 데이터만 복사
- 깊은 복사(Deep Copy) - 참조형의 모든 차원 데이터를 복사

## 객체 예제

```js
const a = { x: 1 }
const b = a

b.x = 2

console.log(b) // { x: 2 }
console.log(a) // { x: 2 }
```

```js
const a = { x: 1 }
const b = { ...a } // 얕은 복사!
// const b = Object.assign({}, a) // 얕은 복사!

b.x = 2

console.log(b) // { x: 2 }
console.log(a) // { x: 1 }
```

참조형 내 참조형이 포함된 경우 얕은 복사만으로는 완전히 새로운 데이터를 만들 수 없습니다.

```js
const a = { x: { y: 1 } }
const b = { ...a } // 얕은 복사!

b.x.y = 2

console.log(b) // { x: { y: 2 } }
console.log(a) // { x: { y: 2 } }
```

참조형 내 참조형이 수 많은 깊이를 가지더라도 완전히 새로운 데이터를 만들 수 있도록,  
Lodash 패키지의 cloneDeep 함수를 사용할 수 있습니다.

```js
import cloneDeep from 'lodash/cloneDeep'

const a = { x: { y: 1 } }
const b = cloneDeep(a) // 깊은 복사!

b.x.y = 2

console.log(b) // { x: { y: 2 } }
console.log(a) // { x: { y: 1 } }
```

## 배열 예제

```js
const a = [1, 2, 3]
const b = a

b[0] = 4

console.log(b) // [4, 2, 3]
console.log(a) // [4, 2, 3]
```

```js
const a = [1, 2, 3]
const b = [...a] // 얕은 복사!
// const b = a.concat([]) // 얕은 복사!

b[0] = 4

console.log(b) // [4, 2, 3]
console.log(a) // [1, 2, 3]
```

```js
const a = [[1, 2], [3]]
const b = [...a]

b[0][0] = 4

console.log(b) // [[4, 2], [3]]
console.log(a) // [[4, 2], [3]]
```

```js
import cloneDeep from 'lodash/cloneDeep'

const a = [[1, 2], [3]]
const b = cloneDeep(a)

b[0][0] = 4

console.log(b) // [[4, 2], [3]]
console.log(a) // [[1, 2], [3]]
```


---
# 가비지 컬렉션

가비지 컬렉션(GC, Garbage Collection, 쓰레기 수집)은 자바스크립트의 메모리 관리 방법으로,  
자바스크립트 엔진이 자동으로 데이터가 할당된 메모리에서 더 이상 사용되지 않는 데이터를 해제하는 것을 말합니다.  
가비지 컬렉션은 자동으로 동작하기 때문에, 개발자가 직접 강제 실행하거나 관리할 수 없습니다.

```js
let a = { x: 1 }
let b = a

b.x = 2
console.log(b) // { x: 2 }
console.log(a) // { x: 2 }

// 가비지 컬렉션을 통해 숫자 1은 메모리에서 해제!
```

```js
const user = {
  name: 'Heropy',
  age: 85,
  emails: ['thesecon@gmail.com', 'heropy@abc.com']
}

delete user.emails
console.log(user) // { name: 'Heropy', age: 85 }

// 가비지 컬렉션을 통해 이메일 배열은 메모리에서 해제!
```

# 클로저

클로저(Closure)는 함수가 선언될 때의 유효범위(렉시컬 범위)를 기억하고 있다가,  
함수가 외부에서 호출될 때 그 유효범위의 특정 변수를 참조할 수 있는 개념을 말합니다.

```js
function createCount() {
  let a = 0
  return function () {
    return a += 1
  }
}

const count = createCount()

console.log(count())  // 1
console.log(count())  // 2
console.log(count())  // 3
```

## 활용 예제

```html
<h1>Hello world!</h1>
<h2>Hello world!</h2>
```

클로저를 사용하지 않은 예제

```js
const h1El = document.querySelector('h1')
const h2El = document.querySelector('h2')

// 별도의 상태 관리가 필요!
let h1IsRed = false
let h2IsRed = false

h1El.addEventListener('click', event => {
  h1IsRed = !h1IsRed
  h1El.style.color = h1IsRed ? 'red' : 'black'
})
h2El.addEventListener('click', event => {
  h2IsRed = !h2IsRed
  h2El.style.color = h2IsRed ? 'red' : 'black'
})
```

클로저를 사용한 예제

```js
const h1El = document.querySelector('h1')
const h2El = document.querySelector('h2')

// 하나의 함수로 정리!
const createToggleHandler = () => {
  let isRed = false
  return event => {
    isRed = !isRed
    event.target.style.color = isRed ? 'red' : 'black'
  }
}
h1El.addEventListener('click', createToggleHandler())
h2El.addEventListener('click', createToggleHandler())
```

# 메모리 누수

메모리 누수(Memory Leak)란, 더 이상 필요하지 않은 데이터가 해제되지 못하고 메모리를 계속 차지되는 현상입니다.

### 불필요한 전역 변수 사용

```js
window.hello = 'Hello world!'
window.heropy = { name: 'Heropy', age: 85 }
```

### 분리된 노드 참조

```html
<button>Remove!</button>

<div class="parent">
  <div class="child">1</div>
  <div class="child">2</div>
</div>
```

메모리 누수 예제

```js
const btn = document.querySelector('button')
const parent = document.querySelector('.parent')

btn.addEventListener('click', () => {
  console.log(parent) // <div class="parent">...</div>
  parent.remove()
})
```

메모리 누수 해결

```js
const btn = document.querySelector('button')

btn.addEventListener('click', () => {
  const parent = document.querySelector('.parent')
  console.log(parent) // <div class="parent">...</div>
  parent && parent.remove()
})
```

### 해제하지 않은 타이머

메모리 누수 예제

```js
let a = 0
setInterval(() => {
  a += 1
}, 100)

setTimeout(() => {
  console.log(a) // 10
}, 1000)
```

메모리 누수 해결

```js
let a = 0
const intervalId = setInterval(() => {
  a += 1
}, 100)

setTimeout(() => {
  console.log(a) // 10
  clearInterval(intervalId) // 타이머 해제!
}, 1000)
```

### 잘못된 클로저 사용

```js
const getFn = () => {
  let a = 0
  return name => {
    // a += 1
    console.log(a)
    return `Hello ${name}~`
  }
}

const fn = getFn()
console.log(fn('Heropy'))
console.log(fn('Neo'))
console.log(fn('Lewis'))
```


---
# 콜 스택, 테스크 큐, 이벤트 루프

- Heap: 데이터가 할당되는 메모리, 수동 할당/해제는 불가, 가비지 콜렉터(GC)가 관리
- Queue: 대기 행렬, 줄을 서서 기다리다
- FIFO(First In First Out): 선입선출, 먼저 들어온 데이터가 먼저 나감
- LIFO(Last In First Out): 후입선출, 마지막에 들어온 데이터가 먼저 나감

```js
setTimeout(() => {
  console.log(1)
}, 0)
for (let i = 0; i < 1000; i += 1) {
  console.log(2)
}

// (1000) 2
// 1
```

```js
function a() {
  console.log('A')
  function b() {
    setTimeout(() => {
      console.log('B1')
      console.log('B2')
    }, 0)
  }
  b()
}
function c() {
  console.log('C')
}

function first() {
  a()
  c()
}
function second() {
  c()
}

first()
second()
```

### 최대 호출 스택 크기 초과

환경에 따라 다르지만, 약 1MB 이상 콜 스택이 쌓이면 다음과 같이 에러가 발생합니다.

> Maximum call stack size exceeded

```js
// 재귀 호출 종료 조건이 없음!
function a() {
  console.log('A')
  a()
}
```

## 테스크(콜백) 큐

### 종류
 
- 마아크로테스크(Microtask Queue) - `Promise`, `queueMicrotask()` 등
- 랜더(Render Queue) - `requestAnimationFrame()`
- 메크로테스크(Macrotask Queue 혹은 Task Queue) - `fetch()`, Ajax, DOM Events 등

### 순서

Micro > Render > Macro

```js
setTimeout(() => console.log('Macro!'))
Promise.resolve().then(() => console.log('Micro!'))
requestAnimationFrame(() => console.log('Animation!'))
console.log('Stack!')
// 'Stack!'
// 'Micro!'
// 'Render!'
// 'Macro!'
```

```js
// Macro
setTimeout(() => {
  alert('setTimeout1')
  // Micro
  queueMicrotask(() => {
    alert('queueMicrotast in setTimeout')
  })
})
// Macro
fetch('').then(() => {
  alert('fetch')
})
// Render
requestAnimationFrame(() => {
  alert('requestAniamtionFrame')
})
// Macro
setTimeout(() => {
  alert('setTimeout2')
})
// Micro
Promise.resolve().then(() => {
  alert('Promise')
})
// Micro
queueMicrotask(() => {
  alert('queueMicrotask')
})
```


---
# 리플로우 & 리페인트

브라우저 화면에 무엇인가 출력하기 위해, 크기나 위치 등을 계산하는 과정을 리플로우(Reflow)라고 합니다.  
리플로우 이후 화면에 실제 출력하는 과정을 리페인트(Repaint)라고 합니다.

노드의 크기, 여백, 위치 등 주변 노드에 영향을 주는 레이아웃 속성이 변경되면,  
브라우저는 모든 노드를 리플로우하고 영향을 받은 모든 화면 영역을 다시 리페인트합니다.

노드의 `visibillty`, `outline`, `opacity`, `transform`, `filter`, `box-shadow`, `background-color`, `color` 등,  
주변 노드에 영향을 주지 않는 단순 표시 속성이 변경되면, 브라우저는 리플로우 없이 해당 노드만 리페인트합니다.

### 브라우저 렌더링 과정

1. HTML 파싱
2. DOM 트리 생성(`DOMContentLoaded` 이벤트)
3. CSS 파싱
4. CSSOM 트리 생성
5. DOM-CSSOM 결합
6. 렌더 트리 생성
7. 레이아웃 계산
8. 렌더링(`load` 이벤트)

### requestAnimationFrame()

브라우저의 리페인트 주기에 맞게 콜백을 실행합니다.

```html
<div class="container">
  <div class="item"></div>
</div>
```

```css
.container {
  width: 400px;
  height: 100px;
  border: 10px solid;
  background-color: lightgray;
}
.item {
  width: 100px;
  height: 100px;
  background-color: red;
}
```

```js
const box = document.querySelector('.item')

let x = 0
let intervalId
const interval = 40 // 리페인트 주기를 정확히 알 수 없으므로, 대략 40ms로 설정
const position = 300
const animation = () => {
  if (x >= position) {
    clearInterval(intervalId)
    return
  }
  x += 10
  box.style.transform = `translateX(${x}px)`
}
intervalId = setInterval(animation, interval)
```

```js
let x = 0
let animationId
const position = 300
const animation = () => {
  if (x >= position) {
    return
  }
  x += 10
  box.style.transform = `translateX(${x}px)`
  animationId = requestAnimationFrame(animation)
}
requestAnimationFrame(animation)
```

# Throttle & Debounce

## Throttle

일정 시간 간격으로 함수를 실행합니다.  
(실행 횟수를 조절)

```js
const throttle = (func, delay = 0) => {
  let lastFunc
  let lastRan
  return function(...rest) {
    if (!lastRan) {
      func.apply(this, rest)
      lastRan = Date.now()
    } else {
      clearTimeout(lastFunc)
      lastFunc = setTimeout(() => {
        if ((Date.now() - lastRan) >= delay) {
          func.apply(this, rest)
          lastRan = Date.now()
        }
      }, delay - (Date.now() - lastRan))
    }
  }
}
```

```js
window.addEventListener('scroll', throttle(event => {
  console.log(event)
}, 400))
```

## Debounce

일정 시간 동안 함수가 실행되지 않으면 함수를 실행합니다.  
(마지막에 한 번에 실행)

```js
const debounce = (func, delay = 0) => {
  let inDebounce
  return function(...rest) {
    clearTimeout(inDebounce)
    inDebounce = setTimeout(() => func.apply(this, rest), delay)
  }
}
```

```js
window.addEventListener('scroll', debounce(event => {
  console.log(event)
}, 400))
```