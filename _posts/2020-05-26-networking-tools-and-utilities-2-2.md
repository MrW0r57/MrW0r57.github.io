---
layout: post
published: true
title: Networking tools and utilities 2.2
tags:
  - PWP
  - Beginner
  - Networking tools and utilities
comments: true
---
## Usage of wireshark,tcpdump,tshark

## Introduction

_**In this blog post we will wireshark, tcpdump, tshark and their high level usage.**_

## Sniffing

Sniffing is the process of capturing and monitoring network packets transmission over a network connection.
We can perform sniffing using tools like wireshark, tshark, tcpdump, etc.

## Spoofing

Spoofing is type of attack when an individual is able to modify packets between the transmission of two or more users.
Its an attacker's approach to gain unauthorized access to a user's system or information by pretending to be the user.


## Wireshark


Wireshark is network analysis tool which lets you interactively browse packet data from a live network or from a previously saved capture file

Parrot has inbuilt wireshark installed, you can run it using terminal
~~~
# wireshark -h
 
# wireshark
~~~
1. Select interface, example if we are using wifi then select wlan0

2. Right click wlan0 and start capture

3. And your are able to capture every packet on your device.


**Applying filters**

1. select interface. ex-eth0.

2. Enter http in filter box and start capture.

3. You're able to capture every single http packet


We can also capture auth packets depending n the authentication mechanism implemented on the target web application, we will have to apply specificfilters in order to get only the meaningful packets

let's assume web app is using http citrix authentication 

1. Select interface

2. Enter http.authcitrix and start capture

3. And we can inspect every packet based on mechanism to get credentials.

**We can also analyse captured packets**
~~~
# wireshark -r captured.pcap
~~~
## TSHARK

Its a command-line flavour of wireshark with same functionalities.
TShark is used to analyze real-time network traffic and it can read .pcap files to analyze the information, dig into the details of those connections

~~~
# tshark -h
~~~

lets capture wlan packets

~~~
# tshark -i wlan0
~~~

To read saved packets 
~~~
# tshark -r captured.pcap
~~~

To capture the exact amount of packets in verbose mode

~~~
# tshark -v -c 20 wlan0
~~~

We can also decode packets in various output formats using -T flag.

~~~
# tshark -r captured -T json
# tshark -r captured -T text
# tshark -r captured -T tabs
~~~
we can redirect their output in file using '>'.

# tshark -r captured -T json > file.json

**Applying filters**

**To capture HTTP packets on wlan0 **

~~~
# tshark -i wlan0 -Y http
~~~

**To capture TCP packets on eth0**

~~~
# tshark -i eth0 -Y tcp
~~~

## TCPDUMP


Tcpdump is a powerful packet sniffer that runs via command line.
Tcpdump  prints  out a description of the contents of packets on a net‐work interface that match the boolean expression


open terminal Let's use it..

~~~
# tshark -h

syntax: tcpdump [options] [filter expression]
~~~
~~~
# tcpdump -i wlan0
~~~
And open user you browser to see the packets on your terminal.

**Applying filters**

suppose we want to capture packets only for a specific destination like 8.8.8.8
~~~
# tcpdump -i wlan0 -xxAXXSs 0 dst 8.8.8.8
~~~

**Now you will only capture packets belongs to 8.8.8.8 destination.
**

## Conclusion

_**Check manual to appply more filters, you can use wireshark,tshark,tcpdump  with nmap to trace nmap packets also, try it to know the working of every flag in nmap.**_


