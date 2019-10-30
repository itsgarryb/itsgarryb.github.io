---
layout: single
title:  "What exactly is the DevOps model and what advantages does it bring to your workflow?"
date:   2019-02-18 09:00:00 -0800
categories: [DevOps]
permalink: /what-is-devops
classes: wide
---
Although DevOps is a practice that's very commonly adopted today, I feel that a not too overly technical explanation of the subject might be beneficial to those individuals, or companies, that are not using it yet but find themselves in a position where it makes sense to use such model. Moreover, if you're completely or partially new to this subject, this is a great place to start!

<figure>
  <img src="{{site.url}}/assets/images/2018-03-01/github_jekyll.png" alt="Jekyll and GitHub logos"/>
  <figcaption>Jekyll and GitHub Pages: a powerful combination!</figcaption>
</figure>

## So what is this DevOps thing?

DevOps can be defined as a combination between cultural philosophies, practices and tools.

The **cultural philosophy** aspect consists in changing how you develop and deploy software. In the DevOps model people who take care of software development and people who take care of operations (by managing, monitoring and operating infrastructure) work very closely together; sometimes the two roles are combined together. The DevOps term originates exactly from here: **Dev**eloper **Op**eration**s**.

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

The DevOps model will improve every aspect of the lifecycle of an application, from development and testing to deployments and production rollouts. The team relies on automation to speed up manual processes and thanks to tools application can grow in a rapid and flexible way.

**DevOps is first of all a mentality shift**, where you are required to change the way you approach software development and release. While it is good to have one person to be the leader of this change, you should make sure that your whole team/company is ready to take the leap.

## Let's dive deeper into the practices

### Continuous Integration
It is the composition of two main elements: a cultural one and a technical/automated one. The cultural part consists in learning how to make frequent integrations. In other words, developers should not wait excessive amounts of time before merging their commits into the rest of the project. The technical/automated part is represented by the tool that helps automating these frequent integrations. Jenkins is a popular open source tool widely used for this. Continuous Integration solves the problem of heavy integrations and it helps reducing time spent solving merge conflicts. Statistically, the longer you wait to merge the more chances you will incur in a conflict. Merge often to avoid this!

### Continuous Delivery / Deployment
It extends Continous Integration by making automated deployments to staging and production environments. These deployments can have pre-requisites such as automated tests; they can even go beyond Unit Tests and require interface tests, load tests, integration tests, API reliability tests and so on. There is difference between Continuous Delivery and Continuous Deployment. With C. Delivery you will automatically deploy on a staging environment and you will be required manual approval if you want to deploy in production. With C. Deployment you go one step further and also automate production rollouts. You can use Jenkins for this or you can search for more specific tools that will hook into the Continuous Integration offered by Jenkins. This practice will help you by reducing human errors and time required to complete the deployment process.











I will briefly cover how to install [Docker](https://www.docker.com/) and [Docker Compose](https://docs.docker.com/compose) since they are required for this set up. This tutorial will work with a fresh Ubuntu install, as long as it is the 64-bit version and sports a kernel version of 3.10 or higher. You can easily find how to do this on a different OS if you search around.

We shall first add the GPG key for the official Docker repository:
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
Then, add the Docker repo to your system's APT sources:
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```
Finally, update the package db and install Docker:
```
sudo apt-get update
sudo apt-get install -y docker-ce
```

Now let's install Docker Compose and apply executable permissions to the binary:
```
sudo curl -L https://github.com/docker/compose/releases/download/1.24.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
Be careful to download the [latest version](https://github.com/docker/compose/releases) of Docker Composer by changing the `1.24.0` part in the request URI above.

You should now be ready to use Docker and Docker Compose. Let's see what role they play in our set up.

## Creating the container

The easiest way to get started is probably to download an existing theme to a local folder. We will call this folder `~/site/`, download a Jekyll theme (for example [Pixyll](https://github.com/johnotander/pixyll)) and store it there.

Let's now create the configuration file relative to our container and let's use Docker Compose to easily create and run that container. Inside `~/site/` create a file named `docker-compose.yml` with the following content:
```
jekyll:
    image: jekyll/jekyll:pages
    command: jekyll serve --watch --incremental
    ports:
        - 4000:4000
    volumes:
        - .:/srv/jekyll
```

The content of this file deserves further explanation. With `image: jekyll/jekyll:pages` we specify that we want to use the official Jekyll image for Docker, in its _pages_ flavor which is suited for GitHub Pages.

With `command: jekyll serve --watch --incremental` we are executing the container. This will run Jekyll's built in development server. It's actually the same as if you would install Jekyll on your machine without a container and tried to make it serve a blog locally. The two additional flags will make sure that Jekyll automatically picks up your edits without having to build the whole site each time. `4000:4000` is there to forward port 4000 of the container to your local port 4000.

The last line will create a mapping between your `~/site/` directory and the directory where the image is configured to look for a Jekyll site, which is `/srv/jekyll`.

Ok, as if that wasn't easy enough, it gets even easier. Just run the following command inside `~/site/`
```
docker-compose up
```
and watch your site go live at `http://127.0.0.1:4000`. Magic.

<figure>
  <img src="{{site.url}}/assets/images/2018-03-01/docker.jpg" alt="Docker logo"/>
  <figcaption>Docker is an amazing tool as it allows to create a working dev enironments in no time! Very useful for teams.</figcaption>
</figure>

## Pushing the site live with GitHub Pages

It's kinda amazing but things are getting even easier, if possible.

Create a new GitHub repository named _username_.github.io (replace _username_ with your GitHub username). Figure out a way to clone the new repository in `~/site/` while retaining all of your previous blog files.

Now just commit and push the blog files to your new GitHub repo. Done, your site should be live at https://_username_.github.io .

___

This is one way to quickly and efficiently set up a fully functional blog at zero cost; I personally find it very convenient! Let me know if you do too.

Should you find any mistake, technical or grammatical, please don't hesitate to let me know!