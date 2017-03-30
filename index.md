---
layout: default
date: 2017-01-23 17:48:58
---

# An Introduction #

My name is Erik Thorsell and I created this site to have something to put on my
resumé as a point of contact between you and me. The idea is that this site may
act as a springboard to relevant information about my persona. If you found
this site through other means *but* my resumé, [here it
is]({{site.url}}/download/erikthorsell_cv.pdf).

So, lets begin.


## Who am I, and what do I do? ##

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
girlfriend, fiddling with (breaking...) my computer and reading
[XKCD comics](https://xkcd.com/1787/) (yes, I use dvorak).

# Notes #

I am a notorious note taker and throughout my education people have often asked
me for notes, so I decided to upload all notes I take (that are somewhat good
and consistent) and share with the world. Currently they are shared through my
ownCloud installation and can be found [here](https://wirsenius.se:1339/index.php/s/aHfPK1Gp3xA3YdU).
Note that my installation uses HTTPS but lacks a valid SSL certificate. (I
know, it really shouldn't, but I haven't gotten around to fix that.)
Regardless, enjoy the notes.

# Posts #

I used to work as a junior journalist and I blogged for almost 10 years. If I
feel the urge to write something down (most likely it will be something nerdy
about computers or it might just be photos), you'll find it below.

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>

