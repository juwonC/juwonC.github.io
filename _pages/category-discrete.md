---
title: "이산수학"
layout: archive
permalink: /categories/discrete/
author_profile: true
---

{% assign posts = site.categories.Discrete %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}