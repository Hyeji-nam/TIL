# 자바스크립트 데이터

## 원시형

### 1) 문자: 문자(String)은 따옴표를 사용합니다.
<br/>

```javascript
    const str1 = "Hello"
    const str2 = 'World'
    // 템플릿 리터럴(보간 가능)
    const str3 = `Good ${str2}`
    console.log(str3) // Good World
```

### 2) 숫자: 정수 및 부동소수점 숫자(floating point number)를 나타냅니다.
<br/>

```javascript
    const n1 = 123
    const n2 = 12.345
```
#### 숫자가 아닌 숫자
`NaN`(Not-A-Number)는 숫자가 아닌 숫자를 나타냅니다.

```javascript
    const num = 123
    console.log(num + undefined) // NaN
```
#### 부동 소수점 오류 및 해결

컴퓨터로 숫자를 표현하는 한계로 10진수로 표현되는 소수를 2진수로 표현하려면 간혹 무한소수가 발생하고, 이를 유한하게 표현할 때 세부 값의 초과 및 손실로 계산 오류가 발생합니다.

- `숫자.toFixed(자릿수)`: 숫자를 고정 소수점 표기(자릿수)로 반환(문자)합니다.
- `parseFloat(값)`: 주어진 값을 파싱해 부동소수점 실수로 반환(숫자)합니다.

```javascript
    const a = 0.1
    const b = 0.2

    a + b // 0.30000000000000004
    parseFloat((a + b).toFixed(1)) // 0.3
```

### 3) boolean: `true`와 `false` 두 가지 값인 논리 데이터입니다. (참: truthy, 거짓: falsy)
<br/>

```javascript
    let a = true
    let b = false
```

### 4) Null: 존재하지 않는(Nothing), 비어 있는(empty), 알 수 없는(unknown) 값을 **명시적**으로 나타냅니다.
<br/>

```javascript
    let age = null
```

### 5) Undefined: '값이 할당되지 않은 상태'를 나타낼 때 사용합니다.
<br/>

변수는 선언했지만, 값을 할당하지 않았다면 변수에 `undefined`가 자동으로 할당됩니다.
<br/>

```javascript
    let abc

    console.log(abc) //undefined
```
### 6) 심볼: 유일한 식별자를 만들고 싶을 때 사용합니다. <br/>주로 보안이 요구되는 상황에서 사용합니다.
<br/>

```javascript
    // Symbol('설명')
    const s = Symbol('Hello world!')
    const user = {
        name: 'hyeji',
        [s]: 123
    }
    console.log(user['name']) // hyeji
    console.log(user[s]) // 123
```

### 7) BigInt: 길이 제한이 없는 정수(integer)입니다. <br/> 큰 정수를 다룰 때 사용합니다.

```js
    console.log(1234567890123456789012345678901234567890)
    // 1.2345678901234568e+39

    console.log(1234567890123456789012345678901234567890n)
    console.log(BigInt
    ('1234567890123456789012345678901234567890'))
    // 1234567890123456789012345678901234567890n
 ```

# 참조형

### 1) 배열(array)
<br/>

 ```javascript
    // 리터럴: 기호를 사용해서 데이터를 만든다.
    const fruits = ['Apple', 'Banana', 'Cherry']

    // 인덱싱: 인덱스 번호로 조회한다.
    console.log(fruits[0]) //Apple

    // 마지막 아이템 인덱싱
    console.log(fruits[fruits.length - 1])
    or
    console.log(fruits.at(-1))

    // 배열의 길이 = 아이템의 갯수
    console.log(fruits.length) // 3
```

### 2) 객체: key:value(속성:값) 형태로 더 복잡한 데이터 구조를 나타낼 때 사용합니다.
<br/>
    
```javascript
    const user = {
        a: 1,
        b: 2
    }
    // 점 표기법
    console.log(user.a) // 1

    // 대괄호 표기법(꼭 문자로 인덱싱!)
    console.log(user['a']) // 1
```

속성의 이름은 **고유**하기 때문에 **마지막에 작성된** 속성으로 값이 할당됩니다.
<br/>

```javascript
    const user = {
        a: 1,
        a: 3,
        b: 2
    }
 
    console.log(user.a) // 3
```
    
속성 삭제
<br/>

```javascript
    const user = {
        a: 1,
        b: 2,
        c: 3
    }

    delete user.b

    console.log(user) // {a: 1, c: 3}
```

### 3) 함수: 자바스크립트에서 함수(function)은 1급 객체(First-class object)로, 하나의 값으로 변수나 인수 혹은 반환이 가능합니다.
<br/>

```javascript
    function a () {
        return 123
    }

    console.log(typeof a) // function 
    console.log(typeof a ()) // number (123)

    console.log(a) // f a() {return 123} (데이터)
    console.log(a ()) // 123 (함수 호출(사용))
```
```javascript
    // 콜백(call back): 또 다른 함수의 인수로 들어가는 함수
    const a = function () {
        console.log('Aa!')
    }
    const b = function (c) {
        console.log(c)
        c()
    }
    b(a) // Aa!    
```

# 형(type)변환

함수와 연산자에 전달되는 값은 대부분 적절한 자료형으로 자동 변환됩니다. <br/>
이런 과정을 형변환(Type conversion)이라고 합니다.

동등 연산자(==)는 두 피연산자의 값이 서로 같으면 참(true)을 반환합니다. 만약에 타입이 다르면 비교를 위해 **강제로 형변환**이 일어납니다. 따라서 동등 연산자는 쓰지 않는 것이 좋습니다.<br/>
하지만 일치 연산자(===)는 타입의 변환 없이 두 피연산자의 값이 같고, **타입**도 같아야만 참(true)을 반환합니다. 
> 일치 연산자는 값의 메모리 주소를 비교합니다.

```javascript
    const a = 1
    const b = '1'

    console.log(a == b) // true
    console.log(a === b) // false
```
```javascript
    const c = {a:1}
    const d = {a:1}

    console.log(c === d) // false
    // 참조형은 생긴 게 같아도 값이 다를 수 있다.
```

# Truthy & Falsy

## 참 같은 값(Truthy)

문맥에서 `true`로 평가되는 값입니다.


```javascript
    if (true)
    if ({})
    if ([])
    if (42)
    if ('0')
    if (' ') // 공백 문자
    if ('false')
    if (new Date ())
    if (Infinity)
    if (-Infinity)
    ...
```

## 거짓 같은 값(Falsy)

문맥에서 `false`로 평가되는 값입니다. (8가지)

```javascript
    if (false)
    if (null)
    if (undefined)
    if (0)
    if (-0)
    if (NaN) // Not a Number
    if (0n) // BigInt
    if ('') // 빈 문자
```

# 자료형 확인

```javascript
const data = {
    string: '123',
    number: 123,
    boolean: true,
    null: null,
    undefined: undefined,
    symbol: Symbol('Hello'),
    bigint: 123n,
    array: [],
    object: {},
    function: function () {}
}

// typeof DATA
console.log(typeof data.string) // 'string'
console.log(typeof data.number) // 'number'
console.log(typeof data.boolean) // 'boolean'
console.log(typeof data.null) // 'object'
console.log(typeof data.undefined) // 'undefined'
console.log(typeof data.symbol) // 'symbol'
console.log(typeof data.bigint) // 'bigint'
console.log(typeof data.array) // 'object'
console.log(typeof data.object) // 'object'
console.log(typeof data.function) // 'function'

// DATA.constructor
console.log(data.string.constructor === String)
console.log(data.number.constructor === Number)
console.log(data.boolean.constructor === Boolean)
console.log(data.null.constructor) // TypeError!
console.log(data.undefined.constructor) // TypeError!
console.log(data.symbol.constructor === Symbol)
console.log(data.bigint.constructor === BigInt)
console.log(data.array.constructor === Array)
console.log(data.object.constructor === Object)
console.log(data.function.constructor === Function)

// Object.prototype.toString.call(DATA) 
// '[object TYPE]'
function checkType(d) {
  return Object.prototype.toString.call(d).slice(8, -1)
}
console.log(checkType(data.string)) // 'String'
console.log(checkType(data.number)) // 'Number'
console.log(checkType(data.boolean)) // 'Boolean'
console.log(checkType(data.null)) // 'Null'
console.log(checkType(data.undefined)) // 'Undefined'
console.log(checkType(data.symbol)) // 'Symbol'
console.log(checkType(data.bigint)) // 'BigInt'
console.log(checkType(data.array)) // 'Array'
console.log(checkType(data.object)) // 'Object'
console.log(checkType(data.function)) // 'Function'
```