---
layout: post
published: false
title: Enumeration Is The Key To Success 6.1
---
## Linux Approaches

_**In this blog post we will learn some tools and techniques to enumerate target network remotely from our Parrot OS.**_




## Enumeration

Enumeration is the process to get more detailed information about target services, security misconfigurations, account names, public shares and more by connecting remotely to the target network.







## Services that reveals information

- FTP  - File transfer protocol is basically a layer 7 protocol that is used to transfer file to and from server, by authenticated user.
 
- SSH - Secure shell is a remote Login Protocol used to securely log on to a computer from another computer remotely and execute commands.
 
- Telnet - Telnet protocol is used to execute commands on network connected systems remotely.

- SMTP - Simple mail transfer protocol is email transfer protocol.

- DNS - Domain Name System resolves the names of internet sites with their underlying IP addresses.

- HTTP/S - HTTP/HTTPs is used by web servers to receive requests from client browsers. 

- LDAP - Lightweight Directory Access Protocol (LDAP) is a set of open protocols used to access centrally stored information over a network.
 
- SQL servers - SQL Server is a relational database management system developed by Microsoft.

- NFS - Network File System is a rpc based file sharing protocol found in linux systems, it used to provide access to shared resources.

- IPSec - IP security is a collection of security standards that enable computers on a TCP/IP network to encrypt and digitally sign their transmissions.
 
- NetBIOS - NetBIOS(network basic input/output system) provides session layer services to Windows workgroup that is, non-Active Directory networks.

- SNMP - Simple Network Management Protocol is an Internet Standard protocol for collecting and organizing information about managed devices on IP networks and for modifying that information to change device behavior.

- Samba - a Linux-based implementation of the SMB/CIFS protocols, provides print and file sharing services for windows clients within an environment.

- SMB - SMB works through a client-server approach, where a client makes specific requests and the server responds accordingly. SMB protocol specifically deals with access to filesystems, such that clients may make requests to a file server.

- RPC - Remote procedure call is an interprocess communication technique that is used for client-server based applications.

- etc.









**Scan the network by nmap and netdiscover to open ports and services, now we have to enumerate them.**

_**To scan verbose, syn, all ports, all scripts, no ping**_

`
nmap -vv -A -sC -sS -T 4 -p- <targetIP> -Pn
`

_**To scan verbose, syn, udp, version, deny DNS rsolution**_

'
# nmap -v -sS -sU -sV -n 192.168.0.1/24
'

**_netdiscover** is an active/passive ARP reconnaissance tool, initially developed to  gain  information  about  wireless  networks  without  DHCP servers  in  wardriving scenarios._

**usage** 

'
# netdiscover -r <targetIP range>
'

**If port 80/443 is running, you can guess server user's from there, that you can  use login ssh, ftp etc.**

## FTP Enumeration
  
nmap -A -p21 <targetIP>


**First check anonymous ftp login on server, if ftp anonymous login is enable on server then connect with command below.**

'
 # ftp <targetIP>
'

And it will connect you to target network, you can perform any ftp operations using ftp commands, 

_**To check ftp commands after connecting to the target server**_

'
# help
'

And it will show comands that you can use to perform actions.

**Using nmap to enumerate ftp**
  
check ftp scripts in nmap

`
# ls /usr/share/nmap/scripts | grep ftp
'

There are various ftp use them together enumeration scripts in nmap

**usage:** 
~~~
# nmap --script ftp-anon,ftp-bounce,ftp-libopie,ftp-proftpd-backdoor,ftp-vsftpd-backdoor,ftp-vuln-cve2010-4221,tftp-enum -p 21 10.0.0.1
~~~


  
  
  
## SSH Enumeration


nmap -A -p22 <targetIP>

**After finding open ssh port we can enumerate it for ssh users using nmap scripts**

**you can try to connect ssh**

'
ssh <TargetIp> 22
'

**You can run below scripts in order to enumerate ssh as per you requirement.**
 
'
# ls /usr/share/nmap/scripts | grep ssh
  
ssh2-enum-algos.nse
ssh-auth-methods.nse
ssh-brute.nse
ssh-hostkey.nse
ssh-publickey-acceptance.nse
ssh-run.nse
sshv1.nse

'


  
  
## SMTP Enumeration


nmap -A -p25 <TargetIP>

**check nmap scripts to run against target host**

'
ls /usr/share/nmap/scripts | grep ftp
'
run all together

# nmap --script smtp-commands,smtp-enum-users,smtp-vuln-cve2010-4344,smtp-vuln-cve2011-1720,smtp-vuln-cve2011-1764 -p25 <targetIP>



  
  
## NFS Enumeration (RPC)


Lets enumerate it

# nmap -p2049 -A <target IP>

**check for nmap scripts**

'
# ls /usr/share/nmap/scripts | grep nfs

nfs-ls.nse
nfs-showmount.nse
nfs-statfs.nse

'

**To find rich result of nfs enumeration**

'
nmap --script nfs-ls,nfs-showmount,nfs-statfs <TargetIP>
'

**To interact with publicaly available nfs exports, we can showmount also.**

'
showmount -e <targetIP>

/home/server/ *
'

**To mount the availaible nfs exports**

'
**We can create a sepearte directory in our system** 

'
 mkdir -p /mnt/home/server
'

**Now mount nfs in this directory**

'
# mount -t nfs <NFS_TargetIP>:/home/server/export /mnt/home/server -o nolock
'

**And now you're able to navigate server exports in your system just check the  directory you made.**


  
  

  
  
## Enumerate rpcbind

rpcinfo -p <TargetIP>


## Samba Enumeration

We can find sensitive informaion if we enumerate samba properly.

You can find Samba listening on NetBIOS ports.

Let's catch Samba

'
# nmap -A -p135,137,138,139,445 <TargetIP> --open

**After that we can enumerate smb shares using smbclient and smbmap tools in Parrot OS**

'
# smbclient -L <TargetIP>
'

**For more detailed information use smbmap**

'
# smbmap -H <TargetIp>
'

**After finding share we can easily interact with using smbclient tool**

'
# smbclient \\\\<targetIP>\\sharename
'

**After succesfully connecting use 'help' command to list navigation commands and try to get more information from those shares.**


You can also simply your task using [enum4linux](https://github.com/portcullislabs/enum4linux) tool in seconds.

**usage :**

'
# enum4linux -a <TargetIP>


  
  
  
## SMTP Enumeration

**Grab SMTP information using telnet and nc on running smtp target server.**


# nc <targetIp> 25


# telnet <targetIP> 25

  
  
There is a tool also to enumerate smtp and smtp users

[smtp-user-enum](http://pentestmonkey.net/tools/user-enumeration/smtp-user-enum)


## Conclusion
  
  _**I have explained tools, techniques and their usage, revise them and read tools manual to know more.**_
  