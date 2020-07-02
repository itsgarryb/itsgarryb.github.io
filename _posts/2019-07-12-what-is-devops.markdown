---
layout: single
title:  "What exactly is the DevOps model and what advantages does it bring to your workflow?"
date:   2020-08-01 09:00:00 -0800
categories: [DevOps]
permalink: /what-is-devops
classes: wide
---
It's 2020 and although DevOps is a practice that's very commonly adopted today, I feel that a not too overly technical explanation of the subject might be beneficial to those individuals, or companies, that are not using it yet but find themselves in a position where it makes sense to use such model. Moreover, if you're completely or partially new to this subject, this is a great place to start!

<figure>
  <img src="{{site.url}}/assets/images/2020-08-01/devops.gif" alt="DevOps"/>
</figure>

## So what is this DevOps thing?

DevOps can be defined as a combination between cultural philosophies, practices and tools.

The **cultural philosophy** aspect is about changing how you develop and deploy software. In the DevOps model people who take care of software development and people who take care of operations (by managing, monitoring and operating infrastructure) work very closely together; sometimes the two roles are combined together. The DevOps term originates exactly from here: **Dev**eloper **Op**eration**s**.

Next, there are **practices**. They help you to understand how the DevOps model works, in practice. Don't worry if you have no idea what these are, more on them in just a moment:
* Continuous Integration
* Continuous Delivery
* Microservices
* Infrastructure as Code
* Monitoring and Logging
* Containerization & Orchestration

Finally, **tools**. These, along with the aforementioned practices, will help you to concretely adopt the DevOps model. Some of the relevant tools are:
* Git
* Jenkins
* Docker
* Kubernetes
* Automated testing libraries/frameworks

The DevOps model will improve every aspect of the lifecycle of an application, from development and testing to deployments and production rollouts. The team relies on automation to speed up manual processes and, thanks to the appropriate tools, applications can grow in a rapid and flexible way.

**DevOps is first of all a mentality shift**, where you are required to change the way you approach software development and release. While it is good to have one person to be the leader of this change, you should make sure that your whole team/company is ready to take the leap.

## Let's dive deeper into the practices

### Continuous Integration
It is composed by two main elements: a cultural one and a technical/automated one. The cultural part consists in learning how to make frequent integrations. In other words, developers should not wait an excessive amount of time before merging their commits into the rest of the project. The technical/automated part is represented by the tools that helps automating these frequent integrations. Jenkins, for example, is a popular open source tool widely used for this. Continuous Integration solves the problem of heavy integrations and it helps reducing time spent solving merge conflicts. Statistically, the longer you wait to merge the more chances you will incur in a conflict. Merge often to avoid this!

### Continuous Delivery / Deployment
It extends Continous Integration by automating deployments to staging and production environments. These deployments can have pre-requisites such as automated tests; they can even go beyond Unit Tests and require interface tests, load tests, integration tests, API reliability tests and so on. There is a difference between Continuous Delivery and Continuous Deployment. With C. Delivery you will automatically deploy on a staging environment and manual approval will be required if you want to deploy in production. With C. Deployment you go one step further and also automate production rollouts. You can use Jenkins for this or you can search for more specific tools that will hook into the Continuous Integration offered by Jenkins. This practice will help you reduce human errors and time required to complete the deployment process.