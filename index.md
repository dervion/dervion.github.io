---
layout: default
title: Home
---

# Welcome to My Cyber Lab Journal

Here are my posts:

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a> — {{ post.date | date: "%B %-d, %Y" }}
    </li>
  {% endfor %}
</ul>
