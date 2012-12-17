---
layout: post
title: "hardware monitor"
description: ""
tags: [hardware monitor]
---
{% include JB/setup %}


### Open Hardware Monitor ###
https://code.google.com/p/open-hardware-monitor/
The Open Hardware Monitor is a free open source software that monitors temperature sensors, fan speeds, voltages, load and clock speeds of a computer.

下面介绍如何在windows下使用VC++编写硬件状态监控程序:  
1.修改computer.cs，增加借口，如果GetFanSpeed(),参考生成report的方法获取风扇速度  
2.设置项目生成文件为类库  
3.参考[VC++使用C#的DLL](http://matrix207.github.com/2012/09/16/VC++-Use-CSharp-Dll/)的文章  

