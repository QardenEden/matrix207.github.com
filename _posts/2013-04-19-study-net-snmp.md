---
layout: post
title: "study net snmp"
description: ""
category: 
tags: [net-snmp]
---
{% include JB/setup %}
## 1.Architecture
#### 1.1 Agent Architecture
Upon starting, the agent goes through the following steps (in SnmpDaemonMain()):

* reads command line options
* decides whether it's a master or subagent
* calls init_agent()
  + initializes the mib-module registration tree
  + registers its own configuration file tokens and callbacks
  + initializes the Agent Helpers 
* initializes all the compiled-in mib modules
* initializes the base libnetsnmp library
* opens all the required ports to listen on
* forks
* saves persistent data (it's likely at least something has changed already)
* sends a coldStart trap
* invokes receive() to perform the main packet handling 

Reference: [Agent_Architecture](http://www.net-snmp.org/wiki/index.php/Agent_Architecture)

####  1.2 snmpget snmpwalk
Reference: [mib2c_General_Overview](http://www.net-snmp.org/wiki/index.php/TUT:mib2c_General_Overview)

	* snmptranslate: learning about the MIB tree.
	* snmpget: retrieving data from a host.
	* snmpgetnext: retrieving unknown indexed data.
	* snmpwalk: retrieving lots of data at once!
	* snmptable: displaying a table.
	* snmpset: peforming write operations.
	* snmpbulkget: communicates with a network entity using SNMP GETBULK request
	* snmpbulkwalk: retrieve a sub-tree of management values using SNMP GETBULK requests.
	* snmptrap: Sending and receiving traps, and acting upon them.

example: 

	[dennis@localhost ~]$ snmpwalk -v2c -c public 192.168.110.98 .1.3.6.1.4.1.30901
	...
	SNMPv2-SMI::enterprises.30901.1.1.2.5.1.3.1 = INTEGER: 856398
	SNMPv2-SMI::enterprises.30901.1.1.2.5.1.4.1 = INTEGER: 432164
	SNMPv2-SMI::enterprises.30901.1.1.2.5.1.5.1 = INTEGER: 424234
	SNMPv2-SMI::enterprises.30901.1.1.2.5.1.6.1 = INTEGER: 1
	SNMPv2-SMI::enterprises.30901.1.1.2.5.1.7.1 = INTEGER: 3
	SNMPv2-SMI::enterprises.30901.1.1.2.5.1.8.1 = STRING: "0:1 0:2 0:3 "
	SNMPv2-SMI::enterprises.30901.1.1.2.5.1.9.1 = INTEGER: 3
	SNMPv2-SMI::enterprises.30901.1.1.2.5.1.10.1 = INTEGER: 0
	SNMPv2-SMI::enterprises.30901.1.1.2.5.1.11.1 = INTEGER: 4
	SNMPv2-SMI::enterprises.30901.1.1.2.5.1.12.1 = INTEGER: 0
	SNMPv2-SMI::enterprises.30901.1.1.2.5.1.13.1 = INTEGER: 5
	[dennis@localhost ~]$ snmpget -v2c -c public 192.168.110.98 .1.3.6.1.4.1.30901.1.1.2.5.1.3.1
	SNMPv2-SMI::enterprises.30901.1.1.2.5.1.3.1 = INTEGER: 856398
	[dennis@localhost ~]$ snmpget -v2c -c public 192.168.110.98 .1.3.6.1.4.1.30901.1.1.2.5.1.8.1
	SNMPv2-SMI::enterprises.30901.1.1.2.5.1.8.1 = STRING: "0:1 0:2 0:3 "

## 2. Install
####  2.1 Yum 
__install snmp__  
`su -c 'yum install net-snmp'`

__install mib2c__  
`su -c 'yum install net-snmp-perl'`

## 3. Steps
####  3.1 [net-snmp中如何加自定义的mib库](http://bbs.csdn.net/topics/300080590)
* 先完成你的mib数据库文件
* 把它放到/usr/share/snmp/mibs目录
* 用snmptranslate -Ts -m ALL 就可以看到所以OID的输出了，当然也包括你新加的。  
  如果写的mib文件不正确，应该不能输出，你可以找第三方工具来验证你的文件格式是否正确。
* 编写相关的函数。
  + 为你的mib新建一个c文件，可以使用mib2c这样的工具来完成。
  + 如果该OID是只读的，那就在该文件里编写一个只读的函数（mib2c应该会生成的）；如果可写，也应该有一个写的函数（相样是生成的）

## 4. Use mib2c
####  4.1 mib object
scalar: int,  string,  time and so on.  
table : table has row and column, like table in database.  

####  4.2 use mib2c to create source file
__append string "DENNIS-MIB" to config file: snmp.conf__   
`su -c 'vim /etc/snmp/snmpd.conf'`  

__copy mib file to mibs directory__  
`su -c 'cp DENNIS-MIB.txt /usr/share/snmp/mibs/'`  

__generate c source file by mib2c__  
`mib2c -c mib2c.scalar.conf DENNIS-MIB::dennis`  for scalar object  
`mib2c -c mib2c.iterate.conf DENNIS-MIB::dennis` for table  object   
if failed to translate, check the mibs directory again, or look the output message.

## 5. Add self-defined mib library
####  5.1 steps:
使用net-snmp扩展私有MIB的大致方法  
参考： [net-snmp tutorial](http://net-snmp.sourceforge.net/tutorial/tutorial-5/toolkit/mib_module/index.html)

step 1. 首先需要使用net-snmp的相关API编写MIB相关C代码，

	1. MFD/mib2c：这是一种通过net-snmp提供的mib2c程序自动生成相关代码的方式
	2. A simple scalar attached to a variable：适合于简单变量类型的object
	3. A simple scalar with the value returned from code：适用于任何变量类型的object

step 2. 然后将刚写的MIB C code编译进net-snmp，有几种方法：

	1. compile it into master agent：
	  1）将刚编写的码加入net-snmp的src目录，
	  2）通过configure的option指示make编译该mib，
	     如./configure --with-mib-modules="myobject" 
	  3）make
	  4）make install
      这样，你的MIB就已经被内置如snmp服务程序中了，MIB的生效也就理所当然

	2. compile your code into a “subagent”：
	  这种方式可以将subagent通过agentx协议与master agent通信，
	  参考： http://net-snmp.sourceforge.net/tutorial/tutorial-5/toolkit/demon/index.html
	  这种情况subagent最终是一个独立的application，包含两种生成方式，
	  1).是通过net-snmp-config工具生成；
	  2).是自己编写程序控制调用；
	  后者更为灵活，subagent功能可以被集成在其它application中。

	3. compile your code into pluggable shared object and tell the snmpd agent to load it
      这种方式最后生成一个.so的共享库，用户启动snmpd服务时可以通过指定参数的方式
	  加载该共享库以扩展MIB，
      参考： http://net-snmp.sourceforge.net/tutorial/tutorial-5/toolkit/dlmod/index.html 

####  5.2 compile net-snmp by shell script
	cd /home/dennis/net-snmp-5.4.2/
	cp -f /home/dennis/dennis.{h,c} ./agent/mibgroup
	./configure --prefix=/usr --with-mib-modules="dennis"
	make clean
	make
	make install
 
####  5.3 update mib
	copy "net-snmp-5.4.2/agent/.libs/libnetsnmpmibs.so" to "/usr/lib/"

## 6. Reference
####  6.1 network link
* [net-snmp之利用pass做snmpget和snmpset](http://imxie.net/2011/07/use_pass_for_snmp_get_and_set.htm)
* [自定义SNMP Agent](http://www.linuxfly.org/post/556/)
* [net-snmp中如何加自定义的mib](http://bbs.csdn.net/topics/300080590)
* [Extending the UCD-SNMP(net-snmp)agen](http://blog.csdn.net/linyt/article/details/2842244)
* [Tutorial](http://www.net-snmp.org/wiki/index.php/Tutorials)
* [Writing a MIB Module](http://www.net-snmp.org/wiki/index.php/TUT:Writing_a_MIB_Module)
* [Writing a net-snmp MIB Modul](http://net-snmp.sourceforge.net/tutorial/tutorial-5/toolkit/mib_module/index.html)
* [在net-snmp agent中扩展自己的mi](http://blog.csdn.net/bearfig/article/details/2080421)
* [用NET-SNMP软件包开发简单客户端代理★★★★](http://bibu.bokee.com/inc/net_snmp_doc.htm)
* [利用NET-SNMP开发代理(原创](http://bibu.bokee.com/inc/net_snmp_doc.htm#_Toc116812027)
* [Extending the UCD-SNMP(net-snmp) agen](http://blog.csdn.net/linyt/article/details/2842244)
* [第一次寫MIB就上手★★★★](http://www.tonylin.idv.tw/dokuwiki/doku.php/snmp:snmp:mibhelloworld)

