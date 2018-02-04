---
layout: default
date: 2018-02-03 13:37:00
---

# Guides #

I enjoy tinkering with things in general (and computers in particular), and
every so often I am able to create something that is kind of useful.
Below, you can find some write-ups I've produced.
Hopefully they'll bring you joy!

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>

