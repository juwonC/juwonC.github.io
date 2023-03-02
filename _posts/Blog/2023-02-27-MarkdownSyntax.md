---
title: "마크다운 문법"
excerpt: "마크다운 문법입니다."

categories:
  - Blog
tags:
  - [Blog, Github Pages, Markdown]

toc: true
toc_sticky: true

date: 2023-02-27
---

## 헤더(Headings)

<br>

```markdown
# 제목1
## 제목2
### 제목3
#### 제목4
##### 제목5
###### 제목6
```
결과
<br>

# 제목1
## 제목2
### 제목3
#### 제목4
##### 제목5
###### 제목6

<br><br><br>

## 줄바꿈(Line Breaks)

<br>

```markdown
안녕하세요.<br> Hello World.

안녕하세요.  <- 두 칸 이상 공백
Hello World.
```
결과
<br>

안녕하세요.<br> Hello World.

<br>

안녕하세요.  
Hello World.

<br><br><br>

## 목록(Lists)

<br>

* 순서있는 목록(Ordered List)

<br>

``` markdown
1. a
2. b
3. c
```
결과
<br>

1. a
2. b
3. c

<br><br>


* 순서없는 목록(Unordered List)

<br>

``` markdown
* a
* b
  - c
    + d
```
결과
<br>

* a
* b
  - c
    + d

<br><br><br>

## 코드 블럭(Code Block)

<br>


    ``` cpp
      #include <iostream>

      int main()
      {
        std::cout << "Hello World!" << std::endl;
      }
    ```


결과
<br>

 ``` cpp
  #include <iostream>

  int main()
  {
    std::cout << "Hello World!" << std::endl;
  }
```