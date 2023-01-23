---
comments: true
date: '2015-01-16T16:02:35Z'
tags:
- emacs
- jekyll
title: Emacs Blog Test
url: "/2015/01/16/emacs-blog-test/"

---
I'm testing blogging to the new Jekyll blog from Emacs using the Lisp code from [William Denton](https://www.miskatonic.org/2014/01/26/more-about-emacs-and-jekyll/ ).
It works extremely well. I had to remap the key definitions since C-c j was already used for something else in my configuration. It's bad Emacs form, but I used C-x j instead. So, C-x j n asks for a post title, then creates a file in the drafts folder with the front matter already inserted. When ready to publish, C-x j t inserts the time stamp, and C-x j p renames the file using the time stamp and moves it into the posts folder. C-x j o opens the site folder in a dired buffer.
