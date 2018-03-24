---
layout: post
title:  "Microservices: Hype vs. Value"
date:   2018-03-24 16:04:45 +0800
categories: blog seminar
author: Jerome
---

## Microservices: Hype vs. Value
Last Thursday, I and some of my colleagues attended PSIA's enablement seminar
at the Makati Shangri-La. Lucky enough, we arrived very early and were able to
reserve the seats in the best possible location - just behind the speakers'
seats, in front of the podium. 

The program had three main talks and a panel discussion;
1. Introduction to Microservices
2. Microservices with Spring Cloud (it uses Java)
3. Implementing Event-driven Microservices

I wasn't sure what to expect since it was my first time to attend a seminar
organized by the PSIA but it turned out I learned some useful and practical
insights from the seminar.

### Introduction to Microservices

The first talk was given by Lorenzo Dee who was one of the top brass (I guess)
in the company Orange&Bronze. I like how he structured the presentation. 

Instead of telling what Microservice Architecture is, he posed the challenges of growing
organizations first. These challenges are then broken down and tackled
one-by-one using the Microservice approach. Throughout the presentation, he
also made clear that Microservice Architecture is not a silver bullet and that
it is not an easy path for some of the companies who want to adopt it. 

According to Dee, the problems of growing companies are:

#### 1. Delivering Value at the Speed of Business

As the company increases in size and visibility, the need to rollout products
become faster to maintain its competitive advantage. Together with this growth
is the evident increase in the codebase and data that the development teams
need to handle. The monolith that was once small has become a gigantic,
hard-to-maintain dump of code. This size and complexity becomes a problem when
the business wants to change directions but the development can't seem to catch
up because one change in a small part of code has rippling effect to the entire
codebase. Thus, it makes sense (as suggested by Microservices approach) to
split the business into each business capability of the company, all of which
has its own Microservice. 

This splitting up into Microservices enables ecah business capability to
rollout features as fast as the want together with the development team that
maintains the Microservice. This also introduces flexibility in choosing which
technology the team could adopt for the task at hand. 

#### 2. Challenge of Deploying

When the team maintains a monolith, a small change means deploying the whole
even if there are no changes in other, possibly core parts of the system. These
deployments might be complex since all parts of the system should be checked to
make sure nothing broke during the deployment. If the system was split into
Microservices, it is now possible to deploy only one part and not affect
others. It also enables the team to scale only those services that needs
scaling. Although Dee made it clear that deploying one service might seem easy,
it actualy isn't. The task won't necessarily become small, it just became
smaller compared to the previous monolith.

#### 3. Capacity-related Changes

I've mentioned previously that with the Microservices Architecture, it is now
possible to scale a certain service depending on the need, the technology, and
the business requirement. Instead of being stuck in the technology stack used
by a single monolith, each service has the freedom to choose which stack to use
depending on the task at hand. As an example, if one service is involved with a full-text
search module, it makes sense to select a database that has great support for
it instead of using a relational database that might not be optimized to doing
full-text searches.

### Microservices with Spring Cloud

After introducing what Microservices are and showing how it can help solving
some of the challenges a growing company might encounter, he went on to the
next talk which was the usage of Spring Cloud to implement Microservices.
I won't delve into the tech itself, just acess it [here][spring-cloud-link].
My greatest take-away from this presentation are the various Microservice
Infrastructure patterns that can be implemented.

#### 1. Dynamic Configuration

This infrastructure pattern enables the microservices to be able to pull the
configuration from a single configuration server and adjust accordingly.

#### 2. API Gateway

This pattern introduces a facade for the set of microservices so as not to
overwhelm the consuming client about the possibly extreme granularity of the
APIs exposed by each service. The gateway serves as the handler of the client
request and to each of the microservices.

#### 3. Service Registry

This pattern is an approach that can be used to enable a Consumer service to
connect to another Producer service that might have several instances or to
ease the discovery of other services for the Consumer service. The Service
Registry has the option to do client-side load-balancing usually using the
round-robin approach which can possibly reduce the cost of having an external load-balancer.

#### 4. Circuit Breaker

Finally, this pattern enables the microservices to have graceful handling of
misbehaving services. The concept comes from the house circuit breaker which
protects the house appliances from abrupt fluctuation in electricity. The
Circuit Breaker makes sure that connections to a service is continuous,
otherwise it will issue a notice to that the service is misbehaving and
regulary check until that misbehaving feature is finally okay.

### Implementing Event-Driven Microservices

In this final talk, another speaker, Sofia Ang (a senior developer from
PayMaya) talks about how to approach breaking down a monolith to possible
microservices using the method EventStorming (playing on the words Events and
Brainstorming) while introducing the concept of a Saga, and how Orchestration
and Choreography of microservices could together solve some of the problems of
each approach. She interestingly presented everyting using sketches she made
on an iPad.

#### EventStorming

In this segment, she talked about how to organize the core events into each
microservice and identify the policies and commands involved in the e-commerce
system example. Saga was also introduced, which from my understanding is just
a long story (like an epic. did you get it?). This became the foundation for
the next segment which was ...

#### Choreography vs. Orchestration

In this segment she differentiated the differences, advantages, and
disadvantages of Choreography and Orchestration.

Orchestration is an approach where you basically have a _maestro_ who conducts
the whole process from beginning to end. This approach is somehow linked to
synchoronous transactions which can also be thought of as a "blocking" approach
to the whole process. If you implement this, it would be easy to use
counter-commands to rollback the changes done or restart the Saga from the
point where it left of when a service breaks down in the middle.

Choreography on the other hand is more of an asynchronous approach. Once a service
finishes a command, it can fire up a signal that it is already done and let the
other services act accordingly to it. This way, there is no waiting time for
one service making moving on the the next request fast. 

Each had its own pros and cons and the team could choose to adopt the
combination of both to get the best of both worlds. 

### Panel discussion and Ideas that Stuck

After the three talks was the panel discussion, which my colleague pointed out
as the highlight because the questions were practical and can be used as
concrete steps for transitioning into microservices.

The ideas that stuck to us were: 

#### Skills are needed to transition

Not only do you need to be able to write a good monolith using proper OOP, you
should also be knowledgeable about Domain-Driven Design to be able to identify
the bounded context properly to lay out the Microservice infrastructure. 

#### Microservices is not for everyone

This architecture is advanced and thus needs skills and control in place.
Debugging itself can be harder if all is not planned properly. Logging and
monitoring should be established enough to aid in identifying the bottleneck in
the system. For other teams who maintain a relatively small product for now
might not need to adopt this architecture but can choose to make services
little-by-little when the product is already growing bigger. Also, it is not
advisable to go full on Microservices if there really isn't a need. 

#### Good Design should be the Foundation

They said that "If you can't write a well-written monolith, Microservices will
be for naught" (this is non-verbatim, but I guess you get the point). If you
don't have the skills and the Dev-Ops mindset, implementing Microservices will
be the same with maintaining multiple monoliths.

## Wrapping it Up

After all the things that I've written based from the talk, they just basically
say that you better be prepared when you choose to adopt Microservices. You can
do it on one of the business capabilities first, then slowly ease into
converting other services once you get the hang of it.

[spring-cloud-link]: http://projects.spring.io/spring-cloud/

Link within Post [link][link-ref]

[jjlink-ref]: http://path/to/link
