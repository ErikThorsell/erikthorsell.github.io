---
title: SLIs, SLOs, and SLAs
---

I just watched a Google Cloud Tech talk from 2019 called: *DevOps Vs. SRE: Competing Standards or Friends*.
You can watch it on YouTube, [HERE](https://youtu.be/0UyrVqBoCAU) and if you want to skip to the part about SLIs, SLOs,
and SLAs you can go [HERE](https://youtu.be/0UyrVqBoCAU?t=1614).

In this talk, Seth Vargo brings up three concepts that I think are key to understand in order to grasp DevOps and how
monitoring plays a key role if you want to successfully develop and deploy software.

## SLI

An SLI is a *Service Level Indicator*.
At any point in time, an SLI will indicate whether or not a service is satisfying a specific metric.
Examples brought up in the talk are: Request latency, requests per second, and failures per request.

If you have a requirement that the ratio between successful and failed requests towards a particular endpoint must
always be above 99.99%, the SLI will tell you whether you fulfill this requirement -- at a particular point in time.

## SLO

An SLO is a *Service Level Objective*; a binding target for a collection of SLIs.
The SLO answers the question: "How many failing SLIs can we allow over a particular period of time?"

## SLA

An SLA is a *Service Level Agreement*, which is a *business agreement* between a customer and a service provider.
Typically, an SLA is based on several SLOs.


## Summary

SLIs drive SLOs which inform SLAs.
