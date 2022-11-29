---
title: "JAVA"
layout: archive
permalink: /java
sidebar:
  nav: "categories"
---

{% assign posts = site.categories.java %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}