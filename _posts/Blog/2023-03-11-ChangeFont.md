---
title: "[Blog]웹 폰트 적용하기"
excerpt: "웹 폰트 적용하기"

categories:
  - Blog
tags:
  - [Blog, Github Pages, Font]

toc: true
toc_sticky: true

date: 2023-03-11
---

## 📝웹 폰트 적용하기
### 📌웹 폰트 고르기
  눈누라는 사이트를 이용하여 폰트를 골랐습니다.
  <br>
  [https://noonnu.cc/](https://noonnu.cc/)
  
  <br>

  저는 이롭게 바탕체를 적용해봤습니다.
  <br>
  ![이롭게 바탕체](/assets/images/FontURL.png)
  <br>
  [https://noonnu.cc/font_page/4](https://noonnu.cc/font_page/4)

<br><br>

### 📌폰트 임포트
마음에 드는 폰트를 찾아 @impot로 시작하는 코드를 복사해서 assets/css/main.scss 파일 맨 아래 부분에 붙여넣습니다.

```css
@import url('//cdn.jsdelivr.net/font-iropke-batang/1.2/font-iropke-batang.css');
```

<br>

main.scss 파일 작성 결과
<br>

```css
---
# Only the main Sass file needs front matter (the dashes are enough)
search: false
---

@charset "utf-8";

@import "minimal-mistakes/skins/{{ site.minimal_mistakes_skin | default: 'default' }}"; // skin
@import "minimal-mistakes"; // main partials

@import url('//cdn.jsdelivr.net/font-iropke-batang/1.2/font-iropke-batang.css');
```

<br><br><br>

### 📌폰트 적용하기
_sass/minimal-mistakes/_variables.scss 파일을 열어서 $serif, $sans-serif 부분에 폰트 이름을 써줍니다. 왼쪽에 적힌 폰트들일 수록 우선순위가 높습니다. $serif, $sans-serif 말고 변수를 따로 만들어서 폰트를 적용할 수도 있습니다.
<br>

```css
$serif: "Iropke Batang", Georgia, Times, serif !default;
$sans-serif: "Iropke Batang", -apple-system, BlinkMacSystemFont, "Roboto", "Segoe UI",
  "Helvetica Neue", "Lucida Grande", Arial, sans-serif !default;
$monospace: Monaco, Consolas, "Lucida Console", monospace !default;
```

<br>
_sidebar.scss로 예를 들면 font-family에 따라 폰트가 결정되는 것을 알 수 있습니다.
<br>

```css
  p,
  li {
    font-family: $sans-serif;
    font-size: $type-size-6;
    line-height: 1.5;
  }
```
<br>

출처
<br>
[https://ansohxxn.github.io/blog/font/#site-nav](https://ansohxxn.github.io/blog/font/#site-nav)
<br>
[https://chaelin0722.github.io/blog/web_font/](https://chaelin0722.github.io/blog/web_font/)

<br><br>