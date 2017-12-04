---
layout: default
date: 2017-06-13 HH:MM:SS
---

# Resources #

* [My resumé]({{site.url}}/download/erikthorsell_cv.pdf)
* [My notes](https://wirsenius.se/index.php/s/0uiVskgkO6e9onr)
* [My GitHub-page](https://github.com/ErikThorsell)

---

# An Introduction #

My name is Erik Thorsell and I created this site to have something to put on my
resumé as a point of contact between you and me.
The idea is that this site may act as a springboard to relevant information
about my persona.
If you found this site through other means *but* my resumé, [here is the
resumé]({{site.url}}/download/erikthorsell_cv.pdf).

So, let's begin.


# School #

The spring of 2016 I acquired my BSc in Computer Science and Engineering and I
am currently pursuing my MSc in [Computer Science, Algorithm's, Languages and
Logic](https://www.chalmers.se/en/education/programmes/masters-info/Pages/Computer-Science-algorithms-languages-and-logic.aspx)
at Chalmers University of Technology.
I have chosen to target my degree at `Machine Learning` and `Artificial
Intelligence`, but I have also taken courses about game theory, optimization and
general algorithms.

# Work #

Before I started my master's studies I spent a summer (2016) working for NASA at
the Goddard Space Flight Center.
(You can find mine, and my comrades, work
[here](https://github.com/ErikThorsell/GSFC_Internship/).)
The following summer (2017) I held a position at Volvo Cars AB, as one of 30
students that were admitted to Volvo's [VESC
Programme](http://www.volvocars.com/intl/about/our-company/careers/students).
As part of said program I will also be doing my thesis at Volvo Cars.

During the first year of my master I worked part time at
[NEVS](https://www.nevs.com/en/) as an engineer (I did all sorts of stuff, hence
the ambiguous title, but mostly Matlab and LaTeX).
Now, doing my second to last semester at Chalmers, I work part time for [Machine
Intelligence Sweden](http://dataintelligence.se/) as a Machine Learning
Engineer. MIS is a small startup founded by [Devdatt
Dubashi](https://www.chalmers.se/en/Staff/Pages/dubhashi.aspx) and [Hans
Salomonsson](https://www.linkedin.com/in/hanssalomonsson/), Chalmers professor
and alumni respectively.

When I don't do anything related to neither school nor work I am responsible
for the music/worship in my church and my free time is spent climbing with my
fiancé, fiddling with (breaking...) my computers and reading [XKCD
comics](https://xkcd.com/1787/) (yes, I use dvorak, the [Svorak
A5-layout](http://aoeu.info/s/dvorak/images/svorak-A5.png)).


# Notes #

## Currently unavailable ##

I caught the [Intel Atom C2000 bug](https://www.theregister.co.uk/2017/02/06/cisco_intel_decline_to_link_product_warning_to_faulty_chip/).
I expect to be onboard again sometime around 2017-12-09.


[//]: # (I am a notorious note taker and throughout my education people have often asked)
[//]: # (me for notes, so I decided to upload all notes I take and share with the world.)
[//]: # (Currently they are shared through my Nextcloud installation and can be found)
[//]: # ([here](https://wirsenius.se/index.php/s/0uiVskgkO6e9onr.)

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

