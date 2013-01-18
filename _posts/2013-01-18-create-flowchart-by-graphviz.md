---
layout: post
title: "create flowchart by graphviz"
description: ""
category: 
tags: [graphviz, dot, flowchart]
---
{% include JB/setup %}

On Fedora:  

1. `yum install graphviz`  

2. write test.dot as below:  

		graph example1 {
		Server1 -- Server2
		Server2 -- Server3
		Server3 -- Server1
		}

3. `dot -Tpng test.dot -o test.png`

reference:  
+ [http://www.oschina.net/question/129540_79958](http://www.oschina.net/question/129540_79958)
+ [http://www.graphviz.org/Gallery.php](http://www.graphviz.org/Gallery.php)
+ [http://www.jishurensheng.com/article-hjo8380-8433934.html](http://www.jishurensheng.com/article-hjo8380-8433934.html)
+ [http://www.fxysw.com/thread-1633-1-1.html](http://www.fxysw.com/thread-1633-1-1.html) 

for emacs :  
+ [http://emacser.com/emacs_graphviz_ds.htm](http://emacser.com/emacs_graphviz_ds.htm)
+ [http://tubocurarine.is-programmer.com/posts/27164.html](http://tubocurarine.is-programmer.com/posts/27164.html)
+ [http://www.wanglianghome.org/blog/2006/05/graphviz-introduction.html](http://www.wanglianghome.org/blog/2006/05/graphviz-introduction.html)
