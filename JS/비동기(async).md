# 비동기

## 동기(Synchronous)와 비동기(Asynchronous)

- 동기: 순차적으로 코드 실행 O
- 비동기: 순차적으로 코드 실행 X

동기 예시:

```js
console.log(1)
console.log(2)
console.log(3)
// 1
// 2
// 3
```

비동기 예시:

```js
console.log(1)
setTimeout(() => console.log(2), 1000)
console.log(3)
// 1
// 3
// 2
```

```js
const btnEl = document.querySelector('button')
btnEl.addEventListener('click', () => {
  console.log('Clicked!')
})

console.log('Hello World!')
// 'Hello World!'
// 버튼을 누르면, 'Clicked!'
```

### 영화 검색 예시

쿼리스트링(Query string)은 URL 주소에 `키=값` 형태로 데이터를 담아 웹서버로 전달하는 방식입니다.  
`?`로 시작해서 `키=값`을 `&`로 구분합니다.

```plaintext
https://google.com?키1=값1&키2=값2&키3=값3
```

```js
fetch('https://www.omdbapi.com/?apikey=7035c60c&s=frozen')
  .then(res => console.log(res))
```

```js
fetch('https://asia-northeast3-heropy-api.cloudfunctions.net/api/todos', {
  method: 'GET',
  headers: {
    'content-type': 'application/json',
    'apikey': 'FcKdtJs202204',
    'username': 'ParkYoungWoong'
  },
  body: {}
})
  .then(res => res.json())
  .then(res => console.log(res))
```

## 콜백 패턴
> 비동기 처리 필요성 => 콜백 => 지옥 => Promise(ES6) => .then() => async/await

```js
const a = () => console.log(1)
const b = () => console.log(2)

a()
b()
// 1
// 2
```

```js
const a = callback => {
  setTimeout(() => {
    console.log(1)
    callback()
  }, 1000)
}
const b = () => console.log(2)

a(() => {
  b()
})
// 1
// 2
```

```js
// 콜백 지옥(Callback hell)

const a = callback => {
  setTimeout(() => {
    console.log(1)
    callback()
  }, 1000)
}
const b = callback => {
  setTimeout(() => {
    console.log(2)
    callback()
  }, 1000)
}
const c = callback => {
  setTimeout(() => {
    console.log(3)
    callback()
  }, 1000)
}
const d = callback => {
  setTimeout(() => {
    console.log(4)
    callback()
  }, 1000)
}
// ...

a(() => {
  b(() => {
    c(() => {
      d(() => {
        // ...
      })
    })
  })
})
```

```js
// 영화 검색 예시

const getMovies = (movieName, callback) => {
  fetch(`https://www.omdbapi.com/?apikey=7035c60c&s=${movieName}`)
    .then(res => res.json())
    .then(res => {
      console.log(res)
      callback()
    })
}

getMovies('frozen', () => {
  console.log('겨울왕국!')
  getMovies('avengers', () => {
    console.log('어벤져스!')
    getMovies('avatar', () => {
      console.log('아바타!')
    })
  })
})
```

## Promise

```js
const a = () => {
  return new Promise(resolve => {
    setTimeout(() => {
      console.log(1)
      resolve()
    }, 1000)
  })
}
const b = () => console.log(2)

a().then(() => b())
```

```js
const a = () => {
  return new Promise(resolve => {
    setTimeout(() => {
      console.log(1)
      resolve()
    }, 1000)
  })
}
const b = () => {
  return new Promise(resolve => {
    setTimeout(() => {
      console.log(2)
      resolve()
    }, 1000)
  })
}
const c = () => {
  return new Promise(resolve => {
    setTimeout(() => {
      console.log(3)
      resolve()
    }, 1000)
  })
}
const d = () => console.log(4)
```

`.then()`에서 `promise` 인스턴스를 반환하면, 다시 뒤에서 `.then()`을 체이닝으로 사용할 수 있습니다.

```js
// 콜백 지옥해서 해방!
a()
  .then(() => b())
  .then(() => c())
  .then(() => d())

// promise 반환
a()
  .then(b)
  .then(c)
  .then(d)
```

```js
// 영화 검색 예시

const getMovies = movieName => {
  return new Promise(resolve => {
    fetch(`https://www.omdbapi.com/?apikey=7035c60c&s=${movieName}`)
      .then(res => res.json())
      .then(res => {
        console.log(res)
        resolve()
      })
  })
}

getMovies('frozen')
  .then(() => {
    console.log('겨울왕국!')
    return getMovies('avengers')
  })
  .then(() => {
    console.log('어벤져스!')
    return getMovies('avatar')
  })
  .then(() => {
    console.log('아바타!')
  })
```

## async/await

```js
const a = () => {
  return new Promise(resolve => {
    setTimeout(() => {
      console.log(1)
      resolve()
    }, 1000)
  })
}
const b = () => console.log(2)

// a().then(() => b())

const wrap = async () => {
  await a()
  b()
}
wrap()
```

```js
// .then()
a()
  .then(() => b())
  .then(() => c())
  .then(() => d())

// async/await
const wrap = async () => {
  await a()
  await b()
  await c()
  await d()
}
wrap()
```

```js
// 영화 검색 예시

const getMovies = movieName => {
  return new Promise(resolve => {
    fetch(`https://www.omdbapi.com/?apikey=7035c60c&s=${movieName}`)
      .then(res => res.json())
      .then(res => {
        console.log(res)
        resolve()
      })
  })
}

const wrap = async () => {
  await getMovies('frozen')
  console.log('겨울왕국!')
  await getMovies('avengers')
  console.log('어벤져스!')
  await getMovies('avatar')
  console.log('아바타!')
}
wrap()
```

## Resolve, Reject 그리고 에러 핸들링

```js
const delayAdd = (index, cb, errorCb) => {
  setTimeout(() => {
    if (index > 10) {
      errorCb(`${index}는 10보다 클 수 없습니다.`)
      return
    }
    console.log(index)
    cb(index + 1)
  }, 1000)
}

delayAdd(
  4,
  res => console.log(res),
  err => console.error(err)
)
```

```js
const delayAdd = index => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (index > 10) {
        reject(`${index}는 10보다 클 수 없습니다.`)
        return
      }
      console.log(index)
      resolve(index + 1)
    }, 1000)
  })
}

// .then()
delayAdd(11)
  .then(res => console.log(res))
  .catch(err => console.error(err))
  .finally(() => console.log('Done!'))

// async / await
const wrap = async () => {
  try {
    const res = await delayAdd(11)
    console.log(res)
  } catch (err) {
    console.error(err)
  } finally {
    console.log('Done!')
  }
}
wrap()
```

```js
const getMovies = movieName => {
  return new Promise((resolve, reject) => {
    fetch(`https://www.omdbapi.com/?apikey=7035c60c&s=${movieName}`)
      .then(res => res.json())
      .then(json => {
        if (json.Response === 'False') {
          reject(json.Error)
        }
        resolve(json)
      })
      .catch(error => {
        reject(error)
      })
  })
}

let loading = true

// .then()
getMovies('avengers')
  .then(movies => console.log('영화 목록:', movies))
  .catch(error => console.log('에러 발생:', error))
  .finally(() => loading = false)

// async / await
const wrap = async () => {
  try {
    const movies = await getMovies('avengers')
    console.log('영화 목록:', movies)
  } catch (error) {
    console.log('에러 발생:', error)
  } finally {
    loading = false
  }
}
wrap()
```

## 반복문에서 비동기 처리

```js
const getMovies = movieName => {
  return new Promise(resolve => {
    fetch(`https://www.omdbapi.com/?apikey=7035c60c&s=${movieName}`)
      .then(res => res.json())
      .then(res => resolve(res))
  })
}

const titles = ['frozen', 'avengers', 'avatar']

// 잘못된 방법!
titles.forEach(async title => {
  const movies = await getMovies(title)
  console.log(title, movies)
})

// 올바른 방법!
const wrap = async () => {
  for (const title of titles) {
    const movies = await getMovies(title)
    console.log(title, movies)
  }
}
wrap()
```

## 이미지 로딩 예제

```html
<div class="image">
  <div class="loader">Loading...</div>
</div>
```

```css
.image {
  width: 360px;
  height: 200px;
  margin: 10px;
  border: 4px solid;
  border-radius: 10px;
  font-size: 40px;
  background-size: cover;
  display: flex;
  justify-content: center;
  align-items: center;
}
.image.done {
  background-image: url("https://gstatic.com/webp/gallery/1.jpg");
}
.image.done .loader {
  display: none;
}
```

콜백으로 구현

```js
function loadImage(src, callback) {
  const img = document.createElement('img')
  img.src = src
  img.addEventListener('load', () => {
    callback(img)
  })
}

const imgContainer = document.querySelector('.image')

loadImage('https://gstatic.com/webp/gallery/1.jpg', img => {
  imgContainer.classList.add('done')
})
```

프로미스로 구현

```js
function loadImage(src) {
  return new Promise(resolve => {
    const img = document.createElement('img')
    img.src = src
    img.addEventListener('load', () => {
      resolve(img)
    })
  })
}

const imgContainer = document.querySelector('.image')

// .then()
loadImage('https://gstatic.com/webp/gallery/1.jpg')
  .then(img => {
    imgContainer.classList.add('done')
  })

// async/await
;(async function () {
  const img = await loadImage('https://gstatic.com/webp/gallery/1.jpg')
  imgContainer.classList.add('done')
})()
```

## 상태

- pending(대기)
- fulfilled(이행)
- rejected(거부)

## Promise.all()

모든 프로미스가 이행한 후 배열을 반환합니다.

```js
const a = () => {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve(1)
    }, 1000)
  })
}
const b = () => {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve(2)
    }, 2000)
  })
}

const wrap = async () => {
  const [resA, resB] = await Promise.all([a(), b()])
  console.log(resA, resB)
}
wrap()
```

## Promise.race()

더 먼저 완료되는 결과만 이행/거부 합니다. 

```js
const a = () => {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve(1)
    }, 1000)
  })
}
const b = () => {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve(2)
    }, 2000)
  })
}

const wrap = async () => {
  const res = await Promise.race([a(), b()])
  console.log(res) // 1
}
wrap()
```

## fetch()

- 