---
layout: post
title: Trans week 23
date: 2023-11-23 14:48 -0500
---

<div class="image-gallery">
  {% for file in site.static_files %}
      {% if file.path contains 'assets/img/Highlights/Trans week 23' %}
    {% if file.extname == '.jpg' or 
      file.extname == '.jpeg' or 
      file.extname == '.JPG' or 
      file.extname == '.JPEG' %}

      {% assign filenameparts = file.path | split: "/" %}
      {% assign filename = filenameparts | last | replace: file.extname,"" %}

      <a href="{{ file.path }}" title="{{ filename }}">
        <img src="//images.weserv.nl/?url=jekyllcodex.org/{{ file.path }}&w=300&h=300&output=jpg&q=50&t=square" alt="{{ filename }}" />
        <span>{{ filename }}</span>
      </a>
    {% endif %}
  {% endif %}
{% endfor %}
</div>
