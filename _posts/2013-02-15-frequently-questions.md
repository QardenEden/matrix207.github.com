---
layout: post
title: "frequently questions"
description: ""
category: 
tags: [FAQ]
---
{% include JB/setup %}

[Install flash on fedora](http://www.if-not-true-then-false.com/2010/install-adobe-flash-player-10-on-fedora-centos-red-hat-rhel/)  
1. Adobe Flash Player 11.2 on Fedora 18/17  

	1). Install Adobe YUM Repository RPM package
	## Adobe Repository 64-bit x86_64 ##
	rpm -ivh http://linuxdownload.adobe.com/adobe-release/adobe-release-x86_64-1.0-1.noarch.rpm
	rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-adobe-linux

	2). Update Repositories
	yum check-update
	
	3). Install
	yum install flash-plugin nspluginwrapper alsa-plugins-pulseaudio libcurl

