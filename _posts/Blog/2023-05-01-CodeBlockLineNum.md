---
title: "[Blog]코드 블럭에서 코드 라인 수 표시"
excerpt: "코드 블럭에서 코드 라인 수 표시"

categories:
  - Blog
tags:
  - [Github Pages, Jekyll, Code Line Numbers]

toc: true
toc_sticky: true

date: 2023-05-01
---

## 📝 코드 블럭에서 코드 라인 수 표시
### 📌전체 코드 블럭에 적용

블로그 전체 글의 코드 블럭에 코드 라인 수를 표시하려면 _config.yml에 아래와 같은 코드를 추가해줍니다.

```yml
markdown: kramdown
highlighter: rouge

kramdown:
  syntax_highlighter_opts:
    block:
      line_numbers: true
```

<br>

저는 아래와 같이 적용했습니다.

```yml
# Conversion
markdown: kramdown
highlighter: rouge
lsi: false
excerpt_separator: "\n\n"
incremental: false


# Markdown Processing
kramdown:
  input: GFM
  syntax_highlighter_opts:
    block:
      line_numbers: true
  hard_wrap: false
  auto_ids: true
  footnote_nr: 1
  entity_output: as_char
  toc_levels: 1..6
  smart_quotes: lsquo,rsquo,ldquo,rdquo
  enable_coderay: false
```

<br><br>

### 📌각각의 코드 블럭에 적용
아래와 같이 코드 블럭을 작성하면 해당 코드 블럭에 라인 수가 표시됩니다.

```cpp
{% raw %}
{% highlight cpp linenos %}
  #include <iostream>

  int main()
  {

  }
{% endhighlight %}
{% endraw %}
```

<br><br>