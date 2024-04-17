---
layout: single
author_profile: true
title: "Hi, care for a cup ☕ ?"
---

My name is Erik and I'm a solution-oriented DevOps enthusiast, who believes
the best way to generate value in a software company is by tearing down walls
and helping developers deliver new
functionality faster.
On top of this, I like to share my experiences -- predominantly in text form --
on [the blog that I host on this site]({{ site.base }}/posts/).

Work wise I run my own consultancy company ([Request for
Coffee](https://requestforcoffee.dev)) which focuses on helping companies adopt
best practices from DevOps and Agile.
The assignments I take on are seldom alike.
Sometimes I am brought in to strengthen an existing platform team, whereas other
times I help clients both with analysing their existing way-of-working as well
as guide them along the way to their new goals.

When I'm not working I spend my time with my family, as a music leader in our
church, training for my next triathlon or fiddling with my home automation.

If this sounds intriguing or interesting, checkout my
[_work with me_]({{ site.base }}/work-with-me/) page.
You'll find more info about me and my company there, as well as my preferred ways
for you to get in touch.

---

# Latest blog posts

{% for post in site.posts limit:5 %}  
  <li><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>  
{% endfor %}  

---
[^ci]: Continuous Integration \| Continuous Delivery \| Continuous Deployment \| Continuous Improvement \| ...
