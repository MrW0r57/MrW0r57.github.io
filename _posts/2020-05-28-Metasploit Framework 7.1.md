---
layout: post
published: true
title: Metasploit Framework 7.1
tags:
  - PWP
  - Intermediate
  - Metasploit Framework
comments: true
---
## Metasploit Fundamentals


## Introduction

_**In this blog post we will discuss a penetration testing framework called Metasploit-Framework.**_


```
whatis msfconsole
whatis msfvenom
man msfconsole
```

Execute above commands in your Parrot OS Terminal.

Let's Introduce Metasploit-Framework !!!

**Metasploit-Framework** _is the all purpose open-source pentesting framework with all kind of collection of exploits, shellcodes, fuzzing tools, payloads, encoders etc._

Its a complete penetration testing arsenal package.

There is also a paid pro version available for Metasploit-Framework that comes with lot more features.


Metasploit-framework comes allready installed in Parrot OS, you can run it by 'msfconsole' command using terminal.

There is also a GUI flavor of Metasploit-framework called 'armitage' which also comes with Parrot OS, you can run it using 'armitage' command in terminal.


**Features of Metasploit-framework**


1. Its easy to use.
2. It comes with over 2014 exploits include 0 days, 1097 auxilaries, 343 post modules, 566 payloads, etc that are updated on regular basis.
3. Anyone can develop his own exploits,payloads auxilaries and use it with metasploit easily.
4. Provides good interface between target and user.
5. It has some shortcuts that are very useful during penetration test.



**What you can hack with metasploit-framework?**

Using metaspploit framework you can hack networks, websites, android mobile phones, iOS mobile phone, Linux Systems, Windows System, MAC systems, IOT's and more .
Its a versatile arsenal in every pentester tool kit.

**What is msfvenom?**

Msfvenom  is a combination of Msfpayload and Msfencode, putting both of these tools into a single Framework  instance.

**To know about msfvenom**

```
man msfvenom
```
To list msfvenom library

```
msfvenom -l
```


**What is metasploit-meterpreter?**


Meterpreter is an advanced, dynamically extensible payload that uses in-memory DLL injection stagers and is extended over the network at runtime. It communicates over the stager socket and provides a comprehensive client-side Ruby API. It features command history, tab completion, channels, and more.


**Metasploit Modules**

Almost all of your interaction with Metasploit will be through its many modules, which it looks for in two locations. The first is the primary module store under /usr/share/metasploit-framework/modules/ and the second, which is where you will store custom modules, is under your home directory at ~/.msf4/modules/.

**You can check Metasploit Modules yourself.**
```
# ls /usr/share/metasploit-framework/modules
   
   auxiliary  encoders  evasion  exploits  nops  payloads  post   
 
```

**They all are organised in seperate directories, you can also check them one by one.**


**Auxiliary**

You can find any kind port scanners, fuzzers, sniffers, and more in auxiliary modules.

```
# ls /usr/share/metasploit-framework/modules/auxiliary 

admin	 client   docx	      fileformat  parser   server   sqli
analyze  cloud	  dos	      fuzzers	  pdf	   sniffer  voip
bnat	 crawler  example.rb  gather	  scanner  spoof    vsploit

```

**Payloads, Encoders, Nops**

Payloads consist of code that runs remotely, while encoders ensure that payloads make it to their destination intact. Nops keep the payload sizes consistent across exploit attempts.

```
# ls /usr/share/metasploit-framework/modules/payloads/
  
  singles  stagers  stages

# ls /usr/share/metasploit-framework/modules/encoders/
  
  cmd  generic  mipsbe  mipsle  php  ppc  ruby  sparc  x64  x86

# ls /usr/share/metasploit-framework/modules/nops/
  
  aarch64  armle  mipsbe  php  ppc  sparc  tty  x64  x86

```

**Exploits**

Exploits used payloads to exploit target system and get meterpreter shell.

```
# ls /usr/share/metasploit-framework/modules/exploits/

 aix        bsdi        firefox  irix       multi    solaris
 android    dialup      freebsd  linux      netware  unix
 apple_ios  example.rb  hpux     mainframe  osx      windows

```

**POST** 

These are post exploitation modules that can quickly gather valuable information about a target, helps to esclate privileges, sensitive data, credentials, etc, easily.

```
#ls /usr/share/metasploit-framework/modules/post

 aix	 apple_ios  bsd    firefox   juniper  multi  solaris
 android  brocade    cisco  hardware  linux    osx    windows

```

**lets look in windows directories**

```
ls /usr/share/metasploit-framework/modules/post/windows

 capture  escalate  gather  manage  recon  wlan

```
**And check some 'post/gather modules' and 'post/escalate' modules **

```
ls /usr/share/metasploit-framework/modules/post/windows/gather | head
 ad_to_sqlite.rb
 arp_scanner.rb
 bitcoin_jacker.rb
 bitlocker_fvek.rb
 bloodhound.rb
 cachedump.rb
 checkvm.rb
 credentials
 dnscache_dump.rb
 dumplinks.rb

```

```
# ls /usr/share/metasploit-framework/modules/post/windows/escalate | head
 

 droplnk.rb
 getsystem.rb
 golden_ticket.rb
 ms10_073_kbdlayout.rb
 screen_unlock.rb
 unmarshal_cmd_exec.rb

```

_We have learnt basic fundamentals of metasploit framework_

**Let's discuss some approaches to use metasploit framework.**

Approaches are mostly same like we perform manual pentesting in our terminal.

* Scan & Enumerate the target using metasploit auxilary modules.

* Select an exploit based on findings, and based of our target scope.

* Use payloads in target system to get successfull access to target.

* Encode arbitrary payload/exploit, if target system is running any protection.

* After successfull access on target system, gather sensitive data. escalate privileges, and delete logs



**These are some basic fundamentals of Metasploit-Framework**


## Conclusion

_**I would like to suggest you to read more about metasploit-framework, because it has every thing you want to exploit your target,there is also a free training title as **[Metaspoit-Unleashed](https://www.offensive-security.com/metasploit-unleashed/)** provided by **Offensive Security** that described every thing about Metsaploit-Framework.**_
