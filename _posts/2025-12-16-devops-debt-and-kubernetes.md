---
title: Kubernetes exposes your DevOps debt
---

Kubernetes is a _point of contention_.

Some look at it in awe and believe _it_ will solve most (if not all) of their application's problems.

If the app does not scale under load: _Use Kubernetes._  
If the app cannot handle zero-down-time upgrades: _Use Kubernetes._  
If the team working on the app is too slow: **_Use Kubernetes!!_**

Others look at Kubernetes with a mix of disgust and fear.

_Kubernetes_ is a huge beast of complexity.  
_Kubernetes_ requires an entire new operational skill set that most teams do not have.  
_Kubernetes_ is not even necessary!

What both sides tend to miss is not what Kubernetes _is_, but what it is _for_.

Kubernetes does not magically make applications scalable, resilient, or fast to change. Instead, it provides a powerful
execution environment for applications that are already designed, built, and operated with those qualities in mind. This
is why organisations migrating to Kubernetes should spend far less time debating YAML manifests and far more time asking
how well their applications and teams adhere to the fundamentals of DevOps.

## DevOps fundamentals

As I have said before:

> DevOps is everything you need, technically and organisationally, to successfully manage the entire life cycle of your
> product.

By better understanding: [Flow, Feedback and Continual Learning; the three fundamental principles that underpin the
entire DevOps movement](https://itrevolution.com/articles/the-three-ways-principles-underpinning-devops/), we become
better informed about all aspects of the Software Development Life Cycle (SDLC). As we grasp the importance of
_feedback_ we can understand why and how we gather and act upon information from our users. When we prioritise _flow_,
we start to find -- and remove -- bottlenecks in our processes. Lastly, when we have a way of working where we feel
comfortable making frequent changes to our products, we can start to experiment and continuously learn new things which
will help us win the marketplace.

The best part? Your organisation can build on top of the three DevOps principles without even looking at Kubernetes.
Here are just a few examples, organisational and technical:

1. Ensure there is a clear mapping between each development team and their output, meaning each team takes
   responsibility for the entire SDLC of the component, service, or application they develop.
2. Make your releases smaller and do them more frequently.
3. Visualise your work and ensure _operational improvement_ is prioritised.
4. Automate. Automate. Automate! Declarative delivery and GitOps-style workflows do not require Kubernetes.
5. Build your application with observability and fault tolerance in mind.

Adhering to the above will yield a better product and as a bonus you are well positioned to migrate to Kubernetes,
should the need arise.

## What is Kubernetes, really?

Kubernetes is a container orchestrator. No more. No less. I don't mean to sell Kubernetes short -- it's an amazing feat
of engineering -- but you must not be led astray.

Kubernetes helps you deploy an arbitrary number of containerised applications across an arbitrary number of nodes,
according to arbitrary rules concerning resource utilisation. Kubernetes follows your arbitrary rules to scale up/down
the number of application instances. Kubernetes even helps you roll out upgrades of your applications in different ways
that ensures there is always at least one instance available. If you tell Kubernetes exactly how to handle your
_deployment_, it will do so -- completely automatically!

_Arbitrary._

Kubernetes is an extremely competent rule engine, but you have to write the rules! You are responsible for taking
everything arbitrary about your application and make it explicit. By better understanding how Kubernetes works, we can
learn how to write these rules, but Kubernetes does not:

1. Tell you how the architecture for your application should look in order to handle zero-downtime upgrades, properly
   utilise scaling, or be more fault tolerant;
2. Help you implement the architecture;
3. Create or enforce any of the five examples I listed under [DevOps fundamentals](#devops-fundamentals).

If you have five teams building a monolithic .NET application which is then handed over to a separate build team to be
containerised and deployed in Kubernetes, you have gained absolutely nothing. On the contrary, you have added an
enormous amount of complexity (i.e. Kubernetes) without attaining any benefits from the system.

If you have ever thought: "We need to use Kubernetes to solve \<any of the issues above\>", you will be disappointed.
The answer is not in Kubernetes itself.

## Kubernetes as a mirror for your DevOps debt

Kubernetes does not _introduce_ most of the problems organisations struggle with, but if you want to use Kubernetes
properly you will inevitably be exposed to them.

Poor (or non-existing) _Configuration as Code_ gets turned into poorly defined Kubernetes resources (the arbitrary rules
are not specified properly for your application). Fragile deployment practices surface when rollouts require manual
intervention and deployments reboot endlessly when applications are not built to handle statelessness. Not to mention
troubleshooting when you rely on logs from a pod that continuously keeps rebooting.

These are all consequences of having a large DevOps debt.

Just like technical debt, DevOps debt is accumulated slowly. Manual processes that "work for now". Releases that are
large and far between, because doing them feels risky. Being OK with a way of working that relies on heroics. None of
this breaks immediately. In fact, many of these patterns are actively rewarded in the short term.

If you start using Kubernetes, you will be made painfully aware of your DevOps debt.

## So, should you use Kubernetes?

Maybe.

I really want to stress the importance of the DevOps fundamentals. You will not have a good time in Kubernetes if you
fail to follow these principles. I don't believe you will have a good time outside of Kubernetes either, but you will at
least not be fighting your entire runtime environment.

### If you are starting from scratch

If you have Kubernetes competence in your organisation and you foresee that you will benefit from the capabilities
provided by Kubernetes, go for it! Greenfield development is lovely and you have the opportunity to build something
properly _cloud native_. Just make sure you strike a good balance between: "Building the perfect Kubernetes application."
and "Building an application that your users want to use.". It's all too easy to get stuck in the weeds.

If you do not have Kubernetes competence or don't intend to build an application that need its features, don't bother. I
_would_ however recommend that you containerise your application. Doing so helps you think about interfaces,
dependencies, building and deploying your applications early in your SDLC.

### If you are migrating

Start with refactoring! If your application is currently composed of tightly coupled services, without clear interfaces,
and code being inherited all over the place; start by fixing this. Create an application that _can_ be containerised by
its different components, _then_ do the actual containerisation, _then_ evaluate whether you can fix your issues without
Kubernetes.

If you cannot -- and only if you cannot -- start migrating your newly containerised services to Kubernetes.

> Kubernetes is not a shortcut to DevOps maturity. It is a very efficient way of discovering how much you are missing.

