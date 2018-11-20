---
title: "Redundancy is important for a robust system"
excerpt: "Embrace redundancy, embrace robust"
categories:
  - articles
tags:
  - Bioinformatics
---

A robust system is dreamed of by every system designer, including me. A robust system can guarantee the system to cope with errors during execution and cope with erroneous input. A large number of areas are related to robust systems, such as life science, computer science, architecture and so on. In this part, we would like to focus on software development.

Of course, we can not deny that there are too many factors are correlated with building a robust system:

1. Evolution
   
   Like buying software, I will not purchase software if it does not keep updating. Good software should keep evolving with the environment, and function well.

2. Regeneration

   Good software should easy to transplant, regardless of platform or operating system.

3. Versatile

   Good software should consider future application scenarios and developed suitable interfaces.

4. Redundancy

   Redundancy can save the world when the disaster happens.

5. ...

Let me count the importance of those factors to the consequences without them, and it reminds me that the redundancy is the most crucial part among them. Life is the typical redundancy system, organs such as the liver and kidney are highly redundant: there is vastly more capacity than is necessary to do the job, so a person with a missing kidney suffers no apparent incapacity. If a finger is damaged, there are ways that the other fingers may be configured to pick up an object. I think only God can create this kind of robust system. We should learn from this design philosophy when building our systems. 

It occurs to me that when I design the MSI algorithm, the pipeline is only allowed the [bam](https://genome.sph.umich.edu/wiki/BAM) file with a chromosome tag "Chr". When the pipeline is deployed in the production environment, many errors emerged, including that someone using bam without a chromosome tag "Chr". As the [murphy's law](https://en.wikipedia.org/wiki/Murphy%27s_law) indicated: Anything that can go wrong, will go wrong. As long as the time is long enough and the sample size is sufficiently large. 

To tackle this problem, what I have done is only making this system a little redundancy and got it solved. Now, the system is allowed to accept a bam regardless of have or have not a chromosome tag "Chr" and the error rate is almost dropping down from 20% to 5%.  

What I would like to emphasis on here is to build a concept that to consider more on redundancy when developing a robust system. Even though creating a system with extremely robustness is hard to achieve due to program budget and deadline, but we still need to do it as a kind of pursuit of life, just like the real life tells us. 






