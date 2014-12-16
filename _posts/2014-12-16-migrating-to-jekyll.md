---
author: Aishwarya Singhal
comments: true
layout: post
title: Migrating to Jekyll
tags:
- jekyll
- wordpress
---

So finally, I bit the bullet. I have been thinking of migrating my blog to Jekyll for almost 2 years now, never had a true reason. Well now I do, I am free and bored of the themes that Wordpress offers for free. I have been a long time fan of Wordpress, which I believe is still awesome, but I needed more control on how my blog looks and so I moved.

Migrating itself was not super hard. There is sufficient help available online, but a quick summary:

1. Get started with [https://help.github.com/articles/using-jekyll-with-pages/]
2. Skip the hello world goodie, create a site instead

	```
	bundle exec jekyll new
	bundle exec jekyll build
	bundle exec jekyll serve
	```
3. Migrate your blogs using [ExitWp](https://github.com/thomasf/exitwp)
4. Migrate comments using Disqus. Read [this blog](http://www.girliemac.com/blog/2013/12/27/wordpress-to-jekyll/). Use the domain migration tool on Disqus to change the links in the imported comments and get the links right. I basically just did a find and replace in Wordpress exported XML.
5. Modify the SCSS to make your blog look the way you want.
6. Attach Google Analytics to your pages if you like stats.
7. Get yourself a coffee :-)

There are three additional benefits of this:

1. The best thing about a Jekyll backed blog is that there is no database involved. It is static content and is super fast in rendering! 
2. It is hosted for free on github. 
3. And you get to write your blogs in markdown!

