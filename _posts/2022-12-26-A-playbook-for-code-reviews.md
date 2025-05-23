---
layout: post
title: A playbook for effective code reviews in engineering teams
---

[Keywords: Code Review, Engineering Excellence, Team Growth, Code Reviewer Persona, Collaboration]

Most observations I have made in the past regarding engineering teams, have been of typical six to eight person squads working on applications with web + mobile front ends and multiple backend systems, utilizing a specific branching strategy with code review gates that determine what gets integrated and moves downstream. 

I have generally viewed these gate keepers (i.e. the code reviewers) at a high level through five lenses: The programming expert, the domain expert, the clean coder, the hacker, and the historian/custodian. Anyone who reviews code can be viewed as someone with a unique overlap of these five distinct personas/traits. Note that these are not borrowed from anywhere, they are my personal classification of the many engineers I have observed and worked with in the past, and the manner in which they approach reviewing changes in a code base.

**The programming expert**

The in-depth subject matter expert in the specific programming language and/or tech stack. Knows the ins and outs of the language and its idiomatic usage + application. These engineers may have the potential for unintentionally splitting hair over technicalities, but they have a keen sense + understanding on when the technology is used or applied the wrong way.

**The domain expert**

Knows the business domain extremely well, and has been exposed to the majority changes in the business that has evolved the organization as well as the system, through time. This engineer is generally a long time team member who would have been present at the inception of the system. He or she will also probably be the person who will be able to explain the meaning + function behind almost every table and column in the database. They can look at a PR and immediately let you know how and why some lines of code are violating a subtle and little known business rule in the system.

**The clean coder**

The clean code and clean architecture evangelist + advocate. They will scan the code for readability, naming conventions, code + design smells, modules/functions to be refactored, and other deviations from clean code + architecture practices. These engineers provide feedback that helps keep code maintainable, readable, and manageable.

**The hacker**

The engineer who points out where your code changes are potential vulnerabilities for attack vectors. These engineers are always in threat-modelling mode, and most probably have prior history and experience working in systems that have needed heavy security hardening. These are the people who give key feedback that help close out security loopholes in your code.

**The historian/custodian**

In most cases a senior engineer with the organization for a long time, who would have been part of initially setting up the project and system. He or she can understand whether a code change is violating established conventions/patterns/practices used by the team, and/or deviates from the system design + architecture. They understand when a change (or an individual approach to implementing/improving something) is going to adversely affect the team and system (A great example borrowed from Kent Beck: In a restaurant, all the cooks know where the knives are. If someone changes the location of the knives, albeit to a better place, it will slow down the productivity of the cooks by impeding on their knowledge and usage of where the knives were by convention - [there are better ways to manage this type of improvement](https://tidyfirst.substack.com/p/the-story-of-a)).

So, what does this mean for someone who wants to be better equipped at conducting increasingly more effective code reviews? Below is a playbook that I have drawn up over time, and observed to be very effective within engineering teams when applied:

- I have never seen anyone (myself included) who is an expert in **all** the five personas described. Work towards being an engineer who is a better balanced overlap of all the five personas above. e.g. if you are an in-depth expert in your programming language, try to learn more about the business domain, clean code/architecture practices, OWASP top ten and secure coding, and probe into established team conventions/practices that are more culturally driven and nuanced. The more you immerse yourself in the business + team and pull information from them, the faster you will learn. Expecting to get better at all five traits while cruising by and waiting for information to be pushed to you, is not going to cut it. Communication and proactive involvement are the key game changers here.
- Collaborate with the authors of code changes, and walk through the code change over a call + screen share or shared workspace + monitor. If you are new to the business domain and codebase, this will help you ramp up while at the same time providing the stage to give your feedback + input, as well as clear out any doubts in real-time.
- Together with the team, decide and lay down expectations on how a code change will be structured and presented (e.g. detailed PR description with enough context, PR size should be <250 LOC, screenshots where required, etc.) that will enable reviewing a code change to be an easy, small, focused, and efficient exercise. Define exceptions to this structure, and how they will be managed.
- Automate everything that tends to be nitpicked: tab space convention, which line curly braces should start, formatting, cosmetic concerns, etc. There are many tools out there that can be used to automate a lot of these away.
- Compile [a simple code review checklist](https://linearb.io/blog/code-review-checklist/) that will help anyone new to the code base. This will be a common ground level check for verifying core team conventions and rules of thumb such as readable code, meaningful naming, no magic numbers, no commented code, if cyclomatic complexity in a function is >8 then extract and refactor into two functions, etc. This list should ideally have items that cannot be automated.
- Pair up on conducting code reviews - e.g. for a given pull request, pair an engineer weak in the business domain + strong in the programming language, with an engineer strong in the domain + is a historian/custodian of the dev conventions, to review the PR together. Maintain a list that contains pairs of engineers who complement each other’s strengths and can learn from each other, from which you can pick and assign to review code changes.
- [Go one step further than pairing to review code](https://twitter.com/allenholub/status/1549454425378328576) - pair program, and/or mob with engineers during development. This (mostly) removes the need for a code review gate and gate keepers, which frees up quite a bit of time and effort. **But approach this practice with caution:** the caveat here is that you might need a well rounded set of engineers (who collectively display a strong overlap of all five traits/personas) to pair or mob with, in order to have the changes implemented and endorsed real-time through all five lenses described above. If not, you might need a checkpoint again after the change (else the persona representative missing during pairing/mobbing will point out the problems from their perspective, after the change is done and/or has gone into production).

In most teams that I have worked with, the above strategies have worked really well. Mobbing, not so much, as it has been challenging to get a well rounded group (making up a good balance of the five traits) of engineers together at the same time, especially in distributed teams across time zones. And even when we have done so, mobbing to build out features didn’t scale well when the expected feature requirements start growing and queuing up. From where I stand, mobbing is still an exploratory area. Alternatively, in the current teams I work with today, pair programming has worked extremely well and has reduced the cognitive load of changes to be reviewed.

So, what will work for you and your team? Experiment with different strategies from the above list to see how well they work for you, and let me know of any new ones that you have learned or practice in your teams. Above all (and more so if you are a senior engineer, team lead, or people manager), create the psychological safety net where engineers have respect + trust within the team to help each other grow. The more you educate your team and champion engineering excellence, the more they will cultivate new found appreciation + focus towards code reviews.
