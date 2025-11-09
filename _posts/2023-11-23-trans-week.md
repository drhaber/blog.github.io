---
layout: post
title: Trans week 23
date: 2023-11-23 14:48 -0500
---

{% assign images = site.static_files | where: "path", "/assets/img/Highlights/Trans week 23/" %}

{% for image in images %}
  ![{{ image.name }}]({{ image.path | relative_url}})
{% endfor %}

{{ images | size }}

{% for file in site.static_files %}
  {{ file.path }}
{% endfor %}

![test]({{'/assets/img/Highlights/Trans week 23/SaveClip.App_401558030_1268105723886163_7337218994715518287_n.jpg'| relative_url}})
