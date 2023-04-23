---
title: "[Blog]포스팅 업데이트 안되는 오류"
excerpt: "포스팅 업데이트 안되는 오류"

categories:
  - Blog
tags:
  - [Github Pages, Jekyll, Error]

toc: true
toc_sticky: true

date: 2023-04-24
---

## 🚧포스팅 업데이트 안되는 오류
게시글을 작성하고 커밋한 후 깃헙 원격 저장소에 푸시했지만 깃헙 페이지에 게시글이 업데이트가 되지 않는 문제가 생겼습니다. 로컬 서버에서 확인했을 때 정상적으로 게시글이 올라가는 것을 확인했고 깃헙 푸시도 문제없이 되어 왜 포스팅 업데이트가 안되는지 원인을 찾기 어려웠습니다.

검색을 해보니 게시글의 날짜와 관련된 문제임을 알게되었습니다. 게시글의 날짜를 미래로 설정하면 jekyll이 포스트를 스킵하는 문제 때문에 이런 오류가 발생한다고 합니다.

자정이 가까운 시간이라 아마 제가 그 다음날로 시간을 설정하여 이런 문제가 발생한 것 같습니다.

<br><br>

### 👷‍♂️해결방법
1. 게시글이 _post 폴더에 있는지 확인합니다.

2. 게시글 파일의 제목이 YEAR-MONTH-DAY-title.md 형식으로 되어 있는지 확인합니다.

3. cmd나 터미널에서 jekyll build --verbose 명령어로 스킵된 jekyll이 없나 확인합니다.

3. 게시글의 날짜가 미래라면 _config_yml에서 future : true로 세팅을 변경합니다.

4. 게시글 옵션(제목, 카테고리, 날짜 적는 공간)에 pusblished: true를 추가해봅니다.

<br><br>

### 👷‍♂️타임존 바꾸기
로컬 환경의 기본 시간대는 운영체제에 의해 맞춰지지만 원격/서버에서의 시간대는 그 서버의 환경에 따라 다르다고 합니다. 따라서 자신의 환경에 맞게 _config.yml에서 타임존을 설정하는 것도 추후에 발생할 오류를 예방하는데 도움이 될 것 같습니다.

한국 시간대로 맞추는 방법은 _config.yml에서 아래와 같이 timezone 설정을 바꿔주면 됩니다.
<br>

```yml
# Outputting
permalink: /:categories/:title/
paginate: 5 # amount of posts to show
paginate_path: /page:num/
timezone: Asia/Seoul
```

<br>


<br>

참고
<br>

[https://stackoverflow.com/questions/30625044/jekyll-post-not-generated](https://stackoverflow.com/questions/30625044/jekyll-post-not-generated)
[https://devyuseon.github.io/github%20blog/githubblog-post-not-shown/](https://devyuseon.github.io/github%20blog/githubblog-post-not-shown/)
[https://jekyllrb.com/docs/configuration/options/](https://jekyllrb.com/docs/configuration/options/)

<br><br>