# favicon 사용법

1. 루트 경로에 ‘favicon.ico’라는 이름의 아이콘 파일을 생성합니다.
2. link 태그에 rel 속성에 ‘icon’을 입력하고, href에 아이콘 이미지 주소를 입력합니다.
<br/>

# 오픈그래프(The Open Graph protocol)

웹페이지가 소셜 미디어(페이스북 등)로 공유될 때 우선적으로 활용되는 정보를 지정합니다.
<br/>
ex) <br/>
[오픈그래프 바로가기](https://images.velog.io/images/cjw960703/post/35697ea5-f484-47bc-860a-47213830b01b/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-03-02%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2010.49.53.png)
<br/>
[트위터카드 바로가기](https://developer.twitter.com/en/docs/twitter-for-websites/cards/guides/getting-started)
<br/>
[오픈 그래프 속성 보기](https://ogp.me/)
<br/>
# SEO(검색 엔진 최적화, Search Engine Optimization)

구글이나 네이버 등에 자신의 웹 사이트/페이지를 노출할 수 있도록 정보를 최적화하는 작업을 말합니다.

# img 태그 아래쪽에 공간이 생기는 이유



img 요소는 inline 요소입니다. 글자를 취급하는 inline 요소는 베이스라인 아래쪽에 특정한 공간이 있습니다.
따라서 이러한 현상을 없애기 위해서는 img 태그의 display 속성을 block으로 바꿔줍니다.
```css
img {display: block;}
```





# URL 해시(Hash)

해시(#)는 몇 가지 쓰임이 있지만 그중 CSS ID 선택자를 이용해 페이지 내 특정 위치로 이동할 수 있습니다. 



# BEM(Block Element Modifier)

### HTML 클래스 속성의 작명법
- 요소__일부분: Underscore(Lodash) 기호로 요소의 일부분을 표시
```html
<div class="item">
    <div class="item__name">COFFEE</div>
</div>
```
- 요소–상태: Hyphen(Dash) 기호로 요소의 상태를 표시
```html
<div class="btn btn--white">바로가기</div>
```
<br/>



# `position: fixed or absolute`가 설정된 요소의  가로 너비 특성

일반적으로 block 요소는 가로 너비가 최대한 늘어나려고 하지만
position이 fixed나 absolute 속성이 적용된 요소는 **가로 너비가 최소한으로 줄어들려고 합니다.** 
이를 해결하기 위해서는 width 값을 100%로 설정해 줍니다.

```css
.box {
    position: absolute;
    width: 100%
}
```
<br/>

# Lodash 라이브러리
다양한 유틸리티 기능을 제공하는 자바스크립트 라이브러리입니다. <br/>
[Lodash cdn 바로가기](https://cdnjs.com/libraries/lodash.js)
```js
// lodash, gsap scroll event
const badgeEl = document.querySelector('header .badges');
const toTopEl = document.querySelector('#to-top');

// _.throttle(함수, 시간)
window.addEventListener('scroll', _.throttle(function () {
  console.log(window.scrollY);
  if (window.scrollY > 500) {
    // badge 숨기기
    // gsap.to(요소(or 선택자), 지속시간, 옵션)
    gsap.to(badgeEl, .6, {
      opacity: 0,
      display: 'none'
    });
     // 버튼 보이기
     gsap.to(toTopEl, .2, {
      x: 0
    })
  } else {
    // badge 보이기
    gsap.to(badgeEl, .6, {
      opacity: 1,
      display: 'block'
    });
    // 버튼 숨기기
    gsap.to(toTopEl, .2, {
      x: 100
    })
  }
}, 300)); // 300 = 0.3s
```

# Gsap 라이브러리
자바스크립트로 제어하는 타임라인 기반의 애니메이션 라이브러리입니다. <br/>
[Gsap cdn 바로가기](https://cdnjs.com/libraries/gsap)

```js
// 요소 하나씩 나타내기
const fadeEls = document.querySelectorAll('.visual .fade-in');

fadeEls.forEach(function (fadeEl, index) {
  // gsap.to(요소, 지속시간, 옵션)
  gsap.to(fadeEl, 1, {
    delay: (index + 1) * .7, // 0.7, 1.4, 2.1, 2.8
    opacity: 1
  })

});
```

# Swiper 라이브러리
하드웨어 가속 전환과 여러 기본 동작을 갖춘 현대적인 슬라이드 라이브러리입니다. <br/>
[swiper 바로가기](https://swiperjs.com/)

```js
// swiper
// new: 생성자(클래스)
// new Swiper (선택자, 옵션)
new Swiper('.notice-line .swiper-container', {
  direction: 'vertical',
  autoplay: true,
  // loop: 반복 재생
  loop: true,
});
```


# Youtube API

```js
// 2. This code loads the IFrame Player API code asynchronously.
var tag = document.createElement('script');

tag.src = "https://www.youtube.com/iframe_api";
var firstScriptTag = document.getElementsByTagName('script')[0];
firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);

// 3. This function creates an <iframe> (and YouTube player)
//    after the API code downloads.

function onYouTubeIframeAPIReady() {
  // <div id="player"></div>
  new YT.Player('player', {
    videoId: 'An6LvWQuj_8', // 최초 재생할 유튜브 영상 ID
    playerVars: {
      autoplay: true, // 자동 재생 유무
      loop: true, // 반복 재생 유무
      playlist: 'An6LvWQuj_8' // 반복 재생할 유튜브 영상 ID 목록
    },
    events: {
      // 영상이 준비가 되면 실행
      onReady: function (event) {
        event.target.mute() // 음소거
      }
    }
  });
}
```


[IFrame Player API 바로가기](https://developers.google.com/youtube/iframe_api_reference)

# html 특수기호

```html
<p class="copyright">
        &copy; Starbucks Coffee Company. All Rights Reserved.
</p>
```
[html 특수기호 바로가기](https://www.w3schools.com/html/html_entities.asp)


# img 요소가 `display: block; + margin: 0 auto;`인 경우, `width` 속성이 없이도 **가운데 정렬**이 가능합니다.

```css
img {
    display: block;
    margin: 0 auto;
}
```


