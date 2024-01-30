---
title: SaaS should die but ONCE is here
description: A new, better and retro way to sell software
date: 2024-01-30
authors:
  - corentin
categories:
  - Blog Post
---

# SaaS should die but ONCE is here

_A new, better and retro way to sell software_

<!-- more -->

---

# SaaS makes everyone unhappy

After paying millions for Slack hosting, Austen, CEO of Bloomtech, had the unfortunate surprise to be asked to pay [78,000$ to extract his own data](https://twitter.com/Austen/status/1752064934970896626). This specific case is a bit extreme, but it highlights the issues with SaaS software and giving other company control over your software and data. SaaS is a loss for everyone. 

- On the customer side: it's easy to set up and can start cheap, but then you are trapped in additional cost, never ending subscriptions and all your belonging are locked in a proprietary system. 

- On the seller side: it's also a trap. Because you sell a service, you need to provide support, maintenance, handle security, SLA... You can't just sell it and forget it. This requires a big team, a lot of work and money.  

Is it possible to escape this pile of complexity that makes everyone unhappy?  

# Introducing DHH and ONCE
[DHH](https://twitter.com/dhh) is the founder of Ruby On rails, Basecamp, HEY and now ONCE. He is famously known for his stances against [cloud hosting](https://world.hey.com/dhh/why-we-re-leaving-the-cloud-654b47e0) (vs. on premise), [apple fees](https://twitter.com/dhh/status/1743378607437680713), [javascript typing](https://world.hey.com/dhh/turbo-8-is-dropping-typescript-70165c01) and now [multi-tenancy](https://world.hey.com/dhh/multi-tenancy-is-what-s-hard-about-scaling-web-services-dd1e0e81). 

His new project, [ONCE](https://once.com/), intend to sell software in a new way a one time fee for a self-hosted software. Their first project is [Campfire](https://once.com/campfire-54cg31), a slack-like chat software.

# How does it work
The idea is very simple: you pay *once*, and you get the software, end of story. No monthly fee, no service fee, nothing. You get a single step setup procedure that you should host yourself, on your own server (whether it's on premise or on a cloud VM). 

Under the hood it relies on Docker to handle the installation on all platforms with a unique and personal (per-client) script to install the whole platform. Including SSL certificates, database (SQLITE), back-end (Ruby on Rails) and front-end. The whole [setup procedure is a 5-minute thing](https://twitter.com/dhh/status/1748378865725329495), not so bad for a self-hosted software, maybe even faster than SaaS setup.

For the user app side, they went with simplicity by only support PWA (Progressive Web App, it's like Webpage that you install in a borderless browser), controversial choice but very efficient in terms of development time. Does it scale ? Yes, a single Raspberry pi 5 deployment can handle [250 concurrent users](https://twitter.com/dhh/status/1751980092232978496).

# But why is it so good ?
There is multiple reasons why this idea is very promising:

- **Full ownership**: you own all of your software and data, do whatever you want with it, it's yours.
- **Simplicity of the infrastructure**: there is something beautiful about a software running on a single server, in its own container. Docker is a beautiful tool, it should be used more often.
- **Predictable cost**: one payment upfront, no surprise.
- **[Open-Source and Modding](https://twitter.com/dvassallo/status/1751440942752825741)**: because your instance code is yours you can do what you want with it and specifically add your new own features, and you can totally inspect the underlying code. This modding capability is one of the best thing that happened to video games, it's exciting to see it on software.
- **[New licence type](https://twitter.com/dhh/status/1748445489648050505)**: the ONCE licence is a tribute to MIT licence, and protect the copyright and distribution of the software while allowing modifications. It gives a great scaffold for people wanting to build ONCE-like software.  

Customers get a predictable and cheap cost, easy to set up, privacy respecting, fully owned software. Seller gets a one-time payment, no extensive maintenance and support work (except for bug and security fix) and no SLA. It's a win-win situation.

**I think there is a lot of things to learn and inspiration to take from this project. Single payment, self-hosted easy to install software sounds like the future I wish software selling would pursue.**
**Interesting blog post ? You can follow me on Twitter: [@corentinm_py](https://twitter.com/corentinm_py)**