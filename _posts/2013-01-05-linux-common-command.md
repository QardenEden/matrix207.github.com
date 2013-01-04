---
layout: post
title: "Linux常用命令技巧"
description:
tags: [linux, shell]
---
{% include JB/setup %}

####shell终端命令技巧  

* `!!` 上一个命令, 常用于su或sudo执行上一次命令，如`su !!`，相当于`su !-1`  
  其实就是history显示的命令的倒数第一个，类似的到!-2为倒数第二个  
  同类型的技巧: `!^`上一个命令的第一个参数(同`!:1`,其他参数类推)，`!$`最后一个参数

* `cd -`切回上次目录  
  `cd` 回到用户目录

* `cp filename{,.bak}`快速备份文件

* `<alt>+.`马上得到上一个命令的最后一个参数

* `time command`计算命令运行时间

* mount命令  
  `mount -t cifs -o username=***,passwd=*** //ip/path /mnt/test` 
  挂载网络共享目录  
  `mount -t iso9660 /mnt/iso/FC17-DVD.iso /mnt/dvd` 
  挂载iso文件  
  `mount --bind /root/project/myprj /root/x86_64_build/source` 
  一个目录挂载到另外一个目录, 交叉编译的时候省掉文件拷贝  

* `tar xvf example.tar.gz -C /root/test` 解压缩文件到指定目录

* `getconf LONG-BIT`           查看系统位数  
  `grep -c "lm" /proc/cpuinfo` 查看cpu位数  

* `Ctrl+L`清屏, 等价与`clear`
* `python -m SimpleHTTPServer` 快速共享当前目录方式
* `ssh root@172.168.1.101` ssh登陆远程主机  
* `scp abc.sh root@172.168.1.101:/root/test` 上传文件  
  `scp root@172.168.1.101:/root/test/abc.sh /root/mytest` 下载文件
* `mount -t tmpfs -o size=1024m tmpfs /mnt/ram` 映射内存(高速IO操作,磁盘空间不足利用内存)

#### TODO
* find
* grep
* awk
* sed
* dd

#### 参考链接
[你可能不知道的Shell](http://coolshell.cn/articles/8619.html)
