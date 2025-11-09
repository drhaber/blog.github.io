---
layout: post
title: Trans week 23
date: 2023-11-23 14:48 -0500
---

{% assign base_url = 'https://drhaber.github.io' %}
{% assign base_path = '/assets/img/Highlights/Trans week 23/' %}

{% for file in site.static_files %}
  {% if file.path contains base_path %}
    ![{{ file.name }}]({{ base_url | append: file.path | relative_url }})
  {% endif %}
{% endfor %}
