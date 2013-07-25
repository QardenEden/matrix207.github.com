---
layout: post
title: "VIM study log"
description: "VIM study log"
tags: [vim]
---
{% include JB/setup %}
I use a variety of vi(m) commands for my job, so many that I can't always 
remember how to do something that I have done before. Therefore I keep notes 
them here, for my bad memory.

###General command use in VIM
	
	###insert mode
	i insert mode at cursor
	I insert mode at the beginning of Line
	a append after the cursor
	A append at the end ot line 
	o insert bank line below current line
	O insert bank line above current line

	###Cursor move
	h,j,k,l ←, ↓, ↑, →
	w  jump to the head of next word
	W  jump to the head of next word which begin with bank
	e  jump to the end of next word
	E  jump to the end of next word which begin with bank
	b  jump to the head of previous word
	B  jump to the head of previous word which begin with bank
	0  jump to the first character of current line
	$  jump to the end of current line
	^  jump to the first not-white-space character of current line
	g_ jump to the last not-white-space character of current line
	gg jump to the first not-while-space character of first line
	G  jump to the first not-while-space character of last line
	`. jump the position of last edit
	'' jump the previous position of cursor
	H  jump to first line of screen
	M  jump to the middle line of screen
	L  jump to the last line of screen
	%  jump to the match symbol
	{  paragraph backward
	}  paragraph backward
	[  jump to previous 
	]  jump to next
	zt move current line to the top of window
	zz move current line to the center of window
	zb move current line to the bottom of window
	ctrl+e  scroll screen backward
	ctrl+y  scrool screen forward
	ctrl+u  scroll half screen backward
	ctrl+d  scroll half screen backward
	ctrl+f  scrool to next screen
	ctrl+b  scrool to previous screen

	###Edit
	cw change word
	C  change to the end of line
	u  undo
	~  switch case
	gu uppercase select characters
	gU lowercase select characters 
	>> indent line one column right
	<< indent line one column left
	== auto-indent current line
	ctrl+r redo

	###Cut, copy and paste
	dd  delete current line, and put it to clipboard
	x   delete current character
	X   delete previous character
	dw  delete to end of word
	D   delete to end of line
	yy  copy current line
	yw  copy to end of word
	y$  copy to end of line
	p   paste after the cursor
	P   paste befor the cursor
	"+y copy to system clipboard
	"+gP  paste from system clipboard
	[N]yy copy N lines

	###Fold
	zm increase the foldlevel by one
	zM close all open folds
	zr decrease the foldlevel by one
	zR decrease the foldlevel to zero -- all folds will be open
	zo opens a fold at the curse
	zO opens all folds at the curse
	zc close one fold
	zC close all folds at the curse
	zj jump to next fold
	zk jump to previous fold

	###Search
	*        search string forward
	#        search string backward
	/pattern search for pattern
	?pattern search backwards for pattern
	n        repeat search in same direction
	N        repeat search in opposite direction
	f        search character forward
	F        search character backward

	###Save and quit
	:w  save
	:wq save and quit
	:x  save and quit
	:q  quit, fail to quit if not save the changed
	:q! force quit
	ZZ  save and quit

	###File 
	use `vim file1 file2 ...` to open multiple files
	:bn     next buffer
	:bp     previous buffer 
	:e path edit file
	:e      reload current file
	:r cmd  read the result the command to the cursor of current file

	###simple skills
	xp   swap two characters
	gg=G indent the file
	[N]G jump to Nth line
	yyp  copy and paste current line
	yw   yank to the end of word
	yiw  yank word
	=    auto-indent selected lines
	==   auto-indent current lines
	n==  auto-indent [count] lines (start from current line)
	gd   jump to the defined position of variable


	###Other
	. repeat last change
	J join [count] lines

	###substitute
	(use command ":help substitue" for more information)
	:[range]s/pattern/string/[c,e,g,i]
	  range   1,7 line 1 to 7  1,$ line 1 to last  % all lines
	  pattern string  be searched
	  string  string for substitute
	  c	comfirm
	  e	not show error
	  g	global, match all search of current line
	  i	ignore
	e.g.
		:%s/\s\+$//	    delete all spaces between first space to the end of line
		:%s/h14/h12/g   replace h14 to be h12 for all occurrence in the file
		:1,$s/h14/h12/g replace h14 to be h12 from first line to the last line

	###Visual Mode
	(use command ":help v" for more information)
	v      start visual mode per character
	V      start visual mode linewise
	ctrl+v start visual mode blockwise

	###Text object 
	(use command ":help objects" for more information)
	Operator Mapping
	v|c|d       i|a          {|[|(|"|'|w
	visual  Inner Object      Region
	change     An Object      {} [] () 
	delete
	e.g.
	  vi{ : select characters between brace
	  va" : select characters, include double quotes
	  viw : visual a word
	  di“ : delete characters between quotes
	  ci( : change characters between bracket

	###Auto completion
	C-p
	C-n
	C-x C-p Word completion, backward
	C-x C-n Word completion, forward
	C-x C-l Line completion
	C-x C-f File name completion

	###History
	q: enter history commands, then choose and execute the command

	###Marks
	(use command ":help mark-motions" for more information)
	mx     set mark x, x can use a..z characters
	'x     jump to mark x
	:marks show all marks

	###Register
	:reg  view register content
	"0p   paste from register 0
	"1p   paste from register 1

	###Complex repeats
	qq operators q   record all operators to q register
	100@q            repeat the operators 100 times
	
	###Editing Files in other places
	vim scp://[user@]hostname[:port]//FilePath
	e.g.: vim scp://root@172.16.110.39//root/a.c

	###Help
	:help symbol


###some skills

1. command mode type `:nohl` cancel high light

2. substituttion  
sample lines:  
> \+ (http://www.google.com)\[google\]  
> \+ (http://www.wolframalpha.com/)\[wolfram\]  
into the lines:  
> \+ \[google\](http://www.google.com)  
> \+ \[wolfram\](http://www.wolframalpha.com/)  
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

11. read range of lines from another file to current file 
	`:r! sed -n 100,158p /home/dennis/test.c`

12. list all the match lines of searching on screen 
	`:g/pattern/p` In its longer format: `:global/regular-expression/print`  
	If `pattern` is leave out, like `:g//p`, vim will uses previous search item.  
	You can leave `p` out too, because p(rint) is the default action.

###other valued skills
* [vim notes](http://www.brezeale.com/technical_notes/vim_notes.shtml)
* [VimTip - Vim Tips Wiki](http://vim.wikia.com/wiki/Category:VimTip)
* [Best Vim Tips](http://vim.wikia.com/wiki/Best_Vim_Tips)
* [Best of Vim Tips](http://www.rayninfo.co.uk/vimtips.html)
* [12 Powerful Find and Replace Examples](http://www.thegeekstuff.com/2009/04/vi-vim-editor-search-and-replace-examples/)
