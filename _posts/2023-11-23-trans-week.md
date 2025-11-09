---
layout: post
title: Trans week 23
date: 2023-11-23 14:48 -0500
---

{% for file in site.static_files %}
  {% if file.path contains '/assets/img/Highlights/Trans week 23/' %}
    ![{{ file.name }}]({{ file.path | relative_url }})
  {% endif %}
{% endfor %}
