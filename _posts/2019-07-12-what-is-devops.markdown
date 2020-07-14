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

### Microservices
It is a type of architecture used to build an application or a set of services. The application is based on a smaller set of services that communicates with each others through, for example, HTTP APIs. Each microservice has its own responsibility and the application is broken down into microservices according to the needs of the application domain. Frameworks or programming languages can be used to write microservices and distribute them, either individually or as a group of services. With this approach, our application will have the following benefits:
* more easily maintainable. I only touch the microservice I need.
* more resilient to errors. If a microservice fails, the rest of the microservices will continue to work since they are independent
* better testable and more modular. You can use different languages and technologies on each microservice, using the most suitable ones case by case without committing to a single technology for the whole project. Each microservice can then be tested with separate approaches and methodologies.

Microservices have gradually become the standard for building systems that make use of practices such as Continuous Deployment.

### Infrastructure as Code
It consists in managing the cloud infrastructure through software development methodologies, such as version control and continuous integration. The cloud can be setup via API, allowing developers and administrators to interact with the infrastructure in a programmatic way and on a very large scale rather than through manual setting and configuration of resources. Since everything can be managed by code, the infrastructure and servers can be deployed as quickly as possible via standardized templates, updated with patches or duplicated iteratively. There are several tools to implement this: Chef, Puppet, Terraform, Ansible, etc. The advantages are remarkable, in addition to those above we have zero downtime (if applied well) and auto-scaling of resources.

### Monitoring and Logging
Keeping parameters and logs under check is useful to find out how application and infrastructure performance affects the end-user experience. Data and logs generated by applications and infrastructure are acquired; after categorizing and analyzing them, the possible causes of problems or unforeseen changes can be thoroughly examined. Creating alarms or analyzing data in real time also help in proactively monitoring services. One of the tools to implement this practice is Nagios.

### Containerization & Orchestration
These are two techniques used to manage software. Containererization, through tools such as Docker, provides a logical packaging mechanism that allows applications to be abstracted from the underlying environment they run on. Decoupling things like this allows for easy and consistent deployments of container-based applications, whether the target environment is a private data center, the public cloud or a developer's computer. Compared to virtual machines, containers have several advantages such as reduced disk size and low overhead. Orchestration refers to practices such as automatic deployment, scaling, and management of containerized applications and can be achieved using tools such as Kubernetes.

## What are the advantages of the DevOps model?
* Speed. Applications developed using a microservice architecture with the addition of continuous integration allow to release updates more frequently and better control services.

* Rapid delivery. Practices such as continuous integration (CI) and continuous delivery (CD) lead to faster releases and bug fixes.

* Reliability. Thanks to CI/CD and monitoring/logging rest assured that releases will meet quality standards without sacrificing the end-user experience.

* Scalability. Infrastructure as code allows you to manage development, testing and production environments in an iterative and more efficient way - on any scale.

* An evolution of software architecture, development and delivery that is not the same as it was twenty years ago.

## A simple pipeline example

Now that we know about DevOps and its advantages, let's briefly look at a simple pipeline example. There is no correct or definitive structure: you can modify the pipeline to better adapt it to certain situations or as you see fit. This is just an example.

In the first step you version the code, with a tool like Git. Developers then develop and commit the code to a repository.

The second step is not always necessary, it depends on the language and technology used. It consists of building the project, which often means having a working version of the project locally.

The third step is running unit tests on the project. This can also be automated - useful to prepare for the next step.

The fourth step is deployment to development/staging environments. At this point you can view the code running on an environment that can be shared with the client. This point can also be automated.

Subsequently, other tests can be run on the development environment. Other people responsible for testing the project can come into play by running their test tasks, even manually, on a development environment that should be complete and working. Depending on requirements, this step can also be automated.

If all goes well it's time to go live! Deployment in production happens. Once this is done there is the operational/monitoring phase. Things such as applications, state of the infrastructure, errors, logs and more are kept under control.

## Final Thoughts
Hopefully by now you have an idea of what DevOps is, at least on paper. DevOps, as I repeatedly stated, is first and foremost a cultural change that impacts all the figures involved in software development. In fact, it requires a different, more modern approach to software development and distribution; in return, if implemented well, it provides us with several advantages such as the reduction of different problems and timescales. It also prepares us to better face challenges that previously would have been more problematic to manage.