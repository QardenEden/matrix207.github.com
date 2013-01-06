---
layout: post
title: "vim english dict"
description: ""
category: 
tags: []
---
{% include JB/setup %}

####vim英文字典#### 

* 下载字典  
	地址:[http://www.vim.org/scripts/script.php?script_id=195](http://www.vim.org/scripts/script.php?script_id=195)

* 解压缩所需字典文件 `tar xvf ~/Downloads/engspchk.tar.gz CVIMSYN/engspchk.dict`  

* 使用vim整理成字典文件 `vim CVIMSYN/engspchk.dict`  
	删除前面三行: `gg3dd`  
	删除行首GoodWord单词: `:%s/^GoodWord\t//g`  
	整理成每个单词占一行: `:%s/\t//g`  
	删除最后一行: `Gdd`  
	排序: `:sort`  

* 拷贝字典文件到指定目录  
	`mkdir /usr/share/vim/vim73/dict`    
	`cp CVIMSYN/engspchk.dict /usr/share/vim/vim73/dict/english.dict`  

* 设置.vimrc文件  
	`setlocal dictionary+=$VIMRUNTIME/dict/english.dict`

* 英文单词自动补全快捷键  
	Ctrl+X Ctrl+K

