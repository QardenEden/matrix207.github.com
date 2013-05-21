---
layout: post
title: "Do you really master c language"
description: ""
category: 
tags: [C]
---
{% include JB/setup %}

#1. Array
#2. point
#3. structure
##3.1 
	struct pid_tag {
		unsigned int inactive : 1;
		unsigned int          : 1; /* fill 1 bit */
		unsigned int refcount : 6;
		unsigned int          : 0; /* fill to next word */
        short pid_id;
		struct pid_tag *link;
	}

##3.2 alignment

	struct st_a {
		int a;
		char b;
		short c;
	};

	struct st_b {
		char b;
		short c;
		int a;
	};

	struct st_c {
		char b;
		int a;
		short c;
	};

	the value of sizeof(st_a) is 8  (address: 0 1 2 3 | 4 . | 6 7)
	the value of sizeof(st_b) is 8  (address: 0 . | 2 3 | 4 5 6 7)
	the value of sizeof(st_c) is 12 (address: 0 . . . | 4 5 6 7 | 8 9 . .)

Therefore, you should careful for doing structure copy, and socket programming.


#4. Function

#3. For more : 
* [Top votes of c questions on stackoverflow](http://stackoverflow.com/questions/tagged/c?sort=votes&pagesize=15)
* [如何学好C语言](http://coolshell.cn/articles/4102.html)
* [C语言的谜题](http://coolshell.cn/articles/945.html)
* [谁说C语言很简单？](http://coolshell.cn/articles/873.html)
* [Why do all these crazy function pointer definitions all work? What is really going on?](http://stackoverflow.com/questions/6893285/why-do-all-these-crazy-function-pointer-definitions-all-work-what-is-really-goi)
* [small c project](http://programmers.stackexchange.com/questions/62502/small-c-projects)
* [结构体内存对齐](http://blog.csdn.net/zhaori/article/details/7659268)
