---
title: "[Blog]마크다운 문법"
excerpt: "마크다운 문법"

categories:
  - Blog
tags:
  - [Github Pages, Markdown]

toc: true
toc_sticky: true

date: 2023-02-27
---

## 📝헤더(Headings)

```markdown
# 제목1
## 제목2
### 제목3
#### 제목4
##### 제목5
###### 제목6
```

<br>

결과
<br>

# 제목1
## 제목2
### 제목3
#### 제목4
##### 제목5
###### 제목6

<br><br><br>

## 📝줄바꿈(Line Breaks)

```markdown
안녕하세요.<br> Hello World.

안녕하세요.  <- 두 칸 이상 공백
Hello World.
```

<br>

결과
<br>

안녕하세요.<br> Hello World.

<br>

안녕하세요.  
Hello World.

<br><br><br>

## 📝목록(Lists)

### 📌순서있는 목록(Ordered List)

``` markdown
1. a
2. b
3. c
```

<br>

결과
<br>

1. a
2. b
3. c

<br><br>


### 📌순서없는 목록(Unordered List)

``` markdown
* a
* b
  - c
    + d
```

<br>

결과
<br>

* a
* b
  - c
    + d

<br><br><br>

## 📝코드 블럭(Code Block)

```cpp
  #include <iostream>

  int main()
  {
    std::cout << "Hello World!" << std::endl;
  }
```

<br>

결과

 ```cpp
  #include <iostream>

  int main()
  {
    std::cout << "Hello World!" << std::endl;
  }
```

<br><br><br>

## 📝링크 삽입(Links)

```markdown
[https://www.google.com/](https://www.google.com/)
```

<br>

결과
<br>

[https://www.google.com/](https://www.google.com/)

<br><br><br>

## 📝이미지 삽입(Images)

```markdown
![doom](/assets/images/doom.png)
```

<br>

결과
<br>

![doom](/assets/images/doom.png)
<br>
출처: [https://en.wikipedia.org/wiki/Video_game](https://en.wikipedia.org/wiki/Video_game)
<br>

### 📌이미지 크기 조절

```markdown
![doom](/assets/images/doom.png){: width="200" height="200"}
```

<br>

결과
<br>

![doom](/assets/images/doom.png){: width="200" height="200"}

<br><br><br>

## 📝영상 삽입(Video)
### 📌정적 링크 삽입
스크린샷을 누르면 해당 영상 페이지로 가는 방법입니다.

```markdown
[![이미지 설명](스크린샷 이미지)](유튜브 링크)

[![SampleVideo](http://img.youtube.com/vi/유튜브주소ID/0.jpg)](https://youtu.be/유튜브주소ID)
```

유뷰트 주소 ID는 v= 뒷 부분에 해당합니다.

![YouTubeID](/assets/images/Blog/YouTubeID.png){: width="400" height="400"}

<br>

예제

```markdown
[![SampleVideo](http://img.youtube.com/vi/F5tbd_q-qPs/0.jpg)](https://youtu.be/F5tbd_q-qPs)
```

<br>

결과

[![SampleVideo](http://img.youtube.com/vi/F5tbd_q-qPs/0.jpg)](https://youtu.be/F5tbd_q-qPs)

<br>

### 📌영상 바로 삽입
minimal mistakes 테마에서 마크다운으로 작성된 페이지에서 바로 영상이 재생되게 하는 방법입니다. minimal mistakes 테마는 비디오를 페이지에서 바로 재생할 수 있게 하는 Helper를 지원합니다. 다른 지킬 테마에서는 적용이 안 될 수 있습니다.


💡minimal mistakes 테마 Helpers 문서
<br>
[https://mmistakes.github.io/minimal-mistakes/docs/helpers/](https://mmistakes.github.io/minimal-mistakes/docs/helpers/)
{: .notice--info}

```liquid
{% raw %}
{% include video id="유튜브주소ID" provider="youtube" %}
{% endraw %} 
```

<br>

예제

```liquid
{% raw %}
{% include video id="F5tbd_q-qPs" provider="youtube" %}
{% endraw %} 
```

<br>

결과

{% include video id="F5tbd_q-qPs" provider="youtube" %}

<br>

출처
<br>
[https://www.youtube.com/@unrealenginekr](https://www.youtube.com/@unrealenginekr)

<br><br><br>

## 📝표(Table)
```markdown
| 이름 | 번호 |
| --- | --- |
| a | 1 |
| b | 2 |
| c | 3 |
```

<br>

결과
<br>

| 이름 | 번호 |
| --- | --- |
| a | 1 |
| b | 2 |
| c | 3 |

<br>

### 📌정렬(Alignment)
:를 왼쪽에 넣으면 왼쪽 정렬, 양쪽에 넣으면 가운데 정렬, 오른쪽에 넣으면 오른쪽 정렬

```markdown
| 이름 | 번호 |
| :---: | :---: |
| a | 1 |
| b | 2 |
| c | 3 |
```

<br>

결과
<br>

| 이름 | 번호 |
| :---: | :---: |
| a | 1 |
| b | 2 |
| c | 3 |

<br><br><br>

## 📝강조(Emphasis)
### 📌굵은 글씨(Bold)

```markdown
Hello **World!**
Hello <strong>World!</strong>
```

결과
<br>

Hello **World!**
<br>
Hello <strong>World!</strong>

<br>

### 📌이탤릭체(Italic)

```markdown
Hello *World!*
Hello <em>World!</em>
```

결과
<br>

Hello *World!*
<br>
Hello <em>World!</em>

<br>

### 📌밑줄(Italic)

```markdown
Hello <u>World!</u>
```

결과
<br>

Hello <u>World!</u>

<br><br><br>

## 📝아래첨자(Subscript)

```markdown
Hello <sub>World!</sub>
```

결과
<br>

Hello <sub>World!</sub>

<br><br><br>

## 📝위첨자(Superscript)

```markdown
Hello <sup>World!</sup>
```

결과
<br>

Hello <sup>World!</sup>

<br><br>