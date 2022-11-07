# 모듈

모듈(Module)은 이해 가능한, 보다 작은 단위로 나눠진 것을 말합니다.  
특히 자바스크립트에서 모듈은 특정 데이터들의 집합(파일)입니다.

## 내보내기(exports)

### 기본 내보내기(Default exports)
  - 이름 X
  - 모듈당 1번만 사용 가능 

### 이름 내보내기(Named exports)
  - 이름 필수!
  - 모듈당 n번 사용 가능

&nbsp; | Default exports | Named exports  
:---:|:---:|:---: 
이름 | 선택 | 필수
출구 | 1개 | n개

```js
export default 데이터
export const 이름1 = 데이터1
export const 이름2 = 데이터2
```

사용 패턴

```js
export default { 
  name: '기본 데이터!', 
  desc: '이름 필요 없음!' 
}
export const str = 'Hello~'
export const num = 123
export const arr = ['A', 'B', 'C']
export function hello() {}
```

`as` 키워드로 내보내는 데이터의 이름 변경이 가능합니다.

```js
const a = 'Named!'
const b = 123
const c = ['A', 'B', 'C']
function d() {}
export {
  a as str,
  b as num,
  c as arr,
  d as hello
}
```

## 가져오기(Imports)
> import 키워드는 파일의 최상단에 작성해야함!
```js
import 기본데이터, { 이름데이터1, 이름데이터2 } from '경로'
```

```js
import defData from './myModule.js'
import defData, { str, num, arr, fn } from './myModule.js'
import { str, num, arr, fn } from './myModule.js'
import { 
  str as myStr, 
  num as myNum, 
  arr as myArr, 
  fn as myFn 
} from './myModule.js'
import * as myName from './myModule.js'
```

> `*`는 와일드카드 문자(wildcard character)로 여러 개를 한 번에 지정한다는 의미의 기호입니다.

### 동적 모듈 가져오기

`import` 함수를 통해 동적으로 모듈을 가져올 수 있습니다.  
`import` 함수는 `promise` 객체를 반환합니다.

```js
// import * as abc from '경로'
// console.log(abc)

import('경로').then(abc => console.log(abc))
```

```js
setTimeout(() => {
  import('./module.js').then(abc => {
    console.log(abc)
  })
}, 1000)
```

### 가져온 후 바로 내보내기

가져온 모듈을 바로 내보낼 수 있습니다.  
`import` 키워드 대신 `export` 키워드를 사용합니다.

```js
export 기본데이터, { 이름데이터1, 이름데이터2 } from '경로'
```