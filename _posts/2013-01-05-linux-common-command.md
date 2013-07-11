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
  `C-]`   search character forward
  `C-M-]` search character backward

* `<alt>+.`马上得到上一个命令的最后一个参数

####常用系统命令

* `cd -`切回上次目录  
  `cd` 回到用户目录

* `cp filename{,.bak}`快速备份文件

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
  `7z a -t7z -ptestpsw123 mytest.7z -r testfolder/*` zip folder and encrypt it by 7z  

* `getconf LONG-BIT`           查看系统位数  
  `grep -c "lm" /proc/cpuinfo` 查看cpu位数  

* `du -sh    du -s * |sort -n |tail`

* `free   bg   kill pid    killall proc    chmod 777 (r:4,w:2,x:1)(user,group,all)`

* `find / -name "***"`  
  `find path \( -name "*.h" -or -name "*.c" \) -exec grep -in "***" {} \;`  
  `find / -type d -name "gedit"` 查找目录  
  `find . \( -path ./.git -o -path dir2 \) -prune -o -type d -print`查找子目录，.git和dir2除外  
  `find /usr/include/ -path /usr/include/boost -prune -o -name '*.h' -print >1.txt`  
  `find . -name ".svn" | xargs rm -rf` find .svn folder in current directory, and remove it.  

* `grep -r "abc" /root/source`  
  `grep -r --include "*.h" "date" path`  
  `grep -m 1 "model name" /proc/cpuinfo` 只匹配第一个  
  `grep -i -E "abc|123"` 匹配字符串abc或123, -i忽略大小写, -E正则表达式   
  `grep -r -l "main" .` 在当前目录及其子目录搜索main字符串，只列出匹配的文件名, -L列出不匹配的文件名  
  `grep -w "linux" *.md` 只匹配整个单词，而不是字符串的一部分  

* `cut -d"" -f1`  
	e.g:  
	`[root@localhost ~]# sensors |grep "Core "`  
	Core 0:       +30.0°C  (high = +76.0°C, crit = +100.0°C)  
	Core 1:       +37.0°C  (high = +76.0°C, crit = +100.0°C)  
	`[root@localhost ~]# sensors |grep "Core " |cut -d"+" -f2 |cut -d" " -f1`  
	30\.0°C  
	37\.0°C  

* `history|awk '{print $2}'|awk 'begin {FS="|"} {print $1}'|sort|uniq -c|sort -rn|head -10`

* `ps aux | sort -nk +4 | tail`

* `uname -a`

* `rpm -qf /usr/bin/cp`  
  `rpm -ivp ***.rpm`  

* `mkdir -p`

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

####VIM  
* vim  
  `:e` reload current file  
  `:e filename` add a file to editor  
  `:bn` or `:bp` goto the next or previous buffer  
  `:bd!` delete current buffer tag  
  `C-x` or `C-a` minus or add 1 to current digit  
  `wm` open or close netrw and TagList windows  
  `:set syntax=python` manual set syntax language  
  `:nohl` not highlight  
  `:set nu` show number  
  `:set wrap`  
  `:set nowrap`  

####git and svn  
* git  
  `git clone url`  
  `git add .`  
  `git commit -m "***"`  
  `git commit file -m "***"`  
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
  `svn di`
  `svn log -r ***:****`  
  `svn add ***`  
  `svn commit -m "***"`  

####network  
* `python -m SimpleHTTPServer`  
* `ssh root@172.168.1.101`  
* `ssh -f -NC -D7070 user@shell.cjb.net` ssh tunnel  
  `ssh -f -NC -D7070 user@216.194.70.6` ssh tunnel 
* `scp abc.sh root@172.168.1.101:/root/test` upload file  
  `scp root@172.168.1.101:/root/test/abc.sh /root/mytest` download file  
  `sshpass -p passwd scp abc.sh root@172.168.1.101:/root/test`
* `nmap ip`  
  `nmap -v -sn 192.168.1.1/24`  
  `nmap -v -sn 192.168.1.1/24 |grep 'report' |grep -v 'down' |awk '{print $NF}'`用于扫描局域网活动IP
* `lsof -i:111`  
  `netstat -apn | grep 111`  
  `iptables -A INPUT -p tcp --dport 111 -j DROP`通过iptables禁掉端口   
  `iptables -A OUTPUT -p tcp --dport 111 -j DROP`  
* `curl ifconfig.me`
* `dig domain`   `dig -x host`
* `netstat -nlp`查看服务及监听端口 
* `wget url` download file  
  `wget -m -p -np -k -E http://site/path/` mirror the site  
  `wget -A pdf,jpg -m -p -np -k -E http://site/path/` only download pdf and jpg file  

####os
* Fedora  
   `Alt+Tab` switch windows  
   ``Alt+` ``  switch sub-windows  
   `Win` windows key, use to show all application  
   `Win` -> `Space` , search application  

####vimperator(Firfox plugin)
* vimperator  
`:help`  Open help page  
`C-[`    cancel command mode  
`d`      close current page  
`/`      search
`H`      Go back in the browser history  
`gg`     Go to the top of the page	 
`G`      Go to the bottom of the page  
`C-f`    forward page  
`C-b`    backward page  
`y`      Copy the current URL to clipboad  
`p`      Open the URL from current clipboad contents in current buffer  
`P`      Open the URL from current clipboad contents in a new tab buffer  
`r`      Reload current page  
`ZZ`     Quit and save the session  
`C-n`    Go to the next buffer  
`C-p`    Go to the previous buffer  
`gi`     Go to input field  
`g-u`    Go to the parent directory  
`g-U`    Go to the root of the website  
`c`		 Start caret mode.Like vim's normal mode, use `h j k l` to move, and 
press `v` to start visual mode, then press `y` to copy select text.  

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
* `cat /proc/uptime | awk -F. '{d=($1/86400);h=($1%86400)/3600;m=($1%3600)/60;s=($1%60);printf("已运行%d天%d时%d分%d秒\n",d,h,m,s)}'`
* `fuser -u /home`  
  `fuser -v -n tcp 7070`  
* `echo 1 > /proc/sys/kernel/sysrq` enable sysrq  
  `echo "b" > /proc/sysrq-trigger`  reboot  
  `echo "o" > /proc/sysrq-trigger`  shutdown  
  `shutdown -h now`                 shutdown  
* `dmidecode | more`    : 查看mainboard信息  
  `cat /proc/cpuinfo`   : 查看CPU信息  
  `cat /proc/pci`       : 查看板卡信息  
  `lspci `              : 查看PCI信息  
  `cat /proc/meminfo`   : 查看内存信息  
  `fdisk -l`            : 查看系统硬盘信息  
  `df`                  : 查看系统硬盘使用情况  
  `cat /proc/interrupts`: 查看各设备的中断请求(IRQ)  
  `dmesg | more`        : 查看启动硬件检测信息日志  
  
#### 参考链接
+ [你可能不知道的Shell](http://coolshell.cn/articles/8619.html)
+ [高效操作Bash](http://ahei.info/bash.htm)
+ [Bash readline 使用技巧](http://docs.huihoo.com/homepage/shredderyin/readline.html)
+ [Shell大杂烩](http://floss.zoomquiet.org/item20051011211622-frameset.html)
+ [Check network connection command](http://www.cyberciti.biz/faq/check-network-connection-linux/)
+ [50 Most Frequently Used UNIX / Linux Commands (With Examples)](http://www.thegeekstuff.com/2010/11/50-linux-commands/)
