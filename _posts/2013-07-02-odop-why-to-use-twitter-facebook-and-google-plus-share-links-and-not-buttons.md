---
layout: post
title: "ODOP Why to use Twitter, Facebook and Google Plus share links and not buttons"
description: ""
category: 
tags: [ODOP]
---
{% include JB/setup %}
From <http://www.garron.me/en/blog/provide-share-buttons-without-exposing-your-visitors.html>

Written by [Guillermo Garron](http://www.garron.me/en/about.html).

Date: 2013-06-30 22:22:35 +0000

##Introduction

Providing not providing share buttons in you posts is something that some consider useful while others consider is not necesary. The arguments are:

###In favor
+ You are giving your visitors an easy way to share your content, if then want to 

###Against
+ If someone wants to share your content, in fact if someone find it good enough to deserve sharing it with their social groups, he will find the way to do it.

But I am not going to discuss if you should or should not insert sharing buttons in your blog, what I am going to show you here is how to do it with out exposing your visitors to the big groups of the Internet, yes, Facebook, Twitter, Google, those who are now tracking you and sharing the info with governments.

I think is each one responsibility to protect your visitors, and try not to expose them to tracking, and keep their info as save and private as possible. Now, when you use Facebook or Twitter buttons, or the G+ button, your are loading scripts from their sites, and thus giving them the possiblity to track your visitors. It is the same if you use addthis, or sharethis widgets.

But you still want to give the visitors who won't mind sharing their info, the easiness of sharing your content, finally you get traffic from that action.

Happily the three major social networks offer a way to do it, with simple links.

##Twitter, Facebook and Google Plus share links and how to use them 

Facebook share link 

For Facebook , you just need to add this link in everyone of your posts. 

	http://facebook.com/share.php?u=http://url-of-the-post 

Twitter share link 

In the case of Twitter, you can use this one: 

	http://twitter.com/intent/tweet?url=http://url-of-the-post&text=Title of the post&via=yuor-twitter-handle 

Google Plus shre link 

Finally in the case of Google Plus you may use this one 

	https://plus.google.com/share?url=http%3A%2F%2Furl-of-the-post

How to use it 

This is different depending which platform you are using to blog, in the case of Wordpress, it has to be coded in the theme. You can use the info [here](http://codex.wordpress.org/Function_Reference/get_permalink). I think something like this may work.

	<a href="http://facebook.com/sharer.php?u=<?php echo get_permalink(); ?>">Share on Facebook</a>

But I am no expert in Wordpress so I may be wrong.

If you are using Jekyll, the I can tell you how I did it.

	<a class="btn btn-primary" href="http://twitter.com/intent/tweet?url=http://www.garron.me/en/blog/provide-shre-buttons-without-exposing-your-visitors.html&text=why to use Twitter, Facebook and Google Plus share links and not button&via=ggarron">Tweet</a> | <a class="btn btn-primary" href="http://facebook.com/sharer.php?u=http://www.garron.me/en/blog/provide-share-buttons-without-exposing-your-visitors.html">Like</a> | <a class="btn btn-primary" href="https://plus.google.com/share?url=http%3A%2F%2Fwww.garron.me/en/blog/provide-share-buttons-without-exposing-your-visitors.html">+1</a>

That line is going to insert three buttons like these ones, if you are using Twitter Bootstrap template. If not, you can use just links or something like this.

	<a href"href="http://twitter.com/intent/tweet?url=http:/www.garron.me/en/blog/provide-share-buttons-without-exposing-your-visitors.html&text=why to use Twitter, Facebook and Google Plus share links and no buttons&via=ggarron"><img src="path-to-twitter-logo"></a>

And the same for Facebook, and Google Plus.

##Conclusion 

I really hope this may be useful for someone, and once again consider to reduce to a minimum the exposure of your visitors to tracking tools out of your control.

This site, does not use Google Analytics (at least for now), does not have Twitter, or Facebook javascripts loading, no Disqus or any big network that may track my visitors.

And I am seriously thinking into serve my own copy of Twitter Bootstrap scripts instead of serving them from the Google Network. (NetDNA, not Google-Editing this thanks to a comment on Hacker News)

Note: This may not true anymore in the future, but I will try to keep it this way as far as I can.

