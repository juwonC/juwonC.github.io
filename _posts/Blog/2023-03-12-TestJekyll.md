---
title: "[Blog]로컬에서 깃헙 페이지 테스트하기"
excerpt: "로컬에서 깃헙 페이지 테스트하기"

categories:
  - Blog
tags:
  - [Blog, Github Pages, Jekyll]

toc: true
toc_sticky: true

date: 2023-03-12
---

## 📝로컬에서 깃헙 페이지 테스트하기
깃헙 페이지에 글을 쓰면서 자잘하게 수정해야할 것들이 많아졌는데 수정 사항들을 하나 하나 깃헙에 커밋하고 블로그에 적용될 때까지 기다리는 것이 시간도 많이 들고 번거로웠습니다.
<br>

그래서 시간도 아끼고 수정 사항들을 한꺼번에 커밋하기 위해 로컬에서 깃헙 페이지 테스트하는 법을 알아보려고 합니다. 저는 minimal mistakes라는 지킬 테마를 사용하고 있어 이 테마를 기준으로 글을 작성하였습니다.
<br>

### 📌_config.yml에서 url 바꾸기
_config.yml 파일에서 # Site Settings의 url이 자신의 깃헙 페이지 주소로 되어있는 경우 이 주소를  **http://localhost:4000**로 바꿔줍시다.
<br>

저는 아래와 같이 기존 주소는 주석 처리해주었습니다.
```yml
# url   : "https://juwonc.github.io/"
url   : "http://localhost:4000"
```

<br>

### 📌지킬 서버 실행
터미널이나 명령 프롬프트를 열어 깃헙 페이지 폴더로 경로를 설정하고 **bundle exec jekyll serve** 명령어를 입력해 지킬 서버를 실행시켜줍니다.

![jekyll_serve](/assets/images/jekyll_serve.png)

<br>
아래와 같은 화면이 나오면 정상적으로 로컬 서버가 실행된 것입니다. 
<br>

![exec_jekyll_serve](/assets/images/exec_jekyll_serve.png){: width="600" height="600"}

<br>

이제 마크다운 파일이나 블로그 설정을 수정하고 저장한 다음 웹 브라우저에서 **http://localhost:4000**로 접속하면 변경 사항이 적용된 것을 확인할 수 있습니다.
<br>
작업을 마치면 ctrl+c를 눌러 로컬 서버를 종료하거나 터미널을 종료하여 마무리하면 됩니다.

<br>

### 📌맥에서 루비, 지킬 설치
처음 블로그를 만들 때 사용한 윈도우 운영체제 컴퓨터의 로컬에 루비와 지킬을 설치하고 진행했기 때문에 아무 문제 없이 로컬에서 깃헙 페이지를 테스트할 수 있었습니다. 
<br>

하지만 다른 맥북에서 깃헙 페이지를 로컬로 테스트 하기 위해 루비와 지킬을 새로 설치하는 과정에서 시행착오가 좀 있었습니다.
<br>

이 과정은 제가 아직 잘 알지 못하는 부분이 있어 아래 블로그를 참고하시면 좋을 것 같습니다. 간단하게라도 나중에 정리해보도록 하겠습니다.
<br>
[https://frhyme.github.io/blog/install_jekyll_again/](https://frhyme.github.io/blog/install_jekyll_again/)

<br>

추가로 vim ~/.zshrc 명령어를 입력해 vim을 사용하는 과정이 있어 vim 사용법에 대한 블로그 링크도 같이 올리겠습니다.
<br>
[https://www.joinc.co.kr/w/Site/Vim/Documents/UsedVim](https://www.joinc.co.kr/w/Site/Vim/Documents/UsedVim)

<br>

출처
<br>

[https://docs.github.com/ko/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll](https://docs.github.com/ko/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll)

<br><br>