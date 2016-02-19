---
layout: post
title: "Project yet name unknown"
date: 2016-02-17 21:17:34 -0800
comments: true
categories: Project 2016
---

Some initial ideas about this project.

By the end of year 2015, I start to get my hands on some DevOps works by chance. It turns out pretty interesting. I am surprised, shamed that how little that I know of this area, and amazed by how fast the technology evolves. Puppet, Chef, MCollective, Docker...all these fancy terms make me so eager to put them on my LinkedIn profile, which ends with this open source idea. Well...I am not even sure about the term "Open Source" is legit in my case. I will probably just put all my codes and documentations somewhere on the Internet publicly and that's all.

Okay, back to the topic. I am thinking of building a dev to release style of pipeline to reduce the unnecessary distraction from non dev works by providing a sort of user friendly interface to inspect a vm's states. At least for the demo and testing purpose. I don't really see too much of actual enterprise level benefits from this project. More of self education purpose.

After couple hours of research, I come out this premature technology candidates:

1. Container will be hosted by AWS Docker enabled environment.
2. Jenkins CI(Continuous Integration) Jobs will be triggered by github post commit actions.
3. Chef runs will be kicked by Jenkins job.
4. Possibly integrates with kitchen for Chef testing.

Roughly saying, I want to give it like a 6 months plan. After first three months named stage one, I would want to be able show it to my team as my side project. So it may focus on a certain set of use cases. The last three months named stage two, I would want to focus on optimizing its scalability. And if goes well I can learn more feedback from the community if this project really worth taking a look at.

Stage one will do a one week sprint planning.
I will divide epics based on technology key word:

1. AWS + Docker
2. Jenkins CI
3. Chef Kitchen testing

Sprint 02-17 ~ 02-24:
-----

1. Learning 101 on AWS + Docker. Deliverable: re-open my aws account, set up a running instance, install docker.

2. Learning 101 on Jenkins. Deliverable: Install Jenkins on the docker image.




