---
layout: single
title:  "Understanding UNIX/Linux File System Permissions (Part 2)"
date:   2017-12-21 15:00:00 -0800
categories: [UNIX, Linux, Permissions, File System]
permalink: /understanding-unix-linux-file-system-permissions-2
classes: wide
---
In the first part of this couple of posts about UNIX permissions we saw how the system is structured under a users/groups model. We saw how each user belongs to at least one group and how users and groups are unequivocally identified by UIDs and GIDs respectively.

In this part we will see the actual UNIX permission system. We will also explain the concept of ownership.

## Ownership and Permissions
Each file in UNIX belongs to a user and to a group. So, for a generic user, we have three main scenarios:

* User is the owner of file
* A group owns the file and user is part of that group
* User does not own the file nor is in a group who owns the file

But what is Unix ownership, to be more precise? It's actually very simple. The ownership system is used to assign different **permission** sets to different users or groups of users.

Now that we laid down the basics about users and groups, let's get straight to the core of the question: permissions.

First of all we need to know how we can actually view the permissions of a file. To do this we execute the following command inside of a directory:
```
ls -al
```
This will print a **list** of all files present in that directory, along with each file's details. Among these details, as you may have guessed, we also have the file's permissions.

<figure>
  <img src="{{site.url}}/assets/images/2017-12-21/ls.png" alt="Output of ls -al"/>
  <figcaption>The output of ls -al</figcaption>
</figure>

As you can see, a lot of columns will be displayed. Most of them, like the file's name, size, owner and group are self-explained in the picture above. What's interesting here is the first column, the **Mode** one.
Each UNIX file is assigned a mode, which contains permissions. Let's take a closer look at how Mode values should be read.

This the mode for the _asset_ folder in the picture above, properly spaced to allow us to read it better.
```
d rwx rwx r-x
```
The first letter indicates whether the entry is a directory (**d**), a symbolic link (**l**) or a normal file (**-**). The following three sets of triads are the actual file's permission:

* The first three characters after the one denoting the file's type, **rwx**, is the permission class called User and defines permissions for the owner of the file.
* The second three characters after the one denoting the file's type, again **rwx**, is the permission class called Group and defines permissions for each user in that group.
* The last three characters after the one denoting the file's type, this time **r-x**, is the permission class called World (or Other) and defines permissions for anyone else, such as the public.

## Read, Write, Execute
Ok but what are these **rwx**? They stand for Read, Write and Execute. Let's see each one of them in detail.

### Read
 - In the case of a normal file, read means that the user is allowed to open the file and access its content.
 - In the case of a directory, read means that the user is allowed to see what's inside of that directory.

### Write
 - In the case of a normal file, write means that the user is allowed to modify and delete the file's content.
 - In the case of a directory, write means that the user is allowed to create new files inside of the directory and delete it. Always be careful with write, since it's "stronger" than write!

### Execute
 - In the case of a normal file, execute means that the user is allowed to run the file as an executable, provided the user also has read permission.
 - In the case of a directory, execute means that the user is allowed to traverse the directory, in other words the user can "cd" (the UNIX command to change directory) into it.

## Some examples
Let's make some example to make the permission system more clear.
```
-rw-rw-rw-
```
In the case above the file is writable by the user, the group and the world too. Everyone can write the file but no one can execute it.
```
-rw-------
```
In the case above the file is writable only by the user; nor the group and the world can read or write the file. Like the previous case, no one can execute.
```
-rwxr-xr-x
```
In the case above the file is executable by everyone; the user can also modify or delete it.
```
drwxr-x---
```
In the case above the directory is accessible by everyone but the world. The owner can also delete or create new file inside of it.

___

Now you should have at least a basic understanding about how the UNIX file system permissions work! If you have any question or should you find typos or mistakes in this page please let me know through the comments.