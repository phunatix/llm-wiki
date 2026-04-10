---
title: The rise and future of Kubernetes and open source at Google | Google Cloud Blog
source: https://cloud.google.com/blog/products/containers-kubernetes/the-rise-and-future-of-kubernetes-and-open-source-at-google?utm_campaign=607ecada7fbea40001636078&utm_content=61afb3dcfdaaab00017b1544&utm_medium=smarpshare&utm_source=linkedin&hl=en
author:
  - "[[Stephanie Wong]]"
published: 2021-12-08
created: 2026-03-21
description: Find out what the last decade of building cloud computing at Google was like, including the rise of Kubernetes and importance of open source security.
tags:
  - clippings
  - gke
  - kubernetes
---
Containers & Kubernetes

## The past, present, and future of Kubernetes with Eric Brewer

December 8, 2021

##### Stephanie Wong

Head of Developer Skills & Community, Google Cloud

##### Try Google Cloud

Start building on Google Cloud with $300 in free credits and 20+ always free products.

[Free trial](https://cloud.google.com/free)

In 2014, the first echos of the word Kubernetes in tech were heard throughout the industry. Back then, the first thing that usually came to mind was “How do you even pronounce it?” Fast forward seven years and it’s become one of the largest open source projects in the world. One of the early stewards of Kubernetes was Google Fellow Eric Brewer. For over a decade, Eric has taken a driver’s seat in advocating for, building, and externalizing technologies at Google. Though he now focuses on a broad set of Google Cloud services—think Kubernetes, serverless, DevOps, [Istio](https://istio.io/), and services—he previously led groundbreaking efforts to separate storage from compute, drive the use of VM live migration at scale, and shape the use of appliances for disaggregation. I had the chance to sit down with him over a series of sessions to learn from his years of experience and dig into the four Kubernetes and open source insights that Eric says have defined the future of cloud computing.

### 1\. Kubernetes became central to cloud native computing because it was open sourced, and we must continue to invest in open source technologies.

![](https://www.youtube.com/watch?v=vi)

![](https://www.youtube.com/watch?v=U-bR1kRldYY)

When Eric joined the UC Berkeley faculty, he focused on what later became cloud computing - a model based on clusters of commodity servers that use many processes, services, and APIs. Once he came to Google in 2011, he brought this view over to develop a new kind of cloud that centered on a higher level of abstraction. This meshed well with the early prototypes that led to [Kubernetes](https://kubernetes.io/), an open-source system for automating deployment, scaling, and management of containerized applications.

While cloud was still forming in the early 2010s, Eric knew that Google’s internal container-based approach would lead to a more powerful cloud than just VMs and disks. Though it was relatively easy to attract a group of supporters at Google, widespread industry adoption is often slower for novel and unproven ideas. With that foresight, Eric knew right away that open sourcing the project would be the only viable way to achieve the potential he knew Kubernetes held to revolutionize cloud computing.

Of course, he faced some resistance. By 2012, Google Cloud already had App Engine and VMs available. The common question from critics was, “Why do we need a third way to do computing?” Well, Google was already running billions of containers per week prior to the emergence of Kubernetes, and Eric saw massive value in further developing the technology for the rest of the industry. Kubernetes’ automation and flexibility makes it much easier to operate compared to raw VMs or raw disks.

After years of open source support, Kubernetes has become the de facto way to run applications in the cloud, with more and more opinionated and vertically oriented services that run on top of it, like [Knative](https://knative.dev/docs/) and [Kubeflow](https://www.kubeflow.org/). The project is still maturing, even as we now face another pivotal shift in cloud computing. Eric is currently spearheading efforts to combine the philosophy that underpins Kubernetes with the strict protection needed by security-sensitive industries. His focus is on open source and software supply chain security, with a goal of creating more opinionated tooling from source code to deployment in order to minimize attack points.

### 2\. As the number of dependencies used in software development grows, the security risks multiply. Investing in software supply chain security is imperative, and a move towards managed services is actually safer than self-managed solutions.

![](https://www.youtube.com/watch?v=vi)

![](https://www.youtube.com/watch?v=_yM7LCcQZGw)

Recent attacks, like those on [SolarWinds](https://www.solarwinds.com/sa-overview/securityadvisory) and [CodeCov](https://about.codecov.io/security-update/), have shown that increasing reuse and development velocity across the software industry has created more openings for attacks. Eric is laying the groundwork to address a challenge that he believes should be a P0 for the entire planet.

#### 99% of our vulnerabilities are not in the code you write in your application. They’re in a very deep tree of dependencies, some of which you may know about, some of which you may not know about.

Eric Brewer

[Tweet this quote](https://x.com/intent/tweet?text=99%25%20of%20our%20vulnerabilities%20are%20not%20in%20the%20code%20you%20write%20in%20your%20application.%20They%E2%80%99re%20in%20a%20very%20deep%20tree%20of%20dependencies%2C%20some%20of%20which%20you%20may%20know%20about%2C%20some%20of%20which%20you%20may%20not%20know%20about.%20-%20Eric%20Brewer%20-%20https%3A%2F%2Fcloud.google.com%2Fblog%2Fproducts%2Fcontainers-kubernetes%2Fthe-rise-and-future-of-kubernetes-and-open-source-at-google)

Because of the growing use of open source software and dependencies in software development, it’s critical for organizations to understand what pieces of software they want to bet on and why. Instead of including unvetted software dependencies in code, organizations must take time to evaluate this software and identify the elements that are either not quite up to par or poorly maintained.

When asked about how Google is investing in Kubernetes (which has several hundred software dependencies), Eric explained that Google Cloud helped form the [Cloud Native Computing Foundation](https://www.cncf.io/) (CNCF) in 2015 to serve as the vendor-neutral home for many of the fastest-growing open source projects, including Kubernetes, [Prometheus](https://prometheus.io/), and [Envoy](https://www.envoyproxy.io/). The foundation’s mission is to make cloud native computing ubiquitous and foster the growth of the ecosystem. Under the auspices of the CNCF, Google has made [over 680,000 additional contributions](https://cloud.google.com/blog/products/containers-kubernetes/building-the-future-with-google-kubernetes-engine) to the project, including over 123,000 contributions in 2020.

Google has a long history of committing to open source. In fact, Google recently [committed another $100M](https://blog.google/technology/safety-security/why-were-committing-10-billion-to-advance-cybersecurity/) to third-party foundations supporting open source security. In addition, Eric helped found the [Open Source Security Foundation](https://openssf.org/) (OpenSSF), which focuses on open source security tooling and best practices so that those responsible for their organization’s security are able to understand and verify the security of open source dependency chains. Eric sees this work as absolutely essential in order to set a precedent. Though it will require lots of largely mundane work to get open source to be as secure as possible, this work is necessary and requires financial support.

#### Open source is a public infrastructure also. And like all public infrastructures, it needs maintenance and support.

Eric Brewer

[Tweet this quote](https://x.com/intent/tweet?text=Open%20source%20is%20a%20public%20infrastructure%20also.%20And%20like%20all%20public%20infrastructures%2C%20it%20needs%20maintenance%20and%20support.%20-%20Eric%20Brewer%20-%20https%3A%2F%2Fcloud.google.com%2Fblog%2Fproducts%2Fcontainers-kubernetes%2Fthe-rise-and-future-of-kubernetes-and-open-source-at-google)

As services continue to move to higher levels of abstraction, managed services set a robust foundation for secure software delivery. Managed services allow providers to enable automatic security preventative controls and attestations. [GKE Autopilot](https://cloud.google.com/blog/products/containers-kubernetes/introducing-gke-autopilot), for example, provisions and manages the cluster's underlying infrastructure, including nodes and node pools, giving you an optimized cluster with a hands-off experience. It follows Google Kubernetes Engine (GKE) best practices and recommendations for cluster and workload set up and security, while also enforcing settings that provide enhanced isolation for your containers. In Eric’s view, this model will continue as a dominant trend moving forward: Providers will manage more features (like security) over time, taking responsibility for features that you don’t want to manage yourself while making the most of the proven protocols and best practices they have built up over years.

### 3\. Platform operators should run GKE as a general purpose platform while imposing guidelines the enterprise cares about.

![](https://www.youtube.com/watch?v=vi)

![](https://www.youtube.com/watch?v=za4IEHPfdTM)

A common question Eric has gotten over the years is how an enterprise should use a managed Kubernetes platform, like GKE. The first thing to remember is that a cloud provider offers more levers, options, and features to tinker with than you really want your developers to use. These levers, however, give platform owners the ability to create secure and maintainable platforms to power their modern apps. For example, it’s wise to apply backups by default and policies to prevent root file system access or creation of public IPs for backend systems. If you're processing credit card transactions, you don’t want to give your internal developers free rein; instead you want to give them a platform where the transactions they execute are guaranteed by the structure of services to be compliant with the regulations where you operate.

Think of Kubernetes as the way to build customized platforms that enforce rules your enterprise cares about through controls over project creation, the nodes you use, and libraries and repositories you pull from. Background controls are not typically managed by app developers, rather they provide developers with a governed and secure framework to operate within.

Managed services often provide or support automated policy controls and best practices that platform operators can easily leverage. [Anthos Service Mesh](https://cloud.google.com/anthos/service-mesh), for example, helps control traffic flows and API calls between services. With the ability to automatically and declaratively secure your services, your developers benefit from more productivity, and the organization benefits from the delivery of more features faster. At the same time, you are protected from shipping features that go against company policies or government regulations.

Google Cloud supports [buildpacks](https://cloud.google.com/blog/products/containers-kubernetes/google-cloud-now-supports-buildpacks) —an open-source technology that makes it fast and easy for you to create secure, production-ready container images from source code and without a Dockerfile. [Artifact Registry](https://cloud.google.com/artifact-registry) lets you set up secure private-build artifact storage on Google Cloud so you can maintain control over who can access, view, or download artifacts. [Container Analysis](https://cloud.google.com/container-registry/docs/container-analysis) provides vulnerability scanning on images in Artifact Registry and Container Registry.

### 4\. Kubernetes will continue to expand to the edge, leverage coprocessors, and run effectively across public and private clouds.

![](https://www.youtube.com/watch?v=vi)

![](https://www.youtube.com/watch?v=BLJdoknCIP4)

In our final episode of the series, we collected questions from the field where a few themes emerged, including Kubernetes at the edge, Kubernetes on coprocessors, and finding the right balance between public and private clouds.

### Kubernetes at the edge

We’re already seeing the potential of Kubernetes being realized at the edge. For example, Kubernetes is being used at the edge in telecommunications and retail spaces. In response to edge security as a concern, Eric explained that Kubernetes can be effectively secured, but it comes down to the full stack. Security can be strengthened through securing hardware through the root of trust, all the way up the stack running on it.

This is an area Google Cloud continues to invest in. At Next 2021, we announced [Google Distributed Cloud](https://cloud.google.com/blog/topics/hybrid-cloud/announcing-google-distributed-cloud-edge-and-hosted), a portfolio of fully managed hardware and software solutions that extends Google Cloud’s infrastructure and services to the edge. It's enabled by [Anthos](https://cloud.google.com/anthos), which GKE is a major component of, and is ideal for local data processing, edge computing, on-premises modernization, and meeting requirements for sovereignty, strict data security, and privacy. To use Kubernetes at the edge securely, Distributed Cloud provides centralized configuration and control over clusters at Google’s edge network, the operator edge (5G and LTE services offered by our communication service provider partners), or your own edge like retail stores, factory floors, or branch offices.

### Kubernetes running on coprocessors

We are also partnering with [NVIDIA](https://www.nvidia.com/) to deliver GPU-accelerated computing and networking solutions for running Anthos at the edge. This speaks to the potential of coprocessors for Kubernetes. Eric believes that coprocessors are an important part of the computing future. We’re reaching the end of [Moore’s Law](https://en.wikipedia.org/wiki/Moore%27s_law), and to make up for it, the industry is adopting domain-specific hardware accelerated for use cases like graphics processing (with GPUs) or machine learning (with TPUs).

### The right balance between public vs. private clouds

Even with all this rapid innovation, companies still face difficult questions in balancing operating in the public cloud versus private sovereign clouds. Eric lays out clear reasons why a public cloud can offer more advantages:

#### You'd be better off with an open public cloud pretty much all the time if you can use one, because it will have better cost efficiency. It will have a higher rate of innovation. It can do more things over time.

Eric Brewer

[Tweet this quote](https://x.com/intent/tweet?text=You%27d%20be%20better%20off%20with%20an%20open%20public%20cloud%20pretty%20much%20all%20the%20time%20if%20you%20can%20use%20one%2C%20because%20it%20will%20have%20better%20cost%20efficiency.%20It%20will%20have%20a%20higher%20rate%20of%20innovation.%20It%20can%20do%20more%20things%20over%20time.%20-%20Eric%20Brewer%20-%20https%3A%2F%2Fcloud.google.com%2Fblog%2Fproducts%2Fcontainers-kubernetes%2Fthe-rise-and-future-of-kubernetes-and-open-source-at-google)

That being said, using a public cloud provider means you must trust your cloud provider and the government in which your provider is based (today, this is usually the US). If you don’t trust those or think they are too risky, you may want to run in your own country, on a private, sovereign cloud. The great thing is that Kubernetes is well-suited to run on a private cloud. Anthos (which Eric helped build) lets you run Kubernetes on GKE for hybrid and multicloud environments, and [on bare metal](https://cloud.google.com/anthos/clusters/docs/bare-metal/1.6/concepts/about-bare-metal). For those worried about vendor lock in, you can move off of Anthos and continue to run your applications on Kubernetes on-premises.

To hear more about Eric’s predictions on the next externalized product from Google Cloud and what the future of cloud computing looks like, check out the videos above. You can stay up-to-date with Eric’s research at Google by following him on Twitter [@eric\_brewer](https://twitter.com/eric_brewer).

And, you can stay up-to-date with my latest content at [@stephr\_wong](https://twitter.com/stephr_wong).[Containers & Kubernetes](https://cloud.google.com/blog/products/containers-kubernetes/building-the-future-with-google-kubernetes-engine)

##### Build your future with GKE

For an idea of where we’re going with Google Kubernetes Engine, take a look at where we’ve been.

By Pali Bhat • 4-minute read

![https://storage.googleapis.com/gweb-cloudblog-publish/images/07_-_Containers__Kubernetes_iY4YTLa.max-900x900.jpg](https://storage.googleapis.com/gweb-cloudblog-publish/images/07_-_Containers__Kubernetes_iY4YTLa.max-900x900.jpg)

[View original](https://cloud.google.com/blog/products/containers-kubernetes/building-the-future-with-google-kubernetes-engine)