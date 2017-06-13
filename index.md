---
layout: default
date: 2017-06-13 HH:MM:SS
---

# Resumé, Notes and GitHub-page #

* [My resumé](https://erikthorsell.github.io/download/erikthorsell_cv.pdf)
* [My notes](https://wirsenius.se:1339/index.php/s/aHfPK1Gp3xA3YdU)
* [My GitHub-page](https://github.com/ErikThorsell)

---

# An Introduction #

My name is Erik Thorsell and I created this site to have something to put on my
resumé as a point of contact between you and me. The idea is that this site may
act as a springboard to relevant information about my persona. If you found
this site through other means *but* my resumé, [here it
is]({{site.url}}/download/erikthorsell_cv.pdf).

So, let's begin.


## Who am I, and what do I do? ##

The spring of 2016 I acquired my BSc in Computer Science and Engineering and I
am currently pursuing my MSc in [Computer Science, Algorithm's, Languages and
Logic](https://www.chalmers.se/en/education/programmes/masters-info/Pages/Computer-Science-algorithms-languages-and-logic.aspx)
at Chalmers University of Technology. I have chosen to target my degree at
`Machine Learning`, `Artificial Intelligence` and the ethics surrounding these
fields.

Before I started my master's studies I spent a summer working for NASA at the
Goddard Space Flight Center. (You can find mine, and my comrades, work
[here](https://github.com/ErikThorsell/GSFC_Internship/).) During the first
year of my master I also worked part time at [NEVS](https://www.nevs.com/en/)
as an engineer (I did all sorts of stuff, hence the ambiguous title, but mostly
Matlab and LaTeX). When I don't do anything related to neither school nor work
I am responsible for the music/worship in my church and my free time is spent
climbing with my fiancé, fiddling with (breaking...) my computers and
reading [XKCD comics](https://xkcd.com/1787/) (yes, I use dvorak, the [Svorak
A5-layout](http://aoeu.info/s/dvorak/images/svorak-A5.png)).


# Notes #

I am a notorious note taker and throughout my education people have often asked
me for notes, so I decided to upload all notes I take (that are somewhat good
and consistent) and share with the world. Currently they are shared through my
ownCloud installation and can be found
[here](https://wirsenius.se:1339/index.php/s/aHfPK1Gp3xA3YdU).  Note that my
installation uses HTTPS but lacks a valid SSL certificate. (I know, it really
shouldn't, but I haven't gotten around to fix that.) Regardless, enjoy the
notes.

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

