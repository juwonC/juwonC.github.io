---
title: "[Blog]맨 위로 올라가기 버튼 만들기"
excerpt: "맨 위로 올라가기 버튼 만들기"

categories:
  - Blog
tags:
  - [Github Pages, Back to Top]

toc: true
toc_sticky: true

date: 2023-03-10
---

## 📝맨 위로 올라가기 버튼 만들기
1. _sass/minimal-mistakes/_sidebar.scss에 아래 내용 삽입

```css
.sidebar__top {
  position: fixed;
  bottom: 1.5em;
  right: 2em;
  z-index: 10;
}
```

<br>

2. _layouts/default.html에 아래 내용 삽입

```html
<aside class="sidebar__top">
<a href="#site-nav"> <i class="fas fa-angle-double-up fa-2x"></i></a>
</aside>
```

<br>

div id="footer" class="page__footer" 의 바로 위에 추가합니다.

<br>

출처: [https://chaelin0722.github.io/blog/back_to_top/#site-nav](https://chaelin0722.github.io/blog/back_to_top/#site-nav)