---
layout: post
title: "vim skill improve"
decription: "vim skill improve"
tags: [vim]
---
{% include JB/setup %}

A very good tutorial of vim skills improve:

[10 Vim Tutorials to jumpstart your editor skills](http://www.thegeekstuff.com/2010/04/vim-editor-tutorial/)

List my study footprints as below:`strikeout line mean study finish`

* <del>Essential Vim editor navigation commands</del>
  * `h j k l`
  * `0 ^ $ g_`
  * `H M L`
  * `C-f C-b C-d C-u`
  * `N% NG G g '" '^`
  * `e E b B w W`
  * `{ }`
  * `/i ?i * # n N`
  * `%`
* <del>Vim search and replace-12 powerful find and replace examples</del>
  * `:s/\<his\>/her/` Substitute only the whole word and not partial match
  * `:%s/^/\=line(".") . ". "/g` Substituting all lines with its line number
  * `:4,$s/\d\+/\=submatch(0) + 1/` Resort numeric
  * <code>:%s/$/`/g</code> Add backtick to the end of lines
* <del>How To add bookmarks inside the Vim editor</del>
  * `:marks`
  * `mx`
  * `'x`
  * <code>`x</code>
* How To record and play inside the Vim editor
* Correct spelling mistakes automatically inside the Vim Editor
* <del>Automatic word completion using Ctrl-x</del>
  * `C-x C-p` Word completion, backward
  * `C-x C-n` Word completion, forward
  * `C-x C-l` Line completion
  * `C-x C-f` File name completion
* Enable thesaurus option in the Vim editor
* Vim autocommand magic. Add custom header to your files automatically.
* Convert Vim editor to a beautiful source code browser.
* Use the Vim editor as a bash IDE, or C/C++ IDE, or Perl IDE.
