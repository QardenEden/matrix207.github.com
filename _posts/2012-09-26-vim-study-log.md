---
layout: post
title: "VIM study log"
description: "VIM study log"
tags: [vim]
---
{% include JB/setup %}

###The usefull skill about use VIM, and continue to update regulary.

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
`%s/+ \(.*\)\(\[.*\]\)/+ \2\1/g`

3. compare file  
   `vimdiff file1 file2` or `gvim -d file1 file2`

4. digit operator  
	`ctrl+a` increment 1  
	`ctrl+x` subtract 1  
