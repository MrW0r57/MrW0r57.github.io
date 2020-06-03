---
layout: post
published: true
title: Information gathering with parrot 5.2
tags:
  - PWP
  - Beginner
  - Information gathering
comments: true
---
## Active approaches to Information gathering 

**It requires direct engagement with the target system through scanning ports, protocols, and services to learn more about the target system.
It helps us to know about what services are running on the target system which helps us to know weaknesses in the target system.**


**Read this document before moving ahead**
https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml

## Banner Grabbing

**Banner grabbing is a technique used to gain information about a computer system on a network and the services running on its open ports**

To grab banner of ssh port of target hosts we can use telnet and netcat like below:

 nc <targetip> <port>
~~~
# nc 10.10.10.189 22
~~~
~~~  
# telnet 10.10.10.189 22
~~~
  
To grab HTTP services banner

~~~
# nc 10.10.10.189 80
~~~

~~~  
# telnet 10.10.10.189 80
~~~


## NMAP

Nmap (Network Mapper) is an open-source tool for network exploration and security auditing. It was designed to rapidly scan large networks, although it works fine against single hosts. Nmap uses raw IP packets in novel ways to determine what hosts are available on the network, what services (application name and version) those hosts are offering, what operating systems (and OS versions) they are running, what type of packet filters/firewalls are in use, and dozens of other characteristics.



**I would strongly recommend reading its manual to know about its flags and usage**

~~~  
# nmap -h
# man nmap
~~~
  
**basic syntax**

nmap <scan type> <options> <target>

**Host discovery techniques used by Nmap**

- -sL: List Scan - simply list targets to scan
- -sn: Ping Scan - disable port scan
- -Pn: Treat all hosts as online -- skip host discovery
- -PS/PA/PU/PY[portlist]: TCP SYN/ACK, UDP or SCTP discovery
- -PE/PP/PM: ICMP echo, timestamp, netmask request discovery
- -PO[protocol list]: IP Protocol Ping
- -n/-R: Never do DNS resolution/Always resolve
- --dns-servers <serv1[,serv2],...>: Specify custom DNS servers
- --system-dns: Use OS's DNS resolver
- --traceroute: Trace hop path to each host

**Scan techniques used by nmap**

- -sS/sT/sA/sW/sM: TCP SYN/Connect()/ACK/Window/Maimon scans
- -sU: UDP Scan
- -sN/sF/sX: TCP Null, FIN, and Xmas scans
- --scanflags <flags>: Customize TCP scan flags
- -sI <zombie host[:probeport]>: Idle scan
- -sY/sZ: SCTP INIT/COOKIE-ECHO scans
- -sO: IP protocol scan
- -b <FTP relay host>: FTP bounce sca


By default nmap use -sS(TCP SYN scan) as known stealthy scan or half scan, it can be performed quickly, scanning thousands of ports per second on a fast network not hampered by restrictive firewalls

**To check its working i suggest you to monitor using wireshark to capture nmap packets**
~~~
# nmap amazon.com
~~~
works as
~~~
# nmap -sS amazon.com
~~~
we can specify port using -p
~~~
# nmap -sS -p 445 amazon.com
~~~
  
**TCP connect scan:** It is the default TCP scan type when SYN scan is not an option. This is the case when a user does not have raw packet privileges. Instead of writing raw packets as most other scan types do, Nmap asks the underlying operating system to establish a connection with the target machine and port by issuing the connect system call. This is the same high-level system call that web browsers, P2P clients, and most other network-enabled applications use to establish a connection.

~~~
# nmap -sT target.com 
~~~

**UDP Scan:** UDP scan is activated with the -sU option. It can be combined with a TCP scan type such as SYN scan (-sS) to check both protocols during the same run.

~~~
# nmap -sS -sU nmap.org
~~~


The Idle scan is a stealth technique that involves the presence of a zombie in the target network. A zombie is a host that is
not sending or receiving any packets thus, the reason its called an idle scan.

~~~
#nmap -sI nmap.org
~~~
**-A (Aggressive scan options)**: This option enables additional advanced and aggressive options. Presently this enables OS detection (-O), version scanning (-sV), script scanning (-sC) and traceroute (--traceroute).  More features may be added in the future. The point is to enable a comprehensive set of scan options without people having to remember a large set of flags. However, because script scanning with the default set is considered intrusive, you should not use -A against target networks without permission. This option only enables features, and not timing options (such as -T4) or verbosity options (-v) that you might want as well. Options that require privileges (e.g. root access) such as OS detection and traceroute will only be enabled if those privileges are available.

~~~
# nmap -A -sV -p- target.com -Pn -T4
~~~
~~~
# nmap -A target.com
~~~

Run both scans and check the difference

There are also many other scans to use as per your need, I recommend you to read manual using 'man' command to learn more

We can also randomly scan host on the internet using the command below

**scan random web servers**
~~~
# nmap -Pn -sS -p 80 -iR 0 --open
~~~
scan all ports of random host
~~~
# nmap -Pn -sS -p- -iR 0 --ope
~~~
~~~
-iR: choose random target over internet
~~~
## Zenmap

Zenmap is the GUI flavor of nmap tool available in parrot and you can install it in windows also.
Zenmap aims to make Nmap easy for beginners to use while giving experienced Nmap users advanced features. Frequently used scans can be saved as profiles to make them easy to run repeatedly. A command creator allows the interactive creation of Nmap command lines. Scan results can be saved and viewed later. Saved scan results can be compared with one another to see how they differ. The results of recent scans are stored in a searchable database.

**There are many other tools also to actively scan networks** 

[Angry IP Scanner](http://angryip.org/) (Linux, Windows, Mac OS X)

[Masscan](https://github.com/robertdavidgraham/masscan) (Linux, Mac OS X, Windows)

[SuperScan](http://www.mcafee.com/us/downloads/free-tools/superscan.aspx) (Windows)

## Conclusion
  
  **Try these approaches on your testing network to gather information.**
