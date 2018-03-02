---
layout: single
title:  "How to set up Jekyll with Docker and GitHub Pages"
date:   2018-03-01 15:00:00 -0800
categories: [Jekyll, GitHub Pages, Docker]
permalink: /how-to-set-up-Jekyll-with-Docker-and-GitHub-Pages
classes: wide
---
Want to set up an easy to maintain and highly scalable blog in little to no time? I personally found that running Jekyll in a Docker container for local development and letting GitHub Pages handle the production stack is the best set up for a developer's blog. Let's find out how to achieve this, starting from scratch.

<figure>
  <img src="{{site.url}}/assets/images/2018-03-01/github_jekyll.png" alt="Jekyll and GitHub logos"/>
  <figcaption>Jekyll and GitHub Pages: a powerful combination!</figcaption>
</figure>

## Installation and configuration of Docker and Docker Compose

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
sudo curl -L https://github.com/docker/compose/releases/download/1.20.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
Be careful to download the [latest version](https://github.com/docker/compose/releases) of Docker Composer by changing the `1.20.0` part in the request URI above.

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