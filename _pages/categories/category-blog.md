---
title: "Blog"
layout: archive
permalink: categories/blog
author_profile: true
sidebar_main: true
---

📝 **minimal mistakes 테마를 기준으로 작성된 글입니다. 다른 지킬 테마에 적용이 안 되는 것들이 있을 수 있습니다. 테마에 대한 자세한 내용은 [https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)를 참고하시길 바랍니다.**
{: .notice--info}

{% assign posts = site.categories.Blog %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}