---
layout: post
published: true
title: Parrot OS basics 1.3
tags:
  - PWP
  - Beginner
  - Parrot OS Basics
comments: true

---
## Basic Linux operations 

In this blog post, we are going to perform some basic operations in our Parrot OS.

**What is the process?**

The process is referred to as a program in execution.

_**There are two types of process in Linux:**_

**Foreground processes**: These are controlled by the user directly through a terminal session. 

**Background processes**: They are controlled by the system, they don't expect any user input.

**Daemons**

They are background processes that start at system startup and keep running as a service automatically. They can be controlled by a user via the init process.

**Commands to interact with processes**

To find a process 
~~~
# pid [service_name]
~~~
Example
~~~
# pidof sshd
# pidof top
# pidof httpd
etc.
~~~
To start a process in background
~~~
# firefox &
~~~
To check background process
~~~
#jobs
~~~
To send a running process to the background use [ctrl + z].

To send a background process to the foreground
~~~
# fg [job id]
~~~
To check active Linux processes
~~~
# ps -aux
~~~
For dynamic real time view of running system processes
~~~
# top
~~~
To control process based on their names:
~~~
#pgrep    (pgrep looks through the  currently  running  processes  and  lists  the process IDs which match the selection criteria to stdout.)
~~~
To kill a process
~~~
# pkill  
~~~
There are multiple signals to send a process. 
~~~
# kill -l //list signals

# kill [signal id] [pid]  (send a signal to process)
~~~
To kill an application process using its name

~~~
# killall [program name]
# pkill [program name]
~~~


**Control packages/programs**

To update packages
~~~
# apt update 
~~~
To upgrade packages
~~~
# apt upgrade
~~~
To install a package
~~~
# apt install packagename
~~~
To remove a package 
~~~
# apt remove packagename
~~~
To purge a package
~~~
# apt purge packagename
~~~
To remove corrupted and unused packages run 
~~~
# apt autoremove // always run it after upgradation
~~~

## Conclusion

_**Execute all commands and check response, it will help you to understand the things if you are beginner.**_
 





 















