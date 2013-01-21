---
layout: post
title: "create flowchart by graphviz"
description: ""
category: 
tags: [graphviz, dot, flowchart]
---
{% include JB/setup %}

On Fedora:  

1.  `yum install graphviz`  

2.  write test.dot as below:  

		graph example1 {
		Server1 -- Server2
		Server2 -- Server3
		Server3 -- Server1
		}

3.  `dot -Tpng test.dot -o test.png`  
	`dot -Tsvg test.dot -o test.svg`

4. `rsvg-convert -f pdf -o test.pdf test.svg`  convert svg to pdf

reference:  
+ [http://www.oschina.net/question/129540_79958](http://www.oschina.net/question/129540_79958)
+ [http://www.graphviz.org/Gallery.php](http://www.graphviz.org/Gallery.php)
+ [http://www.jishurensheng.com/article-hjo8380-8433934.html](http://www.jishurensheng.com/article-hjo8380-8433934.html)
+ [http://www.fxysw.com/thread-1633-1-1.html](http://www.fxysw.com/thread-1633-1-1.html) 
+ [http://www.wanglianghome.org/blog/2006/05/graphviz-introduction.html](http://www.wanglianghome.org/blog/2006/05/graphviz-introduction.html)
+ [http://superuser.com/questions/381125/how-do-i-convert-an-svg-to-a-pdf-on-linux](http://superuser.com/questions/381125/how-do-i-convert-an-svg-to-a-pdf-on-linux)

for emacs :  
+ [http://emacser.com/emacs_graphviz_ds.htm](http://emacser.com/emacs_graphviz_ds.htm)
+ [http://tubocurarine.is-programmer.com/posts/27164.html](http://tubocurarine.is-programmer.com/posts/27164.html)

external link :   
+ [http://forum.ubuntu.org.cn/viewtopic.php?f=63&t=374855](http://forum.ubuntu.org.cn/viewtopic.php?f=63&t=374855)


