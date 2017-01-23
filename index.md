---
layout: default
date: 2017-01-23 14:26:34
---

# An Introduction #

My name is Erik Thorsell and I created this site to act as a nicer online
front matter than simply linking to my GitHub page. The idea is that this site
may act as a springboard to relevant information about me. So, lets start with
some info?

## Who am I? ##

The spring of 2016 I acquired my BSc in Computer Science and Engineering, and I
am currently pursuing my MSc in [Computer Science, Algorithm's, Languages and
Logic](!https://www.chalmers.se/en/education/programmes/masters-info/Pages/Computer-Science-algorithms-languages-and-logic.aspx)
at Chalmers University of Technology. I have chosen to target my degree at
`Machine Learning`, `Artificial Intelligence` and the ethics surrounding these
fields.

When not studying, I work part time at [NEVS](!https://www.nevs.com/en/) as an
engineer (I do all sorts of stuff, hence the ambiguous title) and when I don't
do anything related to neither school nor work I am responsible for the music
in my church, I sport climb with my girlfriend, or find other ways of
pushing my body to its limits.

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

# Contact #

<footer class="container footer group">
  <ul>
    <li><a href="https://github.com/erikthorsell"><img class="img-icon" src="/_images/github.png"></a></li>
    <li><a href="https://linkedin.com/in/thorsellerik"><img class="img-icon" src="/_images/linkedin.png"></a></li>
    <li><a href="mailto:erik@thorsell.cc"><img class="img-icon" src="/_images/email.png"></a></li>
  </ul>
</footer>

