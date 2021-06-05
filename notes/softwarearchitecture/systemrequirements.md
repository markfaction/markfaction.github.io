---
layout: page
title: System vs Functional Requirements
permalink: /notes/softwarearchitecture/systemrequirements
---

Engineers and developers are able to define the data schemas, n-tier application layers/components, internal/external dependencies, sub-systems, and other technical concerns, that will come together to comprise an application that can satisfy the _functional_ requirements of a particular system. But this is still not 'architecting' the system, specifically, the ***system*** requirements have not been dealt with. More often than not, they are given a cursory glance and deferred to a chronological future point where something (always) goes wrong and firefighting ensues.

From what I have observed, primarily with how our CTO at :Different influences architecture and technical decisions, as well as in my prior experience working with many good engineers and architects, a prime responsibility of a tech-lead/architect role is to analyze, plan, and satisfy the functional requirements __as well as the system requirements__ (otherwise also known as non-functional requirements), making necessary architectural trade-offs and decisions, thereby ensuring system outcomes that are optimal for 

 - the overall health and reliability of the system
 - human users utilizing the behavior implemented to satisfy functional requirements
 - the graceful evolution of the system (without having to rewrite it from the ground up one year after it goes live, or regretting technical choices made)
 - observability, monitoring, and tracing potential negative system behaviour
 - extensibility and scaling (whether it's humans and/or external systems/processes)
 - business success (partly a function of getting everything above right in the first place)

Also, this by no means implies that developers do not have any responsibility or accountability for system requirements. Churning out code that satisfies functional requirements is easy. Writing efficient code that satisfies functional requirements _and_ optimizes serial process/request latency is hard.

System requirements can be classified and categorized in many ways (as exemplified with a quick Google search), but the main proponents in most systems would be the following:

1. Performance
2. Scalability
3. Security
4. Reliability
5. Deployment
6. Technology stack


