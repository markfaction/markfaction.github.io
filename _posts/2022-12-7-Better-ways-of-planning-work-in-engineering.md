---
layout: post
title: Discovering better ways of planning and delivering value in engineering teams
---

One of the many problems I’ve observed in the past with how teams use SCRUM (and other prescriptive approaches under the label ‘Agile’), is the manner in which a.) planning work, and b.) delivering value is addressed. Teams would portray a segment of their delivery pipeline, showcasing a stream of technical tasks moving downstream. Planning work generally entails prioritized user stories coming in from the business, and dev teams breaking them down into technical tasks and pulling them into a workflow. 

Some key drivers of this approach are managers expecting developers to estimate stories and provide a fixed ETA, tracking time, and remnants of waterfall era traceability habits of ‘tracking everything you do under an issue/ticket’ (even if it’s a 5 minute fix). A developer’s intuition may suggest “Let’s break this story down into detailed technical tasks, so that we know close-to-exactly how long each one will take, and then implement + integrate them back together again”. Once the sprint demo is done though, developers wonder why a lot of things they committed to could not be completed, why there is so much rework after the demo (on top of things not working properly during the demo), and why the heck they don’t have enough time to plan for the next sprint before falling into the same death spiral again. 

During my past tenure at [:Different](https://different.lk/) as an engineering team lead, we tweaked some changes in the way engineers plan and breakdown work (given a business roadmap), with profound results. Spearheaded by the engineering leadership of the organization and coupled with buy-in from the engineers, the changes in how work was planned and value delivered, created a new way of looking at delivery expectations, both from an engineering as well as business perspective. It also resulted in better engineering productivity, a reduced bug/failure rate, faster cycle times, users being able to see and test incremental value funneled through the delivery pipeline at a regular cadence, and time-boxed iterative planning activities that did not exhaust the engineering team - but ensured that a small batch (three to four days worth) of prioritized work is ready for the team to pick up.

These learnings and takeaways are something that I actively advocate, apply, and continuously improve, within the teams that I work with today. For the past few months at [Corzent](https://corzent.com/index.html), we (the team that I work with) have conducted some interesting experiments, and radically optimized the way the engineering team plan and breakdown business expectations, and deliver value to end users. This post is a short account of how engineering practices within the team evolved, in discovering better ways of planning work and delivering business value to end users.

In the beginning, business requirements/stories were broken down into tasks (in a Kanban workflow), that would be flagged as ‘UI’ tasks, ‘API’ tasks, or ‘Integration’ tasks, and so on. Almost all assignable work items would be horizontal slices of functionality (labelled under the horizontal hierarchy it falls into - UI/API/DB) or an integration/configuration/miscellaneous technical task. The first step we took was to do away with the horizontal slicing of stories into UI/API/Integration/DB tasks, and start breaking down user stories into thin vertical cross sections of end-to-end functionality. 

To show how this works, here’s an example of a (highly oversimplified) requirement from the business: “As a user, I want to fill in the application details and save them in the system”

The developers, when planning work, could potentially break this story down into the following three story slices:

1. As a user, when I click the save application button in main view, I should see a modal popup to enter the application details
2. As a user, when I enter the details into the applications detail modal, the entered values should be validated
3. As a user, when I enter valid application details in the modal and click on save, the application should be saved successfully in the system

The above three story slices are extracted from the original story. What should be observed and emphasized is that:

- Each story slice can be implemented by a developer and independently deployed
- The first two stories slices do not implement the save functionality. Clicking the save button might display a ‘work in progress’ or ‘under construction’ message/toast
- The scope of each story slice is added in the description/acceptance-criteria, so that anyone testing understands what needs to be verified when testing the specific story slice
- The cycle time of each story slice is between half to one day - anything larger is further sliced
- Story slices are not technical sub-tasks of a user story - they do not mention any technical work nor give any indication of what part of the system will be touched (i.e. UI/API/DB). The story slice encapsulates any technical details, and showcases only the value statement to the end user
- Implementing a story slice could result in one or more pull requests, which are linked to the same story slice. The PRs could be for a front end UI client, back end API service, configurations, integration, DB, whatever - anything that needs to get the story slice up and running, and ready to be deployed
- If incremental work in progress denoted by story slices should not be visible in production until the feature set is complete, they can be implemented behind a feature flag, which can be toggled on for developer and test deployment environments

<img src="/images/post-2/blog-2-story-slice.jpg" style="display:block; margin-left:auto;margin-right:auto;width:50%">

A developer would then take a story slice into the Kanban workflow, implement it, raise pull requests for review, and merge + deploy the changes, all within the span of roughly half a day.

 Observable outcomes were 

- Faster cycle time - implementing small units of value imply small PRs, which in turn makes the review/merge/deploy/feedback loop run faster
- Improved developer productivity and agility - the depth of the problem domain + technical solution of a story slice is far smaller and digestible than a complex business expectation compressed within a single user story
- Users/quality-engineers see feature updates sooner and at a regular cadence, giving them the ability to provide feedback faster - this reduces rework stemming from bulk changes and infrequently tested regressions
- The business gains predictable insight into the ETA of features and feature-sets, based on monitoring the regular cadence of value being delivered and observed downstream

There were some caveats that we encountered and learned from, two of the more important being:

1. User stories (and hence story slices) can evolve with time. A user story is not a business expectation set in stone, and therefore should be treated as such. A key point that the team discovered was to get into story slicing only after the business problem is clearly understood + clarified with users, any foreseeable system/architectural constraints related to the requirement are addressed, and space for the possibility of the story evolving with time is provided/accepted by engineers and the business.
2. We could not completely avoid stories that are only technical in nature, that are more often than not, sourced by engineering. Whether it’s refactoring, small configurations, or automations, there will be stories that are produced due to engineering necessity not directly related to business user stories/slices. In these cases, we generally prefix the story with [Dev] to denote that it is an isolated technical story - E.g. “[Dev] Remove unused function foo() of class bar, in order service business layer ” (This specific example is again oversimplified and may not need a story/task, but for the sake of demonstrating how we use this…)

<img src="/images/post-2/blog-2-user-story.jpg" style="display:block; margin-left:auto;margin-right:auto;width:60%">

On another note (and hopefully a future post), the team also brainstormed and came up with a brilliant way of handling highly complex business requirements that could potentially impact the existing architecture and system design. These type of requirements were non-trivial to be directly taken up for story slicing. The approach drawn up by the team turned out to be a very effective ‘functional breakdown and dependency context diagram’ (we are trying to come up with a better name for this), that maps the highly complex requirement(s) into a set of root work items (e.g. implement feature flag for complex feature X) from which all other dependant functional work items branch out in a tree-structured schematic, overlaid by contexts and bounded scopes of impacted systems, sub-systems, and external actors/systems/services. The team grows and evolves this map iteratively, as and when more insights are discovered.

This resulting (but constantly evolving) map/schematic of the complex business requirement helps the team navigate and break down the story slices, and helps ensure there is no overlap/duplication of scope between different stories/slices, as well as avoid missing stories/slices that are edge cases or hidden in the initial requirements (which were problems we initially had when we tried to do story slicing of highly complex requirements without having a visual aid/map/model, and tried to keep all the complexity in our heads). The in-depth details of how this map/diagram was born, how it helps the team decompose highly complex business problems, and how we keep evolving it fueled by our continuous learning, is a story/post for another day.

Looking at how we are learning and evolving our work approach and engineering practices in my team, I am reminded of some key highlights from Alistair Cockburn’s talk - [Getting to the Heart of Agile](https://www.youtube.com/watch?v=sr5wfygbY7k) (I highly recommend watching this if you are in engineering), where he mentions that the world is always in a constant state of change, and to be agile, entails frequently probing the world and getting a feel for what is changing. The value stream of a deliverable or a final outcome (i.e. software system, mobile app, console game, physical product, marketing campaign, scientific/news periodical, etc) is injected with thousands of decisions by hundreds of people within an organization. The final outcome is the embodiment of these hundred thousand or so decisions. Statistically, a person can make a mistake in one out of five (or ten) decisions they make. This could be compounded by people dependent on other people’s decisions, to make their decisions, in a complex web of decision dependencies. This implies that we are shipping roughly 10,000 mistakes or bad decisions into production, wrapped within the artifacts and services that we deliver. 

The engineering practices we are evolving and the experiments we conduct at [Corzent](https://corzent.com/index.html), are geared to shrink the number of ‘decisions in process’ at a given time, and to discover better ways of probing the wider organization to get faster insight and feedback, which will help us reduce the foot print of mistakes we make in our decisions throughout the value stream. This will be an interesting engineering journey that I hope to document more in a series of upcoming posts.
