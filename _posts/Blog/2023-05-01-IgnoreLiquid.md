---
title: "[Blog]Liquid 문법 무시하기"
excerpt: "Liquid 문법 무시하기"

categories:
  - Blog
tags:
  - [Github Pages, Liquid]

toc: true
toc_sticky: true

date: 2023-05-01
---

## 📝 Liquid 문법 무시하기

{% raw %} {% %} {% endraw %}나 {% raw %} {{ }} {% endraw %}와 같은 Liquid 문법을 예시로 글을 작성할 때 오류가 나는 문제를 겪었습니다. 오류 없이 게시물을 포스팅하기 위해 해결방법을 찾아
보니 Liquid 문법의 raw 태그를 사용하면 간단하게 문제를 해결 할 수 있었습니다.

아래와 같이 무시하고 싶은 Liquid 문법을 {{"{% raw"}} %} 와 {{"{% endraw"}} %} 태그로 감싸주면 됩니다.

```markdown
{{"{% raw"}} %} {{"{%"}} %} {{"{% endraw"}} %}


{{"{% raw"}} %} 
{{"{{ "}} }}
{{"{% endraw"}} %}
```

<br>

결과

```markdown
{% raw %} {% %} {% endraw %}


{% raw %}
{{ }}
{% endraw %}
```

<br><br>