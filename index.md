---
layout: single
author_profile: true
title: "It's all about feedback"
---

A successful company is able to provide a monetised solution to a user's problem.
That seems easy enough, until you ask yourself the first (obvious) question:

> What problem am I trying to solve?

You might be able to find a problem in your own life and think: "Others _must_
have the same experience. I'm going to solve this!"
After thinking hard, filling sketchbooks and whiteboards with ideas, and months
of work you finally have your _thing_.
Which gives rise to the second question:

> Will my users pay for the solution I'm providing?

In a perfect world, you _are_ able to count your chickens before they've hatched
and can confidently say that your solution will be well received and loved by
your users.
But the world is not perfect.
Until you have made your solution available to your users, you will not know
whether they like it or not.

Phrased differently, you find an answer to the question above by receiving
`feedback`.

Releasing a product will always come with an inherent risk of failure, but it is
possible to minimise the risk by incorporating `feedback` in your development
process.
For instance, you can gather feedback by creating prototypes, made out of
cheaper materials, in smaller quantities, with limited functionality, and have
a few users test your product for you.

More specifically, in the case of software development, we have multiple phases
between thinking:
_"Hmm. Will the user want this change?"_ and actually shipping a new version of
our software, where we can gather feedback to better learn whether we are
building the right thing.

I run a small consultancy focused on solving this simple (yet so difficult) task.
If this sounds intriguing or interesting, checkout my
[_work with me_]({{ site.base }}/work-with-me/) page.
You'll find more info about me and my company there, as well as my preferred ways
for you to get in touch.

---

# Latest blog posts

{% for post in site.posts limit:5 %}  
  <li><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>  
{% endfor %}  
