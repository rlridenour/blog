---
comments: true
date: '2015-01-13T17:09:21Z'
tags:
- zsh
title: Reloading zshrc
url: "/2015/01/13/reloading-zshrc/"

---
I use zsh instead of bash. If that doesn't mean anything to you, then just skip the rest of this post. I've been restarting the terminal after every change to my zshrc file. I knew there had to be a way to quickly reload the file without restarting the terminal.

It turns out that typing ". ~/.zshrc" will do it. The problem is that I'm not likely to remember it. I found this nice tip at [codeM0nK3Y.com](http://www.codem0nk3y.com/2012/12/how-to-reload-zsh-config/): add the following to your zshconfig:

>alias reload=". ~/.zshrc && echo 'ZSH config reloaded from ~/.zshrc'"

Now, just type "reload" and you're all set.
