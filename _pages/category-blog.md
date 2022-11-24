---
title: "JAVA"
layout: archive
permalink: /java

title: "AWS"
layout: archive
permalink: /aws

title: "Baekjoon"
layout: archive
permalink: /baekjoon

title: "회고"
layout: archive
permalink: /review

title: "etc"
layout: archive
permalink: /etc
---


{% assign posts = site.categories.java %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
{% assign posts = site.categories.aws %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
{% assign posts = site.categories.baekjoon %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
{% assign posts = site.categories.review %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
{% assign posts = site.categories.etc %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}