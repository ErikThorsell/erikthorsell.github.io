---
layout: default
date: 2017-06-13 HH:MM:SS
---

# Resources #

* [My resumé]({{site.url}}/download/erikthorsell_cv.pdf)
* [My GitHub-page](https://github.com/ErikThorsell)
[//]: # (* [~My notes~](https://wirsenius.se/index.php/s/0uiVskgkO6e9onr))

[//]: # (* [~My notes~](https://wirsenius.se/index.php/s/0uiVskgkO6e9onr))

---

# An Introduction #

My name is Erik Thorsell and I created this site to have something to put on my
resumé as a point of contact between you and me.
The idea is that this site may act as a springboard to relevant information
about my persona.
If you found this site through *other* means but my resumé, [here is the
resumé]({{site.url}}/download/erikthorsell_cv.pdf).

So, let's begin.

# Current Status #

I am currently doing my master's thesis at Volvo Cars.
The topic of the thesis is: `Route pattern identification without spatial
information` and concerns whether it is possible to utilize machine learning to
predict said patterns without said information.
My thesis is to be done late May/early June 2018, and after graduation I hope to
combine my interest for machine learning and data analysis with my people skills
and find a job which combines these!


# School #

The spring of 2016 I acquired my B.Sc. in Computer Science and Engineering, and
I am currently pursuing my M.Sc. in [Computer Science, Algorithm's, Languages
and Logic](https://www.chalmers.se/en/education/programmes/masters-info/Pages/Computer-Science-algorithms-languages-and-logic.aspx),
both at Chalmers University of Technology.
I have chosen to target my degree at `Machine Learning` and `Artificial
Intelligence`, but I have also taken courses in game theory, optimization and
general algorithms.

# Work #

Before I started my master's studies I spent one summer (2016) working for NASA at
the Goddard Space Flight Center.
(You can find mine, and my comrades, work
[here](https://github.com/ErikThorsell/GSFC_Internship/).)
The following summer (2017) I held a position at Volvo Cars AB, as one of 30
students that were admitted to Volvo's [VESC
Programme](http://www.volvocars.com/intl/about/our-company/careers/students).

During the first year of my master I worked part time at
[NEVS](https://www.nevs.com/en/), doing all sorts of stuff, but mostly Matlab
and LaTeX).
During my penultimate semester at Chalmers, I worked part time for [Machine
Intelligence Sweden](http://dataintelligence.se/) as a Machine Learning
Engineer. MIS is a small startup founded by [Devdatt
Dubashi](https://www.chalmers.se/en/Staff/Pages/dubhashi.aspx) and [Hans
Salomonsson](https://www.linkedin.com/in/hanssalomonsson/), Chalmers professor
and alumni respectively.

When I don't do anything related to neither school nor work I am responsible
for the music/worship in my church and my free time is spent climbing with my
fiancé, experimenting with with computers, and reading [XKCD
comics](https://xkcd.com/1787/) (yes, I use dvorak, the [Svorak
A5-layout](http://aoeu.info/s/dvorak/images/svorak-A5.png)).


# Notes #

## Currently unavailable ##

I caught the [Intel Atom C2000 bug](https://www.theregister.co.uk/2017/02/06/cisco_intel_decline_to_link_product_warning_to_faulty_chip/)
and setting up my Nextcloud installation is on my todo-list, albeit not the top
priority.
Hence, it might take a while until the notes appear here again.


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

