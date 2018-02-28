---
layout: single
title:  "How to keep Ghost running using pm2"
date:   2016-03-10 15:00:00 -0800
categories: Ghost pm2
permalink: /how-to-keep-ghost-running-using-pm2
classes: wide
---
So you just set up your brand new blog with [Ghost](https://ghost.org/), the node.js-based blogging platform? You will most likely encounter the problem of keeping alive (and/or restarting) the node.js process on which Ghost is running.

In fact, if you want to launch Ghost on production values, you would normally use npm with the following command:
```
npm start --production
```

## What's the Problem?

You'll experience the problem once you close the terminal session where you issued the previous command. Closing the terminal also kills Ghost (i.e. **your blog isn't available anymore**) and that's not what we want! 
You will also notice that once you restart your machine, Ghost will not automatically start on boot. You will have to start it manually **with each physical machine restart**.

There are multiple ways to solve the aforementioned issues, we'll examine one method in particular to achieve the solution. Once we're done you'll be able to close the terminal and have Ghost running in the background without problems. 
This will also help you to have Ghost automatically start when your machine is subject to a system reboot.

<figure>
  <img src="{{site.url}}/assets/images/2016-03-10/ghostlogo.png" alt="Ghost Logo"/>
  <figcaption>I am now using Jekyll but Ghost is a wonderful blogging platform!</figcaption>
</figure>

## Onto the solution

In order to achieve our solution, we will use two [npm](https://www.npmjs.com/) modules called [forever](https://www.npmjs.com/package/forever) and [pm2](https://github.com/Unitech/pm2). They are both easy and relatively straight-forward to install and use.
 
First of all, we navigate to the directory where Ghost is installed.
```
cd /path-to-your-Ghost-installation-directory
```
Then we can proceed with installing and setting up pm2 itself. Execute these commands sequentially, preferably as a non-root user.
```
sudo npm install -g pm2
cd /path/to/ghost/folder
sudo npm install -g pm2
echo "export NODE_ENV=production" >> ~/.profile
source ~/.profile
pm2 kill
pm2 start index.js --name ghost
pm2 dump
```

Now there's only one last command left to execute. This depends on the OS you're currently on.
```
pm2 startup your-os
```
There are good chances that you're on Ubuntu, Debian or CentOS; if that's the case you just have to replace "your-os" with the name of your OS.
For example, if you're on CentOS, you'll have to execute the following command:
```
pm2 startup centos
```
If you're on Ubuntu:
```
pm2 startup ubuntu
```
And so on.

## Some useful commands
Now that we have everything correctly installed and set up let's see how to use this module. Following there are a few useful commands to get data and stats with pm2.

* Stats
    ```
    pm2 status
    ```
    Once executed, this command will show you a few useful statistics on your Ghost instance such the status, memory footprint and the process ID.

* Stopping and starting

    If you want to stop your Ghost instance you should first know what's the "App Name" of the said instance. This can be found under the "App Name" column when you execute the status command. If you followed this guide, your "App Name" should be "ghost". You can stop your Ghost blog by issuing the following command:
    ```
    pm2 stop ghost
    ```
    If you now wish to start Ghost, type and execute the following:
    ```
    pm2 start index.js --name ghost
    ```
    When using the start command you can assign to the newly created instance whichever name you prefer (with the --name parameter as in the example above); to subsequently stop Ghost you will have to use this same name. Notice that we issued this command in the beginning, along with the pm2 setup.
    Otherwise you can simply use:
    ```
    pm2 restart ghost
    ```
    This will restart your Ghost instance with the same previous parameters.

* Logs
    ```
    pm2 logs
    ```
    You can use this command if you want to get live statistics and logs from your Ghost instance.
