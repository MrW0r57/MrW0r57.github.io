---
layout: post
published: true
title: Information gathering with parrot 5.3
tags:
  - PWP
  - Beginner
  - Information gathering
comments: true

---
## Recon in hardway

## Introduction

**In this blog post we will learn strong recon techniques to find sensitive information about the target network, we will connect the target network, to Nmap more deep information about the target.**

## Nmap NSE

The Nmap Scripting Engine (NSE) is one of Nmap's most powerful and flexible features. It allows users to write (and share) simple scripts using the Lua programming language to automate a wide variety of networking tasks. Those scripts are executed in parallel with the speed and efficiency you expect from Nmap. Users can rely on the growing and diverse set of scripts distributed with Nmap, or write their own to meet custom needs.

**Nmap scripting engine is a library of Nmap that enhances your network scan. You can achieve everything in scanning from use.**

There are more than 600 scripts which helps you to run a defined scan against a target, you can run scripts easily to scan and enumerate 
target assets, discover vulnerabilities, and exploit them in using NSE.

Let's have a look at these scripts.

~~~
# ls /usr/share/nmap/scripts
~~~
As you can see its really a library of Nmap scripting engine, even you can add your scripts in this folder and run them using 
nmap.

There are lots of scripts to run, suppose if you want to run only some popular scripts against target network then use -sC default flag, which lets you run the top Nmap scripts at once.

usage:
~~~
# nmap -sC target.com
~~~
## lets see some useful categories of nmap scripts

1. auth: you can find all authentication and user privilege scripts.
2. brute: list of scripts for performing brute force to gain credentials from target services.
3. discovery: list of scripts to perform network, service, and host discovery.
4. dos: Denial of service scripts used to test and perform a dos attack against the target.
5. exploit: used to perform service exploitation on different CVE's.
6. fuzzer: Used to perform fuzzing attacks against web apps, services, or networks.
7. intrusive: a set of noisy scripts used to perform an aggressive scan.
8. malware: Malware detections and exploration scripts.
9. safe: a set of safe and non-intrusive scripts.
10. version: a set of OS, service and software detection scripts
11. vuln: a set of vulnerability detection and exploitation scripts

**Ok, now check how to run these scripts on the target network, don't use intrusive and noisy scripts against any network without permission.**

This will run default and safe scripts together.

 nmap --script default,safe <targetIP>

 nmap  --script discovery <targetIP>

**You can target multiple scripts that finish or end up with any pattern, using wildcard.**

**To run all scripts related to http:**
  
 nmap --script "http-\*" 192.168.122.1

**To run all scripts related to ssh:**
 
 nmap --script "ssh-\*" 192.168.122.1

**To run all scripts related to ftp:**
  
 nmap --script "ftp-\*" 192.168.122.1

T**o run a particular script**

 nmap --script="http-waf-detect" targetip


**You can run any script using this technique, check /usr/share/nmap/scripts folder  to get more idea about scripts.**


## Conclusion
Nmap NSE is a powerful tool, if you know how to use this, then you will be able to discover, enumerate, exploit a target easily.
