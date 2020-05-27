---
layout: post
published: true
title: Information gathering with parrot 5.1
tags:
  - PWP
  - Beginner
  - Information gathering
comments: true

---
## Passive approaches to Information Gathering

_**Passive info gathering is the OSINT(open-source intelligence) approach to know about the target.
In passive info gathering, we gather information from open-source resources like social media network, target partners, their web presence, their infrastructure, financial information and many more.**_

**While performing passive info gathering we need to keep information well organised you can use cherry tree or dradis like tools.**


**Whois lookup:** Whois provides public database infrastructure-related information. 

usage:
~~~
$ whois amazon.com
~~~
it will give you information like below
~~~
Domain Name: AMAZON.COM
   Registry Domain ID: 281209_DOMAIN_COM-VRSN
   Registrar WHOIS Server: whois.markmonitor.com
   Registrar URL: http://www.markmonitor.com
   Updated Date: 2019-05-07T20:09:37Z
   Creation Date: 1994-11-01T05:00:00Z
   Registry Expiry Date: 2024-10-31T04:00:00Z
   Registrar: MarkMonitor Inc.
   Registrar IANA ID: 292
   Registrar Abuse Contact Email: abusecomplaints@markmonitor.com
   Registrar Abuse Contact Phone: +1.2083895740
~~~
## Dnslookup


**We can use ns lookup for DNS enumeration of target host**

**Nslookup is a program to query Internet domain name servers.**
~~~
$ nslookup -h

$nslookup google.com
Server:		192.168.43.1
Address:	192.168.43.1#53

Non-authoritative answer:
Name:	google.com
Address: 172.217.166.238
Name:	google.com
Address: 2404:6800:4002:804::200e
~~~
**We have also another tool called dig**
dig is a flexible tool for interrogating DNS name servers. It performs DNS lookups and displays the answers

that are returned from the name server(s) that were queried.
~~~
$ dig -h

$ dig google.com
~~~
**We will now use search engines as our info-gathering tool.**

## Google

**Google is a powerful search engine, which provides advance search options and its dorks like below.
**

- intitle: Use if you want to search for a specific title over the web.( intitle: indexof mp4)
- inurl: Use if you want to search a specific term in url over the web. (inurl: login.php)
- site: Use if you want a specific website as a search result. (site: virustotal.com)
- filetype: Use it to search all document with specific extension (filetype:docx)
- link: It will display a website that have a link to specific websites. (link:facebook.com)
- cache: It will show the cached content of the website. (cache:virustotal.com)

let's see their usage total, as its old school trick to passive info gathering

search following strings on google.

site:amazon.com filetype:pdf 

site:.pk inurl:admin/login

To get all subdomains about a specific website:

site:.amazon.com


you can make your own as per your requirement

To know more about advance search and dorks;

http://www.googleguide.com/advanced_operators_reference.html
http://pdf.textfiles.com/security/googlehackers.pdf
https://www.exploit-db.com/google-hacking-database/


Using wayback machine we can also find archived/deleted data of website:
just open url below and search website or you can also use dorks 
http://www.archive.org/index.php


There are many search engines which also supports dorks and advance search engines 


## Social Media


Social media is also a way to find information about your target, like a number of employees, physical address, events, job posting, requirements, products and more.
Facebook, Linkedin, Indeed, and other jobs sites are the most useful sites to gather information passively.

## theharvestor

**Its a passive info gathering tools for Linux which gather information about a specific target.**

Basic usage: 
~~~
# theharvester -d netflix.com -l 200 -b google, linkedin, facebook
~~~

~~~
-d: for the domain.
-b: for the data source.
-l: limit result.
~~~

## SHODAN

https://shodan.io

Shodan is the world's first search engine for Internet-connected devices. Use Shodan to discover which of your devices are connected to the Internet, where they are located and who is using them. Websites are just one part of the Internet.

we can search for webcam, open ports, specific ip, specific web on shodan using shodan dorks.

Download DEFCON document for shodan to know more, (click here)[https://www.defcon.org/images/defcon-18/dc-18-presentations/Schearer/DEFCON-18-Schearer-SHODAN.pdf]

## censys

https://censys.io
Censys scans the most ports and houses the biggest certificate database in the world, to provide the freshest and most thorough view of your assets; both known and unknown.

## Conclusion

Use these approaches, to gather information about your target.




























 


















