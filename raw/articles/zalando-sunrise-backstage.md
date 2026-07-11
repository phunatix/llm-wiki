---
title: "Sunrise: Zalando's developer platform based on Backstage"
source: "https://engineering.zalando.com/posts/2023/08/sunrise-zalandos-developer-platform-based-on-backstage.html"
author:
  - "[[Lacey Nagel]]"
published: 2023-08-03
created: 2026-07-07
description: "Lessons learned from adopting Backstage as Developer Platform at Zalando."
tags:
  - "clippings"
---
## Introduction

Since 2021, Zalando invested in building up a developer portal called Sunrise, aimed to become the starting point for Builders at Zalando. The portal is based on Spotify's [Backstage platform](https://github.com/backstage/backstage) with additional extensions built internally. Sunrise enables everyone at Zalando to view and discover information about teams, applications, APIs, events, CI/CD pipelines, Infrastructure accounts and costs, and much more. In this post, we explore how adopting Backstage impacted the daily life of Software Engineers at Zalando and get insights from Lacey and Arthur who led the efforts on the Product and Engineering side.

![Sunrise: application view](https://img01.ztat.net/engineering-blog/posts/2023/08/img/sunrise-application-view.png)

Fig 1. Sunrise: detailed information about applications

### Lacey, what's your role in creating Sunrise?

*Lacey:* Funny story, I actually ran a vision workshop with the team responsible for the Developer Portal at Zalando before I became a member of the department! As the official product manager, I helped solidify the vision with a platform mindset and an experience strategically focused on interoperability and usability. I worked with engineering stakeholders and the engineering manager to devise a strategy and roadmap to give us the best chance at efficient implementation, good adoption, and improved satisfaction from users so that more platform and infra teams would want to contribute. And of course, I'm probably the loudest promoter of our platform's & contributors' solutions 😅

### Arthur, how about you? How are you involved here?

*Arthur:* Hello! I've actually started to be involved with Sunrise as an early adopter and active user first, before moving internally to the team in May 2022. Since then, I've been leading the engineering team, driving the delivery of new features, coordinating support and maintenance on the platform, contributing to the product vision and ensuring our alignment with the organizational strategy, all the while managing our amazing team of 4 software engineers.

### Why did Zalando choose Backstage for its developer portal? Was any similar solution in place before?

*Lacey:* Before Sunrise, we had over 100 disconnected interfaces & resources, plus "the Developer Console" which centralized links to resources mostly for the *Code* through *Deploy* steps of the Developer Journey. After recognizing that we'd need to evolve into a platform to achieve our vision, we considered several options (including building everything ourselves), and Spotify happened to reach out while we were still in the discovery & design phase. What made it a great fit then, was that we had extremely limited resources and skills (both engineering & design) on the team at the time, so we recognized that having an out-of-the-box solution for a design-system and plugins like the basic Software Catalog would be necessary for us to deliver something fast enough to justify the strategic investment & potential risk of failure.

### I hear that our Engineers are really excited about Sunrise. Why and what features are they most excited about?

*Lacey:* From pretty much the beginning, the topic of interoperability has been prevalent as it's what enables us to eliminate friction from the day to day tasks Builders need to perform. Users really celebrated a deeper integration that two contributing teams collaborated on to make the experience of deploying data pipelines more seamless, and features that make org structure and reporting lines more transparent have also had very quick and wide adoption. We also have some very popular Platform features that enable all our users (regardless of whether they actually own services or not) to see personalized content by default and further customize personalization settings. The day to day features that people actually use the most are the action-oriented-easy-access links on the homepage, the CI/CD interface, Search, and the Application catalog, which includes integrations to tooling and resources across the SDLC.

### How do you measure adoption of the platform and along each part of the SDLC?

*Lacey:* Since our vision for Sunrise was to make it the "daily" starting point for Builders, we monitor the share of Builders using the platform on weekdays, and weekly as our primary success metrics for adoption. Since not all features actually need to be used daily (for example, every single person won't be registering a new application every working day), we let contributors determine what makes sense for their integrations and we provide them with a centralized dashboard and support with Analytics to make it easier to understand usage. In the future, we hope to map adoption of features to more tangible improvements in operational performance.

### What features were added on top of Backstage's open-source project?

*Lacey:* That's actually a pretty big question. For our earliest release, we added a personalized homepage with easy-access links to things engineers use often like open PRs and recently deployed pipelines, and added a support overview that they were used to from previous tooling, and our CI/CD platform that is internally built. Since then, we've integrated 27 other tools & services through 30 front-end plugins ranging from our internal [machine learning platform](https://engineering.zalando.com/posts/2022/04/zalando-machine-learning-platform.html), through widgets that make users aware of base image vulnerabilities or delivery performance insights, to a personalized dashboard covering all aspects of critical business events, like Cyber Week. Some of those plugins were contributed back to the open source community, such as the interface for our [API Linter, Zally](https://github.com/zalando/backstage-plugin-api-linter). Our platform features personalization – especially for users who don't own components themselves, but who have some accountability for them – increased adoption amongst [principal engineers](https://engineering.zalando.com/posts/2022/02/principal-engineering-at-zalando.html) and leadership, and has helped contributors to Sunrise provide similar reporting-like features that they never had before with very little effort that in turn drive more regular use within engineering teams.

### Which team operates the platform? Any challenges that you had to overcome to support Zalando's user base?

*Arthur:* Our team is called Builder Portal, and has been operating and evolving the platform since its inception. Our biggest technical challenge at Zalando's scale has been managing the various pre-existing sources of data and determining how to sync them with [Backstage's Catalog](https://backstage.io/docs/features/software-catalog/) system. We currently have over 40k registered entities (between applications, teams, and users) which we sync daily with the respective source of truth services. In terms of adoption, the biggest challenge from the get-go was to make sure that the experience is approachable and consistent for all users, regardless of which part of the development journey they are working on. Builders can be very opinionated in their ways of working, so making sure that our decisions are well thought out and will ultimately support them in working productively and happily can be challenging sometimes, but it's also very rewarding. And hey – we're Builders ourselves too, so we also enjoy using Sunrise while maintaining it.

*Lacey:* A lot of what we see impacting adoption of new features is that people have built habits – and incredibly long bookmark lists – to make up for deficiencies of the fragmented tooling. What turned out to be most impactful for solving this problem is ensuring that we redirect users from old features to the new ones in Sunrise shortly after making them generally available and then *completely shut down* the old tooling.

### Backstage is open-source. How does Zalando and your team approach upstream contributions? Can you name some notable examples?

*Arthur:* Whenever we find some limitation in Backstage in comparison to what we want a feature to look like, we reflect on whether this is something that could impact other adopters of the platform or whether it's a Sunrise-specific problem. If it's the former, we reach out via a GitHub issue (e.g. [bug report](https://github.com/backstage/backstage/issues/17481) and [feature request](https://github.com/backstage/backstage/issues/9805)). If we know how to solve it, we also contribute a pull request (e.g. respective [bugfix](https://github.com/backstage/backstage/pull/17485) and [new feature](https://github.com/backstage/backstage/pull/10041)). We also keep an eye out for opportunities to share in-house plugins with the community. As mentioned by Lacey earlier, last year we open-sourced our [API Linter plugin](https://github.com/zalando/backstage-plugin-api-linter).

![Backstage Plugin: API linter using Zally under the hood](https://img01.ztat.net/engineering-blog/posts/2023/08/img/backstage-plugin-api-linter.png)

Fig 2. Sunrise: open-sourced API linter plugin

### How about the internal features? How easy has it been to get contributions from outside of your team?

*Arthur:* We have at least ten other plugins (the number grows sporadically) owned and maintained by other teams in Zalando, including our own Continuous Delivery and Machine Learning Platform teams. There's always an initial barrier of entry (as with any other application and framework) for contributors to understand the domain-specific language of Backstage, as well as the standards we have implemented on the platform, especially since many platform teams don't have a lot of front-end engineers available to work on the user interface of their plugins. We invest a lot in creating standard components and documenting our patterns so contributors can spend less time figuring out which button to use and more time improving the overall experience for their users.

### You recently reached a major milestone – 2,000 PRs merged to the repository and Sunrise replacing multiple internal tools and the prior generation of the developer portal. What's the next big milestone that you look forward to?

*Lacey:* Creating comprehensive visibility into *everything* running in production and mapping the relationships between entities – automatically where possible – so that we can centrally support global improvements to the operational health of systems and teams. The [SBOM work](https://engineering.zalando.com/posts/2023/04/how-sboms-change-the-dependency-game.html) you mentioned in your recent post is a big part of that, but we are also working on surfacing the relationships between entities like data pipelines and applications, as well as the relationships of applications and their components to business problems through a standardized and semi-automated documentation of Domains. Having that oversight will enable us to shift left not only security and compliance, but also productivity, reliability, and cost efficiency by providing insights about the current balance of operational health in relationship to business metrics relevant to our high-level Domains. It will give Builders easier access to the information they need to involve the right stakeholders and make decisions about what kind of work to invest in and when. To put it shortly: we're all a bit happier, more secure, and more efficient when working with transparency and less uncertainty.

### Any tips that you'd give to teams who are also adopting Backstage as the foundation for their developer portal?

*Lacey:* Haha, the list is long because I've learned a lot over the life of this initiative. I'd sum it up as:

- Having a **clear, inspirational vision** that includes (and delineates) the needs of both users and contributors – and that you *constantly* communicate – will be key for motivating contributors and for reaching the critical mass of user journeys needed for users to feel the benefit of your platform.
- To drive adoption and impact, look for opportunities to **personalize content** to make it easier to recognise and understand, and invest in **increasing the interoperability** along the journeys your users take to complete tasks between both fully integrated interfaces and features, as well as external tooling – and don't forget to shut down old tooling!
- Whether you're using an open source plugin or building something yourself from scratch, **investing in great UX research and design is *critical*** for building an experience that will remain cohesive as it grows – that's important so that your users are enabled to actually find the things you build, and are happy to use them.

*Arthur:* My tip is to **leverage the power of open source**! The Backstage Community is ever-growing and provides a lot of interesting, well-maintained plugins for you to make use of, so don't shy away from engaging with it. The framework itself is also constantly evolving and growing its scope, and with some big adopters already leveraging it (including us!), you're sure to see a lot of examples of interesting use cases that will support your teams to be more productive.

*Bartosz:* Thanks for the conversation and for walking us through our approach to buliding a Developer Platform!

---

*If you would like to know more about Sunrise, check out Henning's talk [Cloud native developer experience at Zalando](https://youtu.be/4EGTa8u-7Ws?t=479) or the [related post](https://platformengineering.org/talks-library/sunrise-zalandos-internal-developer-platform).*

---

*We're hiring! Looking for a new leadership challenge? Consider joining our [Leadership](https://jobs.zalando.com/en/jobs?category=Software+Engineering+-+Leadership&utm_source=eng_blog&utm_content=sunrise-zalandos-developer-pla) team!*