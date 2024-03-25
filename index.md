---
layout: single
author_profile: true
title: "It's all about feedback"
---

My name is Erik and over the last ten years I have been very interested in the
concept of conveying information.
Sometimes it concerns teaching a class or a colleague about something by giving
a live presentation.
Sometimes it's about writing documentation, a news article or a blog post.
Regardless, it is **always** about you knowing something and a wish to share
that _something_ with someone else.

During my university studies I started teaching mathematics to younger peers
using the [Socratic method](https://en.wikipedia.org/wiki/Socratic_method);
and quite early on realised that I wanted to make a career out of understanding
-- and helping others understand -- how people and organisations can be more
efficient when it comes to creating and sharing information.

Since graduating, I have been able to combine my interest in technology with
the one I have for conveying information in the areas around _Continuous 
Everything_[^ci] and today, I run a small consultancy company focused on
solving the issue with _feedback_ in tech organisations.

> What is feedback really? \
> How do we ensure we get the right information to the right people? \
> Who is responsible for acquiring the data? \
> How does this even relate to programming, building software and tech in general?!

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
