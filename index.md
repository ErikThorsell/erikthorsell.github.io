---
layout: default
date: 2017-01-23 14:26:34
---

# An Introduction #

My name is Erik Thorsell and I created this site to have something to put on my
resumé as a point of contact between you and me. The idea is that this site may
act as a springboard to relevant information about me. So, lets start with some
info?


## Who am I? ##

The spring of 2016 I acquired my BSc in Computer Science and Engineering and I
am currently pursuing my MSc in [Computer Science, Algorithm's, Languages and
Logic](https://www.chalmers.se/en/education/programmes/masters-info/Pages/Computer-Science-algorithms-languages-and-logic.aspx)
at Chalmers University of Technology. I have chosen to target my degree at
`Machine Learning`, `Artificial Intelligence` and the ethics surrounding these
fields.

When not studying, I work part time at [NEVS](https://www.nevs.com/en/) as an
engineer (I do all sorts of stuff, hence the ambiguous title) and when I don't
do anything related to neither school nor work I am responsible for the
music/worship in my church. My free time is spent sport climbing with my
girlfriend, fiddling (breaking...) my computer and reading
[XKCD](https://xkcd.com).


# Posts #

Below follows a list of all the posts I have yet posted in/on this
portfolio/blog.

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>


