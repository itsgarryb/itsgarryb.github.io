---
layout: single
title:  "Understanding UNIX/Linux File System Permissions (Part 1)"
date:   2016-09-30 15:00:00 -0800
categories: [UNIX, Linux, Permissions, File System]
permalink: /understanding-unix-linux-file-system-permissions-1
classes: wide
---
This series of articles is mainly for UNIX/Linux newbies, the topic will be covered in a way that is both simple and easy to understand. One of the things that's often not clear to users approaching the UNIX world is how the **permission** system for file and directories works. In fact, _UNIX is a multi-user system_, which means there are multiple users that can connect to a UNIX system at the same time and do operations with it. This is also true for other UNIX-like system like Linux.

Examples of this? Just think of a machine, running a UNIX system, connected to a network (such as an intranet or the Internet). Multiple users can concurrently establish connections with this machine, via telnet or SSH, and execute programs, get outputs and so on.

So a couple of reasons this permissions system exist is to avoid one user accessing files that are protected by another user and not to allow single users to crash the whole system.

## Not every user is human
In UNIX not all users are humans. I may have a user _garry_ in a system, denoting myself, but there may also be a user called _www-data_ which denotes the privileges necessary for a web-server process to run. For the system, users represent an abstraction which **defines what they may or may not do** with any given entity in the file system.

Each user is unequivocally identified by a *UID* (User ID), which is a numeric value that allows the system to discriminate between all present users. Login usernames such as _garry_ and _www-data_ are just aliases for human operators, meant to make us more comfortable. For example, in my system, user _garry_ may have the UID 1021. The system does not have problems associating the UID number with me, but the same number gives no valuable information to other human users operating the system. Instead, if another human user sees my username (garry) instead of my UID (1021), it is much easier for them to recognize me.

## Users belong to groups
In UNIX every user belongs to at least one group. This means there can't be UNIX users not associated to a group. But what are these UNIX groups, precisely?

The purpose of groups is basically to assign the same privileges over a determined resource to multiple users, in a quick and efficient way. To make an example, you may need this is in a situation where different users are working on the same project files. 
Groups, like users, have also their numerical identifiers. They are called **GID** (Group ID).

<figure>
  <img src="{{site.url}}/assets/images/2016-09-30/perm-1.png" alt="Graphical permission representation"/>
  <figcaption>A preview from the next article of this series: this is how permissions are generally represented for a given file.</figcaption>
</figure>

## How to find out your UID and GID
If you are on a UNIX or UNIX-like system you can find out UIDs with the following command:
```
id -u username  
```
Remember to replace _username_ with the desired user. For example, if I want to get the UID of the user _www-data_ in my system, I will have to execute the following:
```
id -u www-data
```  
The result will be printed in the terminal as a numerical value, which is the UID for the specified user.

You can also get the GID of a user by typing the following at the UNIX prompt:
```
id -g username  
```
Don't forget to replace _username_.

If you want to find out all groups a user belongs to, you will need to enter the following:
```
id -G username  
```
Note the capital G which is different from the lower-case g in previous command.

To recap, in this post we saw how a UNIX system is structured, under a user/group point of view. Users in UNIX are quite different than users in Windows; in addition, Windows doesn't have the concept of group as seen in UNIX. These concepts are mandatory to explain what we will see in the next part, the UNIX permission system.

Should you find any mistake, technical or grammatical, please don't hesitate to let me know!

