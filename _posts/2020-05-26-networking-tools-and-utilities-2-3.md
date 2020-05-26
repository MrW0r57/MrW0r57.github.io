---
layout: post
published: true
title: Networking tools and utilities 2.3
tags:
  - PWP
  - Beginner
  - Networking tools and utilities
comments: true
---
## Man in The Middle (MiTM)

## Introduction

_**In this blog post we wil learn Man in The Midlle attacks and how to perform them using ettercap tool.**_

## What is Man in the middle (MiTM) ?

The Man in the Middle (MitM) is an attack in which the attacker is able to read, modify or insert arbitrary data in packets transmitted between two peers.The attacker sits between the peers connection and control the packets.It requires some prerequisites for the attack to be successful

**Commonly this attack is used in Local Area Network (LAN), because of lack of security in layer 2 and layer 3 ports.**

## ARP and RARP

Address Resolution Protocol is the layer 3 protocol which is used to convert IP adress of a host into its MAC address or Ethernet address.

Reverse ARP is used by a client machine in a local area network to request its Internet Protocol address, its opposite to ARP.

## ICMP

Internet Control Message Protocol is layer 3 protocol used to give status and feedback about network packet delivery and it can provide information about problem occur while packet delivery.

## DHCP

Dynamic Host Configuration Protocol (DHCP) is a client/server protocol that automatically provides a host with its IP address and other related configuration information such as the subnet mask and default gateway.With APIPA, DHCP clients can automatically self-configure an IP address and subnet mask when a DHCP server isn't available



## Introduction to Ettercap

Ettercap is a multipurpose  sniffer/content filter for man in the middle attacks. It combines a packet
sniffer for different protocols (POP/HTPPS/HTTPS/SFTP), and also offers password cracking features.

Run Ettercap in GUI

~~~
# ettercap -G
~~~
First we have to choose interface to use and the sniff option.

**We can chose between:**

 Unified: it sniffs all the packets on the cable
 
 Bridged: it uses two network interfaces and forwards the traffic from one to the other
 
The first step once we run Ettercap is to scan the network in order to find alive hosts 

Now toggle menu and select targets to sniff.

**After setting the target we can select type of MiTM attack we want to run:**

**ARP poisoning**: ARP poisoning is an attack that involves sending spoofed ARP messages over a local area network. It divert traffic from its originally intended host to an attacker instead.

**ICMP redirect**: Also called smurff attack,is a distributed denial-of-service attack in which large numbers of Internet Control Message Protocol (ICMP) packets with the intended victim's spoofed source IP are broadcast to a computer network using an IP broadcast address. 

**Port Stealing**: Port stealing is a kind of attack where someone "steals" traffic that is directed to another port.This attacks allows someone to receive packets that were originally directed to another computer.

**DHCP spoofing**: DHCP Spoofing attack is an attack in which attackers set up a rogue DHCP server and use that to send forged DHCP responses to devices in a network. Attackers often use this attack to replace the IP addresses of Default Gateway and DNS servers and thereby divert traffic to malicious servers

**Select attack 1 ARP poisoning and you will get a popup, enable Sniff remote connections and press OK.**

_**Now ARP Poisoning attack will automatically start and now we should be able to intercept the traffic of our target host**_

To inspect the intercepted packets **click on view -> connections**, and you're able to see all the traffic generated from the target machine. To inspect the packets, we can double click on a connection listed and you will get details of data transmitted.

**Ettercap automatically tries to intercept credentials sent via the network**


## Conclusion 

_**There are many mitm tools you can check them in your Parrot OS.**_
