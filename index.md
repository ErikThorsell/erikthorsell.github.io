---
layout: default
---

## Table of Contents

I realized I was in need of a portfolio, here it is.

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
