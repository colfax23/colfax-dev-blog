---
title: "TEEs are like toasters"
date: 2024-09-30
published: true
---

I’ve been experimenting with Trusted Execution Environments (TEEs) recently and I’ve been getting the question “what is a TEE?” a lot. My objective of this post is to help you understand the basics of what a TEE is and how it can be useful.

_Note: in this context, when I refer to a TEE I’m referring specifically to AWS Nitro Enclaves._

An analogy I’ve found useful when explaining TEEs is: a toaster.

![My Toaster](/images/mytoaster.jpg)
*My toaster.*

A toaster is a simple kitchen device that is very good at one job — toasting bread. Toasters are designed and built in such a way that there’s a high likelihood that it’ll toast your bread correctly and there’s a low likelihood that an undesirable outcome will happen (e.g. holes get poked in it, it disappears). Using a grill to toast bread is a different story — grills have a much larger feature set than toasters and thus can be used to accomplish many different things, however the likelihood of getting your desired outcome every time when toasting bread on a grill is much lower.

Toasters are designed intentionally with a few key characteristics in order to make this happen:
- Limited access to external resources: electricity (which it turns into heat)
- Limited interface of interaction: start/stop, magnitude of toasting
- Limited objective: toasting bread
- No memory of historical events: one toast does not affect the next toast
- Undergone rigorous QA: when a toaster arrives at your house, it’s likely to work as expected
- A record of what’s been done: the analogy breaks down a bit here, but you can have a pretty good idea if toast was made in a toaster based on the smell and whether there are lingering crumbs at the bottom

TEEs at their core are similar. They are secure, isolated compute environments in which you can deploy code to do a particular task, and because of their inherent guarantees, you can trust that only that code will get executed, resulting in your desired outcome.

Diving a bit deeper into the core characteristics of TEEs:
- Limited access to external resources: TEEs do not have external network access or persistent storage, either you need to pass in the data you want to use or in some cases you can fetch specific data from specialized storage services like key managers
- Limited interface of interaction: through code, you define the interface to your TEE catered to your exact purpose
- Limited objective: generally a TEE is implemented to serve a specific, singular purpose
- No memory of historical events: given that there is no persistent storage, one execution of a TEE cannot have an impact on the next
- Undergone rigorous QA: the code that runs in a TEE should undergo rigorous testing and you can configure them to only run predetermined and vetted releases (based on a hash)
- A record of what’s been done: you can emit an attestation from a TEE as a provable record of the computation that happened

TEEs are good for highly-sensitive tasks where it is paramount to keep data private.  They aren’t the best tool for every job, but they can be extremely useful for specific tasks.

A closing thought – configuration is key, both with toasters and TEEs.  If you set the toast setting to too dark, your toast will still get burnt.  If you misconfigure your TEE, it can result in some serious problems as well.  As with all software development, mistakes can prove extremely costly, and TEEs are no exception - proper review policies and QA are critical.

So the next time you hear about a TEE, I hope you can understand what the toaster-like functionality it is meant to be used for, and that it helps you understand why a TEE is being used in the first place (or in some cases why it shouldn’t be!).
