---
layout: post
published: true
title: Enumeration is the key to sucess 6.2
tags:
  - PWP
  - Intermediate
  - Enumeration
comments: true
---
## Windows Approaches

## Introduction

_**In this blog post we will learn windows enumeration approaches, tools to use and techniques to implement.**_





## NetBIOS Enumeration


NetBIOS basically allows an application on different computer systems to communicate with one another in a local area network.
It allows a computer to share printers and files, remote procedure calls, exchange messages, etc.
This may reveal much information than we expected.




**There are some NetBIOS suffix's that you must know before interacting with NetBIOS**

Open the link and read about them [click here](https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-brws/0c773bdd-78e2-4d8b-8b3d-b7506849847b?redirectedfrom=MSDN)


 **nbtscan**


nbtscan is a tool used to scan networks for NetBIOS name information.



**usage:**


 nbtscan -v  <TargetIP>
 

**In Windows there is also a tool called nbtstat, you can also use it to enumerate.**

  

 nbtstat -A <target_IP_Address>



**The result will show the name, service, type. Use NetBIOS suffix table to figure out what service they are offering.**


  
  
  
## Enumerating SMB



**Like linux samba enumeration we have to use smbclient and smbmap.**


  
**usage:**

 smbclient -L <Target IP>

  

  
**It will display some smb shares, how to interact with them?**

  
suppose you found some shares like



   Public
  
   IPC$
  
   Admin$
  
   C$
  
   hacker


smbmap -h <TargetIP> to get more detailed information


Let's interact with IPC$
  


# smbclient \\\\<targetIP>\\IPC$ -U 

  

we can use username also with '-U '<Username>' '
  


**you can guess username from website**
  
  
  
  

**Mount SMB shares using mount in your folder /home/share**


sudo mount.cifs //<targetIP>/C /home/share/ user=,pass=


or you can use your windows to interact with smb shares


C:\> net use \\<TargetIP>\IPC$ "" /u:""


  
  
**You can also use multiple tools to enumerate NetBIOS**

  
enum4linux


enum4linux -a <TargetIP>


Wininfo


winfo <targetIP> -n


**-n** tells the tool to establish a null session before trying to dump the information.

There are other windows gui based tool to enumerated dumpsec, you can install it to use

  
  
  
**rpcclient**

  

rpcclient  :rpcclient is a utility initially developed to test MS-RPC functionality in SMB itself.


  rpcclient -N -U "" <targetIP>


-N - Not asking for password
-U - set username (""for none)


**After connecting**


rpcclient $> enum


  
  
you will get multiple commands to execute.

To enumerate users 


rpcclient $> enumdomusers

  
this will tell you all users on the target network

**There are many more rpcclient commands used to interact with target.**

``
enumalsgroups , srvinfo , lookupnames ,
queryuser , enumprivs .
``


## SNMP Enumeration


SNMP Stands for Simple Network Management Protocol and it is used for exchanging management information between network devices.
You can even use SNMP to configure router and check its status.


**nmap scripts for snmp enumeration**


ls /usr/share/nmap/scripts | grep snmp

  snmp-brute.nse

  snmp-hh3c-logins.nse

  snmp-info.nse

  snmp-interfaces.nse

  snmp-ios-config.nse

  snmp-netstat.nse

  snmp-processes.nse

  snmp-sysdescr.nse

  snmp-win32-services.nse

  snmp-win32-shares.nse

  snmp-win32-software.nse

  snmp-win32-users.nse


**usage :**


 nmap -A -p <TargetIP> 

  
nmap -p161 --script snmp-info,snmp-interfaces,snmp-netstat,snmp-brute <TargetIP>


Another tool to enumerate
  
  

**snmpcheck**
  
snmpcheck  is  a  program  that checks the SNMP status of the specified hosts
  
  
**usage:**


man snmpcheck

  
snmpcheck -t 192.168.1.X -c public


  
  
  
  
  
**snmpwalk**

snmpwalk is an SNMP application that  uses  SNMP  GETNEXT  requests  to query a network entity for a tree of information.
  
  
  
  
**usage:**

 man snmpwalk

 snmpwalk -v 2c <TargetIP> -c public

  
  
  
  
  
## Conclusion

**_There may be many other tools for this purpose, but I have covered useful tools. I recommend please check their manual using 'man <toolname>` command to know all functionalities of these tools._**
