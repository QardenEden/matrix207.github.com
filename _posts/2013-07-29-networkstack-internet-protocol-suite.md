---
layout: post
title: "NetworkStack Internet protocol suite"
description: ""
category: 
tags: [NetworkStack]
---
{% include JB/setup %}

###Introduce
The Internet protocol suite and the layered protocol stack design were in use 
before the OSI model was established. Since then, the TCP/IP model has been 
compared with the OSI model in books and classrooms, which often results in 
confusion because the two models use different assumptions and goals, including 
the relative importance of strict layering.

Layers in the internet protocol suite:( a four-layer model )
Link layer --> Internet layer --> Transport layer --> Application layer

Application layer

    DHCP
    DHCPv6
    DNS
    FTP
    HTTP
    IMAP
    IRC
    LDAP
    MGCP
    NNTP
    BGP
    NTP
    POP
    RPC
    RTP
    RTSP
    RIP
    SIP
    SMTP
    SNMP
    SOCKS
    SSH
    Telnet
    TLS/SSL
    XMPP

Transport layer

    TCP
    UDP
    DCCP
    SCTP
    RSVP

Internet layer

    IP(IPv4,IPv6)
    ICMP
    ICMPv6
    ECN
    IGMP
    IPsec

Link layer

    ARP/InARP
    NDP
    OSPF
    Tunnels(L2TP)
    PPP
    Media access control(Ethernet/DSL/ISDN/FDDI)

###Reference  
+ [Internet protocol suite](http://en.wikipedia.org/wiki/Internet_protocol_suite)
+ [IP/IP协议](http://zh.wikipedia.org/wiki/TCP/IP协议)
