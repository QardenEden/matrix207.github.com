---
layout: post
title: "maxima tutorial"
description: ""
category: 
tags: [maxima]
---
{% include JB/setup %}

1. 安装 `yum install maxima`
2. 运行 `maxima`

		[root@localhost ~]# maxima --version
		Maxima 5.29.1
		[root@localhost ~]# maxima
		Maxima 5.29.1 http://maxima.sourceforge.net
		using Lisp SBCL 1.1.2-1.fc18
		Distributed under the GNU Public License. See the file COPYING.
		Dedicated to the memory of William Schelter.
		The function bug_report() provides bug reporting information.
		(%i1) 2+3;
		(%o1)                                  5
		(%i2) 1/3;
		                                       1
		(%o2)                                  -
		                                       3
		(%i3) float(1/3);
		(%o3)                          .3333333333333333
		(%i4) sum(i^2, i, 1, 3);
		(%o4)                                 14
		(%i5) ? if

		 -- Special operator: if
			 Represents conditional evaluation.  Various forms of `if'
			 expressions are recognized.

			 `if <cond_1> then <expr_1> else <expr_0>' evaluates to <expr_1> if
			 <cond_1> evaluates to `true', otherwise the expression evaluates
			 to <expr_0>.

			 The command `if <cond_1> then <expr_1> elseif <cond_2> then
			 <expr_2> elseif ... else <expr_0>' evaluates to <expr_k> if
			 <cond_k> is `true' and all preceding conditions are `false'.  If
			 none of the conditions are `true', the expression evaluates to
			 `expr_0'.

			 A trailing `else false' is assumed if `else' is missing.  That is,
			 the command `if <cond_1> then <expr_1>' is equivalent to `if
			 <cond_1> then <expr_1> else false', and the command `if <cond_1>
			 then <expr_1> elseif ... elseif <cond_n> then <expr_n>' is
			 equivalent to `if <cond_1> then <expr_1> elseif ... elseif
			 <cond_n> then <expr_n> else false'.

			 The alternatives <expr_0>, ..., <expr_n> may be any Maxima
			 expressions, including nested `if' expressions.  The alternatives
			 are neither simplified nor evaluated unless the corresponding
			 condition is `true'.

			 The conditions <cond_1>, ..., <cond_n> are expressions which
			 potentially or actually evaluate to `true' or `false'.  When a
			 condition does not actually evaluate to `true' or `false', the
			 behavior of `if' is governed by the global flag `prederror'.  When
			 `prederror' is `true', it is an error if any evaluated condition
			 does not evaluate to `true' or `false'.  Otherwise, conditions
			 which do not evaluate to `true' or `false' are accepted, and the
			 result is a conditional expression.

			 Among other elements, conditions may comprise relational and
			 logical operators as follows.

				  Operation            Symbol      Type

				  less than            <           relational infix
				  less than            <=
					or equal to                    relational infix
				  equality (syntactic) =           relational infix
				  negation of =        #           relational infix
				  equality (value)     equal       relational function
				  negation of equal    notequal    relational function
				  greater than         >=
					or equal to                    relational infix
				  greater than         >           relational infix
				  and                  and         logical infix
				  or                   or          logical infix
				  not                  not         logical prefix


		  There are also some inexact matches for `if'.
		  Try `?? if' to see them.

		(%o5)                                true
		(%i6) 
		(%i6) quit ();
		[root@localhost ~]# 

网络相关教程资源:  
+ [Maxima 5.28.0 Manual](http://maxima.sourceforge.net/docs/manual/en/maxima.html)
+ [Linux下的数学工具Maxima 简明教程 上](http://www.matrix67.com/blog/archives/337)
+ [Linux下的数学工具Maxima 简明教程 下](http://www.matrix67.com/blog/archives/338)
