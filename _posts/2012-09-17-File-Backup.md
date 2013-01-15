---
layout: post
title: "File Backup Study"
description: "collect information of file backup."
category:
tags: [FileBackup]
---
{% include JB/setup %}

#### Defined of File Backup

You can make it three type as below:
* Full only
* Incremental
* Differential

####假设有一文本文件1.txt，内容如下:  
	abcd789123jka
	asdfiuqwoiuer
	qwer897234-089---==235498

第一次备份,进行完全备份1.txt，得到B.txt(B.txt与1.txt相同)

####即设现在1.txtx被修改了,内容如下:
	abcd789123jka
	asdfiuqwoiuer
	qwer897234-089---==235498
	1234

* 修改后，如果做增量备份,得到B^+1.txt,内容为:  
	1234

* 修改后，如果做差异备份,得到B^-1.txt,内容为:  
	1234


####即设现在1.txtx被修改了,内容如下:
	abcd789123jka
	asdfiuqwoiuer
	qwer897234-089---==235498
	1234
	AAAA

* 修改后，如果做增量备份,得到B^+2.txt,内容为:  
	1234
	AAAA

* 修改后，如果做差异备份,得到B^-2.txt,内容为:  
	AAAA

#### Reference
[http://en.wikipedia.org/wiki/Backup](http://en.wikipedia.org/wiki/Backup)

