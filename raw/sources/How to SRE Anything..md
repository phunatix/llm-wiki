---
title: How to SRE Anything.
source: https://www.reliablepgm.com/how-to-sre-anything/
author:
  - "[[Jennifer Petoff]]"
published: 2025-09-04
created: 2026-02-18
description: I’ve worked at the intersection of Site Reliability Engineering and Program Management for over a decade. One of the biggest “Aha!” moments I had in my career was realizing that the foundational principles and practices of SRE apply to situations far beyond large-scale distributed software systems. This realization led me to develop the “How to… Read More »How to SRE Anything.
tags:
  - clippings
  - sre
  - googlecloud
  - site-reliability-engineering
---
I’ve worked at the intersection of [Site Reliability Engineering](http://sre.google/) and Program Management for over a decade. One of the biggest “Aha!” moments I had in my career was realizing that the foundational principles and practices of SRE apply to situations far beyond large-scale distributed software systems.

This realization led me to develop the “How to SRE Anything” framework, a pragmatic approach to applying Site Reliability Engineering principles to a wide range of domains including:

- designing training programs
- running a restaurant
- optimizing customer service

or even building a family emergency plan. This practical framework can help tackle any challenge in work or in life more effectively.

![A watercolor illustration in a landscape format showing a seven-layer pyramid. To the left of the pyramid are a notebook, a pen, a mortar board, a first aid kit, and a stethoscope. To the right are a chef's hat, plates, cutlery, a headset, a juggling pin, and a party horn.](https://www.reliablepgm.com/wp-content/uploads/2025/09/how-to-sre-anything-hero-image-1-1024x535.jpg)

AI-Generated Image by Gemini representing How to SRE Anything

## Site Reliability Engineering (SRE) Fundamentals

For those new to the concept, SRE was born at Google in 2003. At its heart, SRE focuses on keeping production infrastructure and critical services up and running 24/7, 365 days a year. A key tenet is that **reliability is a foundational feature of any product**. If a service isn’t available to its users, all its other features don’t matter.

### Key SRE Principles and Patterns

Over the years, a number of core SRE principles and cultural tenets have emerged. These include:

- Users should never notice an outage before you do; robust monitoring is a must.
- Engineer solutions to eliminate classes of errors, rather than being satisfied with just point fixes. SREs aim for systemic improvements.
- Don’t feed the machines with human effort by actively working to vanquish toil through automation.
- Failure is an opportunity to improve, not to brandish pitchforks. This is central to fostering a blameless postmortem culture, where learning and transparency are prioritized over finger-pointing.

### SRE is About Balance

It’s crucial to understand that SRE isn’t about achieving 100% perfection, which is an impossible goal. Instead, it’s about finding the appropriate level of reliability and balancing competing concerns such as reliability, engineering time, development velocity, and cost in a way that keeps your users happy.

## The How to SRE Anything Framework

My How to SRE Anything framework provides a clear structure for tackling any challenge with a reliability mindset. To begin, you need to define 3 things:

- **$TheDomain:** This is the specific area or context of your project. It could be anything from a business operation like a customer service function to something that is important on a personal level like a family emergency preparedness plan.
- **$TheThing:** This defines the **what**. What is it that you are trying to do or build?
- **$MeansToGetThere:** This is the **how**. How will you achieve $TheThing and turn it into a well-oiled machine. It involves defining the tactical steps you need to take to deliver $TheThing.

### Valuing the What and the How

When you are starting something new, it’s easy to focus on the **what**, but there is an equally important dimension to consider: the **how**. To illustrate, consider the software development lifecycle. The **what** is your shiny product features. The **how** is about reliably deploying those features to production to meet user needs. In the same vein, any project, regardless of its domain, needs to clearly define both the **what** and the **how** (Table 1).

#### Table 1. The What and the How for Different Domains

| Domain | “What” ($TheThing) | “How” ($TheMeansToGetThere) |
| --- | --- | --- |
| **Software Development** | Product Features | Deploying to production in a reliable way to meet the needs of our users |
| **Training Programs** | Training Content | Deploying a consistent and reliable training program that meets the needs of our students |
| **Running a Restaurant** | The Menu | Taking orders, delivering food, and accepting payments in a timely manner to keep our diners happy |
| **Customer Service Function** | Customer Experience | Solving (or better yet, preventing!) issues in a timely manner to keep our customers satisfied |

### Applying the Service Reliability Hierarchy to SRE Anything

The **Service Reliability Hierarchy**, included in the [first edition of the SRE Book](http://sre.google/books), is typically visualized as a pyramid (Figure 1). It covers elements necessary to make a service reliable from most foundational at the bottom to most advanced at the top. The beauty is that this hierarchy can be adapted to **any** context you can think of.

![a watercolor pyramid with 7 levels. The word “Product” is overlaid on the top tier of the pyramid. Level 6 says “Development” Level 5 says “Capacity Planning” Level 4 says “Testing & Release” Level 3 says “Postmortem / Incident Analysis” Level 2 says “Incident Response” Level 1 says “Monitoring”](https://www.reliablepgm.com/wp-content/uploads/2025/09/service-reliability-hierarchy-sre-1024x1024.jpeg)

a watercolor pyramid with 7 levels. The word “Product” is overlaid on the top tier of the pyramid. Level 6 says “Development” Level 5 says “Capacity Planning” Level 4 says “Testing & Release” Level 3 says “Postmortem / Incident Analysis” Level 2 says “Incident Response” Level 1 says “Monitoring”

![A watercolor pyramid with 7 levels. The word “Well-Oiled Machine” is overlaid on the top tier of the pyramid. Level 6 says “$TheThing” Level 5 says “How will you scale?” Level 4 says “How can you pilot?” Level 3 says “How will you learn from failure?” Level 2 says “What will you do when things go wrong?” Level 1 says “What can you observe?”](https://www.reliablepgm.com/wp-content/uploads/2025/09/how-to-sre-anything-pyramid.jpeg)

A watercolor pyramid with 7 levels. The word “Well-Oiled Machine” is overlaid on the top tier of the pyramid. Level 6 says “$TheThing” Level 5 says “How will you scale?” Level 4 says “How can you pilot?” Level 3 says “How will you learn from failure?” Level 2 says “What will you do when things go wrong?” Level 1 says “What can you observe?”

AI-Generated Images by Gemini

#### Figure 1. The Service Reliability Hierarchy generalized to any domain

Let’s explore how we can adapt this hierarchy to your chosen domain. We can divide the service reliability hierarchy into two parts:

**1\. Your Aspiration:** These elements at the top of the pyramid define your ultimate goals and how you’ll recognize sustained success (across both the **what** and the **how**).

- **$TheThing:** What you are trying to build.
- **Well-Oiled Machine:** Envision your project fully actualized, reliable, and sustainable.

**2\. Tactics:** These are the actionable steps you’ll take that you believe are necessary to achieve your aspiration. You can define the tactics that make sense for your domain by asking a series of questions that correspond to different levels of the pyramid.

1. **What can you observe? (Monitoring)**: You can’t improve what you don’t measure.
2. **What do you do when things go wrong? (Incident Response)**: Define a clear plan for addressing issues that arise.
3. **How will you learn from failure? (Postmortem / Incident Analysis)**: Embrace failure as an opportunity to improve.
4. **How can you pilot? (Testing & Release)**: Implement progressive rollouts and pilots at small scales (i.e., lower risk) before wider deployment.
5. **How will you scale? (Capacity Planning)**: Minimize toil through automation to free up your limited human cycles, allowing you to scale operations super-linearly to the size of your team.

## How to SRE Anything in Practice

I’ve found these principles to be incredibly versatile both on the job and in life in general.

### Work Examples of How to SRE Anything

My day job for many years was teaching the SREs at Google the key principles and practices of Site Reliability Engineering. So, we decided to get meta and apply those same principles and practices *to the training program itself.*

I’ve talked in detail about how to SRE a training program in my keynote at DevOpsDays Zurich (and at other conferences too).

![](https://www.youtube.com/watch?v=GUSUEN0al5g)

Now let’s go through a couple of additional hypothetical business examples:

- Running a Restaurant (Table 2)
- Customer Service (Table 3)

#### Table 2. How to Apply SRE Principles to Running a Restaurant

| Aspirations |  |
| --- | --- |
| Well-Oiled Machine | Restaurant receives rave reviews on Google Maps & via Social Media influencers. Investors approach about opening a 2nd location. Staff turnover less than industry benchmark |
| $TheThing | Brunch and dinner service consistently booked to capacity 7 days a week! |

| Tactics |  |
| --- | --- |
| How will you scale? | Ensure no single points of failure. Minimize toil! e.g., invest in self-serve ordering technology. Table-side QR codes. |
| How can you pilot? | Conduct experiments in one section of the restaurant. e.g., Overbook reservations relative to tables based on historic no-show data |
| How will you learn from it? | Test the actions and share the results with all staff |
| What do you do when things go wrong? | Analyze bad reviews as a team weekly. Identify hypotheses on how to address & 3 actions to test |
| What can you observe? | Staffing roster. wait times for tables/food customer reviews. Social media mentions. |

#### Table 3: How to Apply SRE Principles to Customer Service

| Aspirations |  |
| --- | --- |
| Well-Oiled Machine | AI delivering front line support. Customer experience reps have time to proactively identify opportunities for the customer to grow. |
| $TheThing | Customer CSAT above 90%. Call volume trending down. NPS rising. Social media sentiment positive. |

| Tactics |  |
| --- | --- |
| How will you scale? | Test automation and AI enhancements. |
| How can you pilot? | Set up a pilot template and process for sign-off. |
| How will you learn from it? | Hold per market weekly Ops Reviews. Bubble up insights in monthly all team mtg. Feed to product team via their ticket system. |
| What do you do when things go wrong? | Page additional customer experience reps if support volume spikes. |
| What can you observe? | email, call, chat volume. Staffing levels, CSAT, NPS |

### Life Examples of How to SRE Anything

Now let’s consider an example far removed from the workplace. This is one that I can talk about [based on my personal experience](https://www.linkedin.com/pulse/site-reliability-engineering-best-practices-applied-medical-petoff/).

The domain we are tackling is a family emergency plan (Table 4). $TheThing we are trying to achieve is: Reliable support is available to your loved one when needed. Information flows appropriately and in a timely manner.

What does our well-oiled machine look like? Family members and friends are seamlessly working together to take care of your loved one when you can’t be there yourself.

#### Table 4. How to SRE a Family Emergency Plan

| Aspirations |  |
| --- | --- |
| Well-Oiled Machine | Family members and friends are seamlessly working together to take care of your loved one. |
| $TheThing | Reliable support is available to your loved one when needed. Information flows appropriately and in a timely manner. |

| Tactics |  |
| --- | --- |
| How will you scale? | Understand who can support you |
| How can you pilot? | Get and test access to medical information. |
| How will you learn from it? | Complete a retrospective based on DiRT tests. Ensure documentation is up to date. |
| What do you do when things go wrong? | Be clear who is oncall and who can support you (avoid SPoFs) Detailed playbooks, DiRT Tests |
| What can you observe? | Set-up a Lifeline. Have friends with line of sight |

Let’s dive deeper into our tactics.

#### What can we observe?

For loved ones who live alone, a Lifeline is a great form of monitoring. It’s a small device that your loved one can wear around their neck with a button that they can press to call for help in an emergency. The Lifeline will also trigger if your loved one falls down.

Just like with a production incident, when you lower time to detect (TTD) you often achieve a better, faster resolution.

Also, make friends with their friends so that you have people with line of sight when you can’t be there yourself.

#### What will we do when things go wrong?

Be clear who is oncall and who can support you (avoid SPoFs–single points of failure). Make sure that your loved one has specified emergency contacts locally (or at least in country). Just like with a production incident, there is no expectation that you have to do this alone. Escalate!

Understand which family members and friends you can call upon to support you in taking action to support your loved one and in decision-making. In addition to friends and family, there are likely community resources that you can avail of.

Create a detailed playbook. Ideally, this will be in the form of a healthcare proxy written by your loved one with detailed descriptions of what your loved one would/would not want doctors to do if they can’t speak for themselves.

DiRT test your family emergency plans. Just like with production systems, disaster recovery testing is critical to stress test your family emergency plans before you need them. Do a [Wheel of Misfortune](https://github.com/dastergon/wheel-of-misfortune) exercise.

You don’t want to find out that you’ve missed a key element or point of access in a crisis. Think through what might go wrong (with your loved one if they are willing) and discuss what you’d do in that situation (or what they’d want you to do).

#### How will you learn from things that go wrong?

Do a retrospective based on your DiRT test / Wheel of Misfortune exercise and take action to ensure that your documentation is up to date and that you’ll be able to help your loved one through a healthcare emergency and carry out their final wishes when the time comes.

#### Think about what you can pilot?

Get and test access. A crisis is not a great time to learn that you can’t get access to medical information. Make sure your loved one has signed a HIPAA release giving permission for doctors to release their healthcare information to you and to discuss their health and treatment options. This is also necessary to get access to insurance information/claims. You’ll likely need to get them to sign a HIPAA release for each medical provider.

#### How will you scale?

We talked about this already, but knowing you are not in it alone and that there are people who can help is key to scaling what you do to support your loved one.

## SRE Anything With AI Assistance

In the above examples as with any new challenge you might be facing you’ll want to think about and brainstorm about defining your $TheThing and what it means to be a well-oiled machine.

From here, there is no single answer on how to get there. There are many tactics you might consider. Having a partner to brainstorm with can be helpful for speccing out the full range of possibilities effectively.

To that end, I was able to codify the “How to SRE Anything” framework into an AI agent. I’ve found Gemini Gems to be a fantastic no-code tool for this. I trained a Gem with instructions and context, enabling it to act as an SRE expert to help brainstorm and apply these principles to any domain. The only downside is that Gems are aimed at personal use and they aren’t easy to share. Never fear though, you can set up your own “How to SRE Anything” Gemini Gem by following these steps:

- Navigate to [http://gemini.google.com/](http://gemini.google.com/) with any Google Account.
- In the left sidebar, select “Explore Gems,” then “+ New Gem.”
- Input the detailed prompt (Prompt 1) as instructions and this [Google Doc](https://docs.google.com/document/d/1jzf5n6F-lYn4gOi-O-WvyZBkjqOX5f48W4RCSAjWwJw/edit?tab=t.0) that I created which outlines the principles of the How to SRE Anything framework as knowledge into the appropriate boxes (Figure 2).

#### Prompt 1. Instructions in Markdown to create a “How to SRE Anything” Gemini Gem

```
Purpose and Goals:

* Act as an expert on Site Reliability Engineering (SRE) principles and best practices.  
* Help users apply SRE principles to non-traditional situations or 'SRE Anything'.  
* Brainstorm ideas for what should be included at each level of the 'How to SRE Anything' rubric based on the user's domain. This is the order of operations  
* Define the aspirational elements     
  * $TheThing 
  * The Well Oiled Machine   
* Define the tactics  
  * Monitoring \- what can you observe?  
  * Incident Response \- what do you do when things go wrong?  
  * Postmortems / RCA \- How will you learn from failure?  
  * Testing \- How can you pilot new things?  
  * Capacity Planning \- How will you scale?  
  * Iterate on suggestions with the user based on their feedback.  
* Offer to output the final result in a Google Doc.

Behaviors and Rules:

1) Initial Inquiry:

a) Greet the user with a welcoming message and introduce yourself as an SRE expert.
b) When the user says 'hi', ask them to describe the domain of their program or initiative.
c) Take on the persona of an expert in that domain after they reply.
d) Use your domain expertise to help them 'SRE Anything' for that domain.

2) Applying the Service Reliability Hierarchy:

a) Apply the Service Reliability Hierarchy as a rubric for approaching this new domain one element at a time so that you don't overwhelm the user.
b) Start with "$TheThing": Brainstorm ideas for what should be included at this level of the 'How to SRE Anything' rubric.
c) Present the brainstormed ideas on this element of the rubric to the user in a clear and structured format (number the bullet points for easy reference in the discussion).
d) Ask the user what they think and iterate on those suggestions with the user based on their feedback.
e) When they are satisfied, repeat this process for the next level of the rubric. Do not proceed to the next level of the rubric until you can an explicit acknowledgement from the user that they are satisfied with the results for the current level.
f) Once you have progressed through all the parts of the rubric, offer to output the final collective result in a markdown format that can be copied and pasted into a Google Doc.

Overall Tone:
* Use expert, knowledgeable, and helpful language.  
* Be encouraging and supportive of the user's non-traditional SRE applications.  
* Be flexible and adaptable to the user's feedback and ideas.  
* Be concise and to the point.
```

![Gemini Gem screenshot showing where to input instructions and knowledge.](https://www.reliablepgm.com/wp-content/uploads/2025/09/how-to-sre-anything-gemini-gem-screenshot-1024x802.jpg)

Gemini Gem screenshot showing where to input instructions and knowledge.

#### Figure 2. Screenshot of the Gemini Gems user interface.

Once set up, you can start chatting with your Gem! For example, I used my gem to brainstorm on how to start a clown college! Why a clown college? I like *The Simpsons*

![](https://www.youtube.com/watch?v=_sFDjHAvPko)

How did my “How to SRE Anything” Gem and I get on? You can [read through my entire conversation with the Gem here](https://g.co/gemini/share/2e5109ad64be).

### How to “SRE Anything” for a Clown College

The final output from my Gem was in a nice package that was easy to export to a Google Doc. I’ve included it here as well.

#### Aspiration

- **$TheThing:** Graduating a cohort of highly-skilled clowns who are well-versed in both traditional techniques and modern improvisational comedy.
- **The Well-Oiled Machine:** The clown college is a world-renowned institution with a thriving alumni network, a self-sustaining financial model, and a celebrated faculty who consistently produce the next generation of highly sought-after, award-winning performers.
	- *Supporting Context:*
		1. Your college has a strong, recognizable brand and reputation, with a long waiting list of applicants each year.
		2. The curriculum is continuously updated and refined based on alumni feedback and industry trends.
		3. Your graduates consistently win prestigious awards at comedy festivals and are sought after by top circuses and entertainment companies.
		4. You have a sustainable, recurring revenue model through successful workshops, a touring alumni troupe, or partnerships with theaters.
		5. Your instructors are renowned experts in their fields, are well-compensated, and have a high level of job satisfaction, leading to low turnover.

#### Tactics

- **Monitoring – What can you observe?**
1. **Student Performance and Progress:** Track student grades, practical skill assessments (e.g., how long they can juggle, the complexity of their gags), and class attendance. This helps you monitor the quality of the educational delivery.
2. **Alumni Career Progression:** Actively track the number of professional contracts secured by graduates, their earnings, and any awards or recognition they receive. This is a direct measure of your program’s long-term success.
3. **Satisfaction Feedback:** Conduct regular surveys to measure both student and instructor satisfaction with the curriculum, facilities, and overall college experience. This gives you a direct line of sight into the “health” of your internal community.
4. **Enrollment Funnel Metrics:** Monitor key metrics like the number of applications received, the percentage of applicants who are accepted, and the rate at which accepted students enroll. This tracks the college’s brand appeal and growth.
5. **Instructor Toil and Satisfaction:** Monitor instructor-specific metrics, such as time spent on non-teaching administrative tasks (toil), and use regular one-on-one meetings and surveys to gauge their job satisfaction and morale.
- **Incident Response – What do you do when things go wrong?**
1. **Defining Critical Incidents:** Establish a clear definition of what constitutes a “critical incident” that requires a formal response.
2. **Communication Plan:** Create a standardized communication plan for different types of incidents.
3. **Emergency Response Playbooks:** Develop “playbooks” for common incidents. For example, a “Playbook for an Unexpected Instructor Departure” could include steps for finding a substitute, communicating with students, and updating the curriculum.
4. **“On-Call” Schedule:** Establish a clear “on-call” schedule for key personnel.
5. **Blameless Postmortem Policy:** An incident response plan should always lead to a blameless postmortem to focus on system and process failures.
- **Postmortems / RCA – How will you learn from failure?**
1. **Mandatory and Timely Postmortems:** Conduct a blameless postmortem for any event that impacts your students’ learning, safety, or your college’s reputation within 48 hours.
2. **Blameless Culture:** The postmortem’s goal is to improve processes, not to assign blame to individuals. The focus should be on systemic issues.
3. **Actionable Follow-up:** Every postmortem must generate a list of concrete, tracked action items.
4. **Share the Learnings:** The findings and action items from postmortems should be shared transparently with the entire community.
- **Testing – How can you pilot new things?**
1. **Pilot Programs for New Curriculum with a Success Criteria Template:** Before rolling out a new class, use a formal template to define the pilot’s objectives and the specific success metrics.
2. **Staged Performance Reviews:** Before a final performance, hold a series of staged “dress rehearsals” with a small, private audience.
3. **Peer Review and Shadowing for New Instructors:** When a new instructor is hired, they will shadow a senior instructor and be peer-reviewed by the existing faculty before leading a class.
4. **“Red Team” Exercises for Incident Response:** Periodically, conduct surprise drills to test your incident response plan.
- **Capacity Planning – How will you scale?**
1. **Student and Instructor Burnout Metrics:** Actively monitor for signs of burnout.
2. **Student Enrollment Projections & Load Balancing:** Project student enrollment and then balance the course load across your instructors to prevent any one individual from being over-scheduled.
3. **Resource Inventory & Human Resources:** Maintain a detailed inventory of all your critical resources, including your instructors, with a plan for when to hire more permanent staff or bring in guest lecturers.
4. **Surge Planning with a Human-Centric Lens:** When planning for unexpected surges in demand, plan for the human resources as well, not just physical resources.
5. **Proactive Maintenance of Physical and Mental Well-being:** Schedule not only maintenance for your facilities but also mandatory “recharge weeks” for students and staff.

\*\*\*  
I hope these practical examples of applying Site Reliability Engineering principles and best practices to various domains–both hypothetical and ones I’ve personally put into practice–has inspired you to try to “SRE Anything” for a domain you care about.

Tags: