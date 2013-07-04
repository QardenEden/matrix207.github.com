---
layout: post
title: "VIM study log"
description: "VIM study log"
tags: [vim]
---
{% include JB/setup %}
I use a variety of vi(m) commands for my job, so many that I can't always remember how to do something that I have done before. Therefore I keep notes them here, for my bad memory.

###General command use in VIM
	
	<C-*> = Ctrl *

	###基本操作
	gg 	  第一行第一个字符处
	G	  末行第一个字符处

	<C-f> <C-b> 往后(前)翻页 

	^ $   跳到当前行首(末)端字符处.
	0 |   跳到当前行第一个字符前.
	w b   往后(前)移动到下一个单词
	e     移动到单词末尾
	u     撤销操作
	<C-R> 还原被撤消的编辑操作
	%     跳到匹配的大中小括号{}[]() #if #endif
	i     在光标前插入
	I     在当前行第一个非空白符号前插入
	a     在光标后插入
	A     在行尾插入
	o O   在行后(前)插入一行,并进入插入模式
	dd    删除当前行
	yy    复制当前行
	yyp   复制并粘贴当前行
	yw    复制单词
	yiw   复制单词
	<< >> 当前行左(右)缩进
	n<< n>> 从当前行起n行 左(右)缩进
	=     格式化选中的代码
	==    格式化当前行
	n==   格式化n行(从当前行算起)
	gg=G  格式化整个文件

	gu    uppercase select characters
	gU    lowercase select characters 

	C   修改到行尾,并进入插入模式
	D   删除到行尾

	xp	交换两个字符

	ZZ	保存退出.(可以替换:wq)
	:e!	重新载入原始文件

	.   重复上一个编辑操作

	J 合并两行

	H (shift+h) 视窗第一行
	M (shift+m) 视窗中间行
	L (shift+l) 视窗末行

	ctrl+e	向上滚屏	
	ctrl+y	向下滚屏
	ctrl+u	向下滚半屏
	ctrl+d	向上滚半屏
	ctrl+f	向前滚动整屏
	ctrl+b	向后滚动整屏

	// 查找替换功能
	f(F) h a
	  查找当前行当前位置往后(或往前)的第一个h字符后,然后进入插入模式
	  f : Find, 查找. f往后查找, F往前查找 
	  h : 要查找的字符
	  a : append 在字符的后面追加(同时进入插入模式)

	查找后
	n 下一个
	N 上一个

	:[range]s/pattern/string/[c,e,g,i]
	  r 	范围, 
	  	1,7表示第一到第七行.
	  	1,$表示第一到最后一行.
	  	%  表示整篇文章
	  pattern 被替换的字串
	  string 替换用的字串
	  c	comfirm, 询问确认
	  e	不显示error
	  g	globe, 不询问,整行替换.
	  i	ignore, 不区分大小写.
	例子:
		:%s/\s\+$//	删除每行后面多余的空格
		:%s/h14/h12/g 替换整个文档中的h14为h12
		:1,$s/h14/h12/g 替换整个文档中(第一行到最后一行)的h14为h12

	替换文本中的h14为h12(只有一处)(可以利用n.来找到下一个h14并重复替换操作)
	/h14[enter]er2
	或
	/h14[enter]2lr2

	###copy and paste
	"+y  复制
	"+gP 粘贴

	[或] 用来移动到所属的 {或}
	{或} 向前(或后)移动到空白行

	Visual Mode (视图模式)
	v 进入字符视图选取模式 
	V 进入行视图选取模式
	<C-v> 进入列选取模式

	Operator Mapping
	v|c|d       i|a          {|[|(|"|'|w
	visual  Inner Object      Region
	change     An Object      {} [] () 
	delete
	例如:
	  vi{ : 选中大括号内(不包括大括号本身)全部内容
	  va" : 选中双引号(包括双引号本身)全部内容
	  viw : visual a word
	  di“ : 光标移动到双引号内,用来删除双引号的全部字串
	  ci( : 光标移动到小括号内,用来修改小括号的全部字串,可以用来修改函数的全部参数

	gd 可以跳转到当前光标所在的单词(变量)的局部定义处

	###命令跳转
	* zt 当前行至窗口首行
	* zz 当前行至窗口中间
	* zb 当前行至窗口末尾

	###折叠
	* zm increase the foldlevel by one
	* zM close all open folds
	* zr decrease the foldlevel by one
	* zR decrease the foldlevel to zero -- all folds will be open
	* zo opens a fold at the curse
	* zO opens all folds at the curse
	* zc close one fold
	* zC close all folds at the curse
	* zj jump to next fold
	* zk jump to previous fold

	###多文档跳转
	* :bp 前一个文档
	* :bn 后一个文档

	###搜索替换
	* `:%s/Matirx207/Matrix207/g`, 全文搜索`Matirx207`替换为`Matrix207`

	###自动补齐
	* C-P, 即Ctrl+P, 自动补齐上个可能字
	* C-N, 即Ctrl+N, 自动补齐下个可能字
	* C-x C-p Word completion, backward
	* C-x C-n Word completion, forward
	* C-x C-l Line completion
	* C-x C-f File name completion


	###历史命令
	* q: enter history commands
	* move by hjkl, type enter to execute the command

	###标签
	* mx     set mark x, x can use a..z characters
	* 'x     jump to mark x
	* :marks show all marks

	###寄存器
	* 输入:reg 查看寄存器内容
	* 输入 "寄存器名p 即可粘贴相应的寄存器内容

	###宏操作录制
	* qq operator q
	* 100@q
	
	###Editing Files in other places
	vim scp://[user@]hostname[:port]//FilePath
	e.g.: vim scp://root@172.16.110.39//root/a.c


###some skills

1. command mode type `:nohl` cancel high light

2. substituttion  
sample lines:  
> \+ (http://emacser.com/org-mode.htm)\[Emacs org mode学习笔记\]  
> \+ (http://www.cnblogs.com/holbrook/archive/2012/04/12/2444992.html#sec-3-5)\[org-mode，最好的文档编辑利器，没有之一\]  
> \+ (http://emacser.com/org-mode-tricks.htm)\[Org-mode写作的几个快捷方式\]  
> \+ (http://i.linuxtoy.org/docs/guide/ch32.html)\[组织你的意念：Emacs org mode\]  
into the lines:  
> \+ \[Emacs org mode学习笔记\](http://emacser.com/org-mode.htm)  
> \+ \[org-mode，最好的文档编辑利器，没有之一\](http://www.cnblogs.com/holbrook/archive/2012/04/12/2444992.html#sec-3-5)  
> \+ \[Org-mode写作的几个快捷方式\](http://emacser.com/org-mode-tricks.htm)  
> \+ \[组织你的意念：Emacs org mode\](http://i.linuxtoy.org/docs/guide/ch32.html)  
Here is the command to do this:  
`:%s/+ \(.*\)\(\[.*\]\)/+ \2\1/g`  

3. compare file  
   `vimdiff file1 file2` or `gvim -d file1 file2`

4. digit operator  
	`ctrl+a` increment 1  
	`ctrl+x` subtract 1  

5. delete all comments  
	`:%s/\/\*\_.\{-}\*\//g` or `:%s#\M/*\m\_.\{-}\M*/##g`

6. delete match lines  
	`:g/.*patternSearch.*/d`

7. more substitution  
	Substituting all lines with its line number  
	`:%s/^/\=line(".") . ". "/g`  
	Resort numeric  
	`:4,$s/\d\+/\=submatch(0) + 1/`  

8. delete bank line
	`:g/^$/d`  
	`:g/^ *$/d` delete lines only contain space   

9. add "inline" to all function  
	`:%s/\(.*(\)/inline \1/g`  this can work, but not perfect!!    
	`%s/\(^[□tab]*\)\(.*(.*\)/\1inline \2/g`  

10. delete all spaces at the end of every line:
	`:%s/\(.*\)  *$/\1/`

###other valued skills
* [vim notes](http://www.brezeale.com/technical_notes/vim_notes.shtml)
* [Best of Vim Tips](http://www.rayninfo.co.uk/vimtips.html)
* [Vi and Vim Editor: 12 Powerful Find and Replace Examples](http://www.thegeekstuff.com/2009/04/vi-vim-editor-search-and-replace-examples/)
