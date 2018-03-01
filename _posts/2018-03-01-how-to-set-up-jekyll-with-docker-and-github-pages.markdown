---
layout: single
title:  "How to set up Jekyll with Docker and GitHub Pages"
date:   2018-03-01 15:00:00 -0800
categories: [Jekyll, GitHub Pages, Docker]
permalink: /how-to-set-up-Jekyll-with-Docker-and-GitHub-Pages
classes: wide
---
Want to set up an easy to maintain and highly scalable blog in little to no time? I personally found that running Jekyll in a Docker container for local development and letting GitHub Pages handle the production stack is the best set up for a developer's blog. Let's find out how to achieve, starting from scratch.

## Installation and configuration of Docker and docker-compose

I will briefly cover how to install [Docker](https://www.docker.com/) and [docker-compose](https://docs.docker.com/compose) since they are required for this set up. This tutorial will work with a fresh Ubuntu install (as long as it the 64-bit version and sports a kernel version of 3.10 and onwards) but you can easily find how to do this on a different OS if you search around.

We shall first add the GPG key for the official Docker repository:
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
Then, add the Docker repo to your system0s APT sources:
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```
