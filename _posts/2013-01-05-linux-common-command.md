---
layout: post
title: "Linux frequently used commands"
description:
tags: [linux, shell, git, svn, vim]
---
{% include JB/setup %}

####shell terminal
* `!!` the previous command (Actually the latest command list with command `history`)   
  `!-1` is equal to `!!`  
  `!-2` is second command list with command `history`   
  `!^`  first parameter  
  `!:1` first parameter   
  `!:$` last parameter  

* `C-A/E` jump to the head/end position  
  `C-U/K` trim to head/tail  
  `C-P/N` prev/next command  
  `C-R`	  history command  
  `C--`   zoom in  
  `C-L`	  clear screen, same as `clear`  
  `C-C`	  cancel current command  
  `C-&`	  cancel modify  
  `C-T`	  switch  
  `C-Y`   paste  
  `C-W`   delete a word  
  Below operation need to unset Enable menu access keys option of terminal.  
  `C-f/b` move cursor forward/backward a character  
  `M-f/b` move cursor forward/backward a word  
  `C-d`	  delete a character forward  
  `C-h`   delete a character backward  
  `M-d`   delete a word froward  
  `C-M-h` delete a word backward, the word was splited by any special symbols  
  `C-w`   delete a word backward, the word was splited by space symbol only  
  `C-]`   search character forward  
  `C-M-]` search character backward  

* `<alt>+.` get the last parameter of previous command

####common command
* `cd -` switch to last dir  
  `cd` switch to user home dir  

* `cp filename{,.bak}` a fast method to bakup a file

* `time command` count the elapsed time

* `mount -t cifs -o username=***,passwd=*** //ip/path /mnt/test` 
  mount network sharing dir  
  `mount -t iso9660 /mnt/iso/FC17-DVD.iso /mnt/dvd` 
  use for mounting ISO file  
  `mount --bind /root/project/myprj /root/x86_64_build/source` 
  mount a dir to another, use for across-compilation mostly  
  `mount -t tmpfs -o size=1024m tmpfs /mnt/ram`  
  mount memory as a w/r dir (use for high speed I/O operation, and disk space not enough)  

* `tar xvf example.tar.gz -C /root/test` extract files to specific dir  
  `tar tvf example.tar.gz` list the contents of an archive  
  `7z a -t7z -ptestpsw123 mytest.7z -r testfolder/*` zip folder and encrypt it by 7z  

* `getconf LONG-BIT`           check system bits  
  `grep -c "lm" /proc/cpuinfo` check cpu bits

* `du -sh    du -s * |sort -n |tail`

* `free   bg   kill pid    killall proc    chmod 777 (r:4,w:2,x:1)(user,group,all)`

* `find / -name "***"`  
  `find path \( -name "*.h" -or -name "*.c" \) -exec grep -in "***" {} \;`  
  `find / -type d -name "gedit"` search direactorys  
  `find . \( -path ./.git -o -path dir2 \) -prune -o -type d -print` search sub-dir, except .git and dir2  
  `find /usr/include/ -path /usr/include/boost -prune -o -name '*.h' -print >1.txt`  
  `find . -name ".svn" | xargs rm -rf` find .svn folder in current directory, and remove it.  

* `grep -r "abc" /root/source`  
  `grep -r --include "*.h" "date" path`  
  `grep -m 1 "model name" /proc/cpuinfo` only display the first match line    
  `grep -i -E "abc|123"` match abc or 123, -i ignore, -E extended regular expression.  
  `grep -r -l "main" .` search all files under each directory, -l files-with-match, -L files-withou-match  
  `grep -w "linux" *.md` match word  

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
  `awk -F'<|>' '{if(NF>3){print $2 ":" $3}}' /tmp/test.xml` parse xml file  

* sed  
  `sed [options] 'command' file(s)`  
  `sed [options] -f scriptfile file(s)`  
  `sed -i '/'$prj'/{s/\(.*#.*#\)[0-9]\+/\1'$rev_new'/}' $conf_file`  

####VIM  
* `vimdiff a.log b.log` diff two files
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
* `ip addr`  
  `cat /sys/class/net/eth{0,1}/address` display mac address  
* `python -m SimpleHTTPServer`  
* `ssh root@172.168.1.101`  
* `ssh -f -NC -D7070 user@shell.cjb.net` ssh tunnel  
  `ssh -f -NC -D7070 user@216.194.70.6` ssh tunnel 
* `scp abc.sh root@172.168.1.101:/root/test` upload file  
  `scp root@172.168.1.101:/root/test/abc.sh /root/mytest` download file  
  `sshpass -p passwd scp abc.sh root@172.168.1.101:/root/test`
* `nmap ip`  
  `nmap -v -sn 192.168.1.1/24`  
  `nmap -v -sn 192.168.1.1/24 |grep 'report' |grep -v 'down' |awk '{print $NF}'` scan local alive ip  
* `lsof -i:111`  
  `netstat -apn | grep 111`  
  `iptables -A INPUT -p tcp --dport 111 -j DROP` forbid specific port
  `iptables -A OUTPUT -p tcp --dport 111 -j DROP`  
* `curl ifconfig.me`
* `dig domain`   `dig -x host`
* `netstat -nlp` view service and listen ports
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

####Others  
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
* `dmidecode | more`    : view mainboard info   
  `cat /proc/cpuinfo`   : view CPU info  
  `cat /proc/pci`       : view pci info  
  `lspci `              : view PCI info  
  `cat /proc/meminfo`   : view memory info  
  `fdisk -l`            : view disk info  
  `df`                  : view disk space useage  
  `cat /proc/interrupts`: view interrupt request    
  `dmesg | more`        : view device debug message  
  
####Reference
+ [你可能不知道的Shell](http://coolshell.cn/articles/8619.html)
+ [高效操作Bash](http://ahei.info/bash.htm)
+ [Bash readline 使用技巧](http://docs.huihoo.com/homepage/shredderyin/readline.html)
+ [Shell大杂烩](http://floss.zoomquiet.org/item20051011211622-frameset.html)
+ [Check network connection command](http://www.cyberciti.biz/faq/check-network-connection-linux/)
+ [50 Most Frequently Used UNIX / Linux Commands (With Examples)](http://www.thegeekstuff.com/2010/11/50-linux-commands/)
