---
layout: post
title: "frequently questions"
description: ""
category: 
tags: [FAQ]
---
{% include JB/setup %}

### Adobe Flash Player 11.2 on Fedora 18/17  
1). Install Adobe YUM Repository RPM package  
`rpm -ivh http://linuxdownload.adobe.com/adobe-release/adobe-release-x86_64-1.0-1.noarch.rpm`  
`rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-adobe-linux`  

2). Update Repositories  
`yum check-update`

3). Install  
`yum install flash-plugin nspluginwrapper alsa-plugins-pulseaudio libcurl`

参考:  
* [Install flash on fedora](http://www.if-not-true-then-false.com/2010/install-adobe-flash-player-10-on-fedora-centos-red-hat-rhel/)  


### play music and movies  
1). add yum repository  
`su -c 'yum localinstall --nogpgcheck http://mirrors.163.com/rpmfusion/free/fedora/rpmfusion-free-release-stable.noarch.rpm http://mirrors.163.com/rpmfusion/nonfree/fedora/rpmfusion-nonfree-release-stable.noarch.rpm'`

2). install mp3 and other audio support  
`su -c 'yum install gstreamer-plugins-good gstreamer-plugins-bad gstreamer-plugins-ugly libtunepimp-extras-freeworld xine-lib-extras-freeworld'`

3). install video support  
`su -c 'yum install ffmpeg ffmpeg-libs gstreamer-ffmpeg libmatroska xvidcore'`

问题:  
	获取 GPG 密钥失败：[Errno 14] Could not open/read file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rpmfusion-free-fedora  
解决:  
	打开fusion源官网上的密钥页面：http://rpmfusion.org/keys  
	下载 RPM Fusion free for Fedora 18 对应的版本RPM-GPG-KEY-rpmfusion-free-fedora-18  
	`su -c 'rpm --import '/home/XXX/RPM-GPG-KEY-rpmfusion-free-fedora-18''`  
参考:  
* [Fedora 17 无法播放mp3 rmvb](http://www.linuxidc.com/Linux/2012-06/62112.htm)  
* [获取 GPG 密钥失败](http://blog.csdn.net/grantxx/article/details/8509480)  
