---
title: "기타"
layout: archive
permalink: /other
---

{% assign posts = site.categories.other %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}