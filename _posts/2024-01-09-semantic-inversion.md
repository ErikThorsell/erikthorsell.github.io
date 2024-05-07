---
title: Has DevOps become the new Agile, in a bad way?
classes: wide
---

I had not yet started working when the [Agile Manifesto][agile-manifesto] was
written, but when I learned about it and its implications I was immediately
hooked.

> **Individuals and interactions** over processes and tools  
> **Working software** over comprehensive documentation  
> **Customer collaboration** over contract negotiation  
> **Responding to change** over following a plan  

Four concise statements which identify the importance of getting things done and
understanding that iterative work and continuous communication is key to
building good software.
My first opportunity to try these concepts out for myself -- in a software
development context -- arose when I worked a little along side my university
studies, with companies where autonomy and flexibility was imperative.
Then I graduated and I got my first full time job, at a large engineering
company, and my _agile bubble_ was popped.

All of a sudden, _agile_ meant:

* "We use [SAFe][safe] and plan our work in Jira."

and:

* "If the PM wants to change something last minute, we need to be agile."

especially in combination with:

* "No, you don't talk to the customers, that's done by _the stakeholders_."

When us youngsters tried to discuss whether our way of working was an efficient
use of time and money, we were told that agile only worked in theory and SAFe
was a real world implementation.
We looked at a version of the image below and sighed.
The image is a perfect example of how to incorporate the right hand side of all
statements above.

<p align="center">
  <a href="https://scaledagileframework.com/wp-content/uploads/2023/03/Full-1.png">
    A link to the SAFe image.
  </a>
</p>

Fresh out of school, I figured that maybe they were right...

## A semantic inversion?

Fast forward to today and I have had the opportunity to work with many
engineering companies, ranging from 10 to 100 000 people strong.
What I have noticed is that it's more fun -- and companies tend to be better at
solving their users' problems -- when they work in ways which relate to the four
statements at the beginning of this post.

And I want to emphasise that _SAFe_ is not the only culprit here.
I have worked with companies who sprinkle mandatory meetings and processes all
over their work weeks, all in the name of "being agile"; often motivated by a
need for communication and ensuring everyone knows what's expected of them.
Great intentions, but poorly executed.

I have also noticed that the companies who embrace the statements above tend to
not call themselves _agile_, they just do the work that needs to be done to
solve their users' problems.
They live: _people over processes_.

> Has _agile_ done a semantic inversion and come to mean the opposite of what
> it was originally meant to?

## Is DevOps going down the same route?

When I talk to companies about DevOps, I often find that they are surprised
by my focus on the agile fundamentals and developer enablement. 
They are mostly interested in which CSPs I am familiar with and if I have
experience with their suite of tools.
Often, they want me to join their "DevOps Team" and when I ask what this team
does I often get a response similar to:

> Our DevOps Team is responsible for managing the pipelines which build and
> test our products.

To which I always counter with two follow up questions:

1. Why is it that your developers are not responsible for this?
2. Who is responsible for deploying the products?

More often than not the first question is answered with: "They don't have the
competence." or "We want them to focus on coding." and the second one with:
"That is done by our operations department."

Instead of tearing down the wall over which developers throw half working code
for operation to try and deploy, a new wall has been erected.
A wall which separates developers from their builds and tests by obscuring them
in YAML and organisation-wide CI gates, imposed by _someone_; but likely not by
the dev teams.

Too many times, "The DevOps Team" has become a part of an organisation which
imposes restrictions instead of focusing on developer enablement.
Instead of helping the development teams own their deliverable's life cycle --
by taking a sideline role, fully focused on support -- the DevOps Team is wedged
in between the developers and operation department, effectively moving the
developers even further from the end-users.

And just like agile has been devoured by processes, the very thing it strived
to eradicate, DevOps has become a checklist; ensuring we use certain tools
when -- at its core -- DevOps is just a never ending loop.
Its only purpose to provide a way for developers to take complete ownership of
their deliverables' life cycle.


## The buts and exceptions

I am **not** opposed to meetings and tools and am by no means a proponent of
anarchy!
There are many tools that can help an organisation be more agile, and striking
a good balance between asynchronous, digital and in-person meetings is key.
In my book, a daily meeting where people share information about changes to
their previously communicated plan is great[^daily] and I believe the
retrospective is one of the most important meetings a team can have.

When it comes to tools, being able to deliver "working software" while also
"responding to change" at any scale becomes impossible without continuous
integration and proper version control; both require tools.
Which tools to use depends on the organisation and what problem we intend to
solve and it's excellent that there are many good tools out there.
Thy dynamic workloads enabled by cloud, the reproducibility offered by
infrastructure as code, and the traceability that comes with an issue handling
system like Jira; they're all needed (to some extent), we just need to
understand why.

Lastly, in many cases, a _platform team_ is an excellent way to enable
developers to take complete ownership of their deliverable's life cycle.
By providing templates and a unified way to develop, build, test, deploy and
monitor applications, a platform team can help developers to focus on what
they do best: "Listen to the users' problems and solve them."
But don't make this team another hurdle over which the developers deliverables
must be thrown on its way to the end user.

The key takeaway here is that:

> Everything we do in our organisation should serve the purpose of solving
> our users' problems, preferably at an increasing speed.
> If a tool helps us, use it; if a meeting is needed, have it; but when push
> comes to shove, the developers are the ones who solve the users' problems
> and therefore the rest of the organisation must always focus on helping
> them do their jobs.

---

I have previously written a post about planning which you can find
[HERE]({{site.url}}//2023/11/01/planning.html).
It describes the concept of _planning proportionally_.

<!-- --------------------------------------------------------------------------------------------------------------- -->

<!-- FEET NOTES -->
[^daily]: My best tips for having a daily/stand-up is to make attendance
    mandatory, but everyone should **not** be expected to share something.
    Don't go around the table and expect everyone to say: "What they did
    yesterday, what they plan to do today, and whether they need help.",
    instead, have people share whether they need help and whether things
    are _not_ progressing according to plan.
    This way, the meeting becomes relevant and short.

<!-- REFERENCES -->
[agile-manifesto]: http://agilemanifesto.org/
[safe]: https://scaledagileframework.com/