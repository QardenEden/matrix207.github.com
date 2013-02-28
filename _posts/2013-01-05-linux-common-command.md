---
layout: post
title: "Linux常用命令技巧"
description:
tags: [linux, shell, git, svn, vim]
---
{% include JB/setup %}

####shell终端命令技巧  

* `!!` 上一个命令, 常用于su或sudo执行上一次命令，如`su !!`  
  相当于`su !-1`,其实就是history显示的命令的倒数第一个，类似的!-2为倒数第二个  
  同类型的技巧: `!^`上一个命令的第一个参数(同`!:1`,其他参数类推)，`!$`最后一个参数

* `C-A/E` 跳到命令头/尾  
  `C-U/K` 截取命令字串至头/尾  
  `C-P/N` 前/后一个命令  
  `C-R`	  历史命令  
  `C--`   缩小  
  `C-L`	  清屏,同`clear`  
  `C-C`	  取消  
  `C-&`	  撤销  
  `C-T`	  交换  
  `C-Y`   粘贴  
  `C-W`   删除一个词  
  下面的操作需要去掉Terminal的Enable menu access keys选项.  
  `C-f/b` 向前/后移动一个字符  
  `M-f/b` 向前/后移动一个字  
  `C-d`	  向前删一个字符  
  `C-h`   向后删一个字符  
  `M-d`   向前删一个单词  
  `C-M-h` 向后删一个单词, 单词之间以符号分割  
  `C-w`   向后删一个单词, 单词之间以空格分割  

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
  `mount -t tmpfs -o size=1024m tmpfs /mnt/ram` 
  映射内存(高速IO操作,磁盘空间不足利用内存)

* `tar xvf example.tar.gz -C /root/test` 解压缩文件到指定目录  
  `tar tvf example.tar.gz` 查看压缩包文件

* `getconf LONG-BIT`           查看系统位数  
  `grep -c "lm" /proc/cpuinfo` 查看cpu位数  

* `df   fdisk -l  du -sh    du -s * |sort -n |tail`
* `free   bg   kill pid    killall proc    chmod 777 (r:4,w:2,x:1)(user,group,all)`

* `find / -name "***"`  
  `find path \( -name "*.h" -or -name "*.c" \) -exec grep -in "***" {} \;`  
  `find / -type d -name "gedit"` 查找目录
* `grep -r "abc" /root/source`  
  `grep -r --include "*.h" "date" path`  
  `grep -m 1 "model name" /proc/cpuinfo` 只匹配第一个  
* `cut -d"" -f1`  
	e.g:  
	`[root@localhost ~]# sensors |grep "Core "`  
	Core 0:       +30.0°C  (high = +76.0°C, crit = +100.0°C)  
	Core 1:       +37.0°C  (high = +76.0°C, crit = +100.0°C)  
	`[root@localhost ~]# sensors |grep "Core " |cut -d"+" -f2 |cut -d" " -f1`  
	30\.0°C  
	37\.0°C  

####awk and sed  
* awk  
  `awk FS'' 'condition1{operator1}condition2{operator2}...' filename`  
  NR:number row, NF:number field  
  `awk 'NR==1{print $0}'`  
  `arr=($(awk -F'#' '{print $1,$2,$3,$4}' $conf_file))`  
  `ps aux | awk 'NR==1{print $0}$3>10{print $0}'`  
  `awk -F'<|>' '{if(NF>3){print $2 ":" $3}}' /tmp/test.xml` 解析显示xml  

* sed  
  `sed [options] 'command' file(s)`  
  `sed [options] -f scriptfile file(s)`  
  `sed -i '/'$prj'/{s/\(.*#.*#\)[0-9]\+/\1'$rev_new'/}' $conf_file`  

* `history|awk '{print $3}'|awk 'begin {FS="1"} {print $1}'|sort|uniq -c|sort -rn|head -10`
* `ps aux | sort -nk +4 | tail`
* `uname -a`
* `rpm -qf /usr/bin/cp`  
  `rpm -ivp ***.rpm`  
* `mkdir -p`


####VIM  
	v|c|d  i|a  {|[\(|"|'  
	qq operator q   100@q  
	:Tlist    C-WW  
	ctags -R   :set tags=..../tags     C-[, C-T  
	cscope -Rb :cs add .../cscope.out :cs find g *** :cs find c ***  
	:cw  
	C-X C-P/N/L  

####git and svn  
* git  
  `git clone url`  
  `git add .`  
  `git commit -m "***"`  
  `git push origin master`  
  `git status`  
  `git rm ***`	remove file  
  `git rm -r ***` remove directory  
  `git pull`  
  `git mv *** ###`  

* svn  
  `svn list url`  
  `svn co url`  
  `svn status`  
  `svn info url`  
  `svn log -r ***:****`  
  `svn commit -m "***"`  
  `svn add ***`  

####network  
* `python -m SimpleHTTPServer`  
* `ssh root@172.168.1.101`  
* `ssh -f -NC -D7070 user@shell.cjb.net` ssh tunnel 
* `scp abc.sh root@172.168.1.101:/root/test` upload file  
  `scp root@172.168.1.101:/root/test/abc.sh /root/mytest` download file  
* `nmap ip`     
  `nmap -v -sn 192.168.1.1/24`  
* `lsof -i:111`
* `curl ifconfig.me`
* `dig domain`   `dig -x host`

####other  
* patch  
  `diff a.c b.c > c.patch`  
  `patch a.c c.patch`  

* `vmstat iostat ifstat nload top hexdump od`

* `dd if=/dev/zero of=$test_file bs=1M count=$dev_size 2>> $log`

* `> file.txt`
* `man ascii`
* `watch -n 5 command`
* `chroot .`

* `date "+%F %R:%S"`       
  `date "+%s"`

* `ldd file` print shared library dependencies
  
  
#### 参考链接
+ [你可能不知道的Shell](http://coolshell.cn/articles/8619.html)
+ [高效操作Bash](http://ahei.info/bash.htm)
+ [Bash readline 使用技巧](http://docs.huihoo.com/homepage/shredderyin/readline.html)
+ [Shell大杂烩](http://floss.zoomquiet.org/item20051011211622-frameset.html)
+ [Check network connection command](http://www.cyberciti.biz/faq/check-network-connection-linux/)
