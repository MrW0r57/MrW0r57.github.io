---
layout: post
published: false
title: Parrot OS Basics 1.2
---
# Managing services in parrot

## Introduction

In this blog post we will learn how to manage services and programs in parrot os.

## Linux Services

Basically linux services are the program which runs in background outside the interactive control of system.
Services also known as daemons in linux systems. example - sshd, httpd (d is for daemon).

We have to switch user to root to use sytemctl and service command (check the usage using 'man systemctl', 'man service'.
``
$ su ( to switch user to root)
``
Now list all the services using command below
~~~
 # systemctl list-unit-files --type service --all

~~~
This command will show enable, disable. masked, static services

To know only running services
~~~
# systemctl | grep running
~~~

To start a service 
~~~
# service [service_name] start
~~~
or
~~~
# systemctl start [service_name]
~~~
To stop service
~~~
# systemctl stop [service_name]
~~~
or
~~~
service [service_name] stop
~~~
To know the service status
~~~
# systemctl status [service_name]
~~~
or
~~~
# service [service_name] status
~~~

It is also possible to have a service run while the operating system is being loaded:

~~~
# systemctl enable [service_name]
~~~
or
~~~
# service [service_name] enable
~~~

To disable service
~~~
# systemctl disable [service_name]
~~~
or
~~~
# service [service_name] disable
~~~
_**This is the high level overview to system services and how to manage them..
**_