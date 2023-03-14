---
title: "MyInterests"
layout: archive
permalink: categories/interest
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.MyInterests %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}