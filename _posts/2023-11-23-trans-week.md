---
layout: post
title: Trans week 23
date: 2023-11-23 14:48 -0500
---

{% assign images = site.static_files | where: "path", "assets/img/Highlights/Trans week 23" %}

{% for image in images %}
  ![{{ image.name | split: '.' | first }}]({{ image.path | relative_url}})
{% endfor %}
