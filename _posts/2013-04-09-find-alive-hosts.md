---
layout: post
title: "find alive hosts"
description: ""
category: 
tags: [network]
---
{% include JB/setup %}

This command can find alive hosts on linux:  
`nmap -v -sn 192.168.1.1/24 | grep 'Nmap scan' | grep -v 'host down'`

Reference:  
* [Nmap扫描原理与用法](http://blog.csdn.net/aspirationflow/article/details/7694274)
* [通过ARP探测局域网活动主机](http://blog.sina.com.cn/s/blog_644eb9350100p3yv.html)
* [编写ARP扫描器探测局域网活动主机](http://www.2cto.com/kf/201011/78750.html)
* [如何获取局域网内其他主机的ip地址和mac地址](http://bbs.csdn.net/topics/350022203)
* [icmp探测活动主机](http://download.csdn.net/detail/joeycc/4945784)
* [利用ICMP数据包探测网络中的活动主机 VC++](http://download.csdn.net/detail/pilipenhuolong/3118860)
* [使用ICMP协议来进行主机探测](http://www.xfocus.net/articles/200103/77.html)
* [一个简单扫描器的实现 ](http://blog.csdn.net/yiyefangzhou24/article/details/6819874)
