---
layout: post
published: true
title: Parrot OS Basics 1.1
tags:
  - PWP
  - Beginner
  - Parrot OS Basics
comments: true
---
# File System and basic commands

## Introduction
In this blog post you will learn linux file system and basic commands, 
it will be good if you learn them practically on your system.


## File System

Parrot OS adheres to filesystem hierarchy standard. The Filesystem Hierarchy Standard defines the directory structure and directory contents in Linux distros. 

**Parrot Directories and Description**

_Below are some important directories of Parrot(Linux)._

- / - Its root directory.
- /bin - basic programs available for all users.
- /sbin - contains binary executables for root user only.
- /dev - Contains device drivers.
- /etc - Contains configuration files.
- /lib - It contains shared library files.
- /tmp - Temporary files which typically deleted on boot.
- /usr/bin - It contains users binaries.
- /usr/sbin - It contains root user binaries or system binaries.
- /usr/share - It contains application support and data files
- /home - User home directory.
- ~ - User default working directory.


There are many other directories also, but i only mentioned which we use mostly.


**Basic Commands**

- cd - to change directory(usage: cd dirname)
- ls - list files (usage: ls /home, ls)
- ls -la -> to list files in details
- pwd - print working directory(usage: pwd)
- cat - print file content (usage: cat filename)
- more - It also print file content (usage: more filename)
- cp - to copy files (usage:  cp file /dir/newname)
- mv - to move files(mv file /dir/newname
- mkdir - create directory(usage: - mkdir hacker)
- rm - remove file(usage: rm hacker.txt)
- rmdir - remove directory(usage: rmdir hacker)
- touch - create blank file (usage: touch hacker.txt)
- whereis - show to location of file (usage: whereis cat)
- locate - find files by name ( usage: locate ping)
- man - very useful system commands manual ( usage: man

There are many commands please have a look

**Basic network commands and utilities**
- ping 
- arp
- telnet
- ifconfig
- iptables
- netstat
- route 
- traceroute
- ss

_Use them one by one, read manual using 'man' command_


**Basic system commands and utilities**

- whomai
- hostname
- w
- lslogin
- sudo
- dpkg 
- ps
- users
- crontab 
- less
- more
- apt 
- service 
- free
- top
- mem
- grep
- awk
- find
- lsof
- last
- kill
- uname 
- watch
- df
- dd

**Terminal**

- '$ : specifies, you're in user shell.'
- '# : specifies, you're in root.'

 
**chown command**

chown command changes the user and/or group ownership of for given file.
~~~
chown owner-user file 
chown owner-user:owner-group file
chown owner-user:owner-group directory
chown options owner-user:owner-group file
~~~

**chmod command**

To change access permissions, change mode.

we can edit permissions using chmod command

```$ chmod permissions file
```

There are three types of linux users
-  1. owner
-  2. group
-  3. world

There are three types of permissions that Linux allows for each file.
-  1. read(4 or r)
-  2. write(2 or w)
-  3. execute(1 or x)


So, try wrapping your head around this!!

- 7 = 4+2+1 (read/write/execute)
-  6 = 4+2 (read/write)
-  5 = 4+1 (read/execute)
-  4 = 4 (read)
-  3 = 2+1 (write/execute)
-  2 = 2 (write)
-  1 = 1 (execute)

examples:-
~~~
chmod 777 hacker.sh   

chmod 600 hacker.sh 
~~~

Try it !!!


**_There are many more, have a look and read manual using 'man' command on terminal.
And if you want a tool to help you simple use -h or --help, example ping -h._**
