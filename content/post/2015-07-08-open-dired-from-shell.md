---
comments: true
date: '2015-07-08T09:47:32Z'
tags:
- emacs
- zsh
title: Open Dired From Shell
url: "/2015/07/08/open-dired-from-shell/"

---
I was browsing the interwebs this morning, looking for a way to open a Dired buffer of the current finder window. There is a lot on going the other way, from Emacs to the Finder, but nothing from the Finder to Emacs.
I got this from [Fortune Datko](http://datko.net/2013/07/11/open-emacs-dired-buffer-from-dired/ ):

Add this to your shell rc file (in my case, .zshrc):

```
# open a dired window for the current directory
dired() {
    emacsclient -e "(dired \"$PWD\")"
}
```

Then, assuming that Emacs server is running, type "`dired`" in the shell, and a Dired
buffer of that directory opens in the current Emacs frame.

Just out of curiosity, I wondered what typing "`emacsclient -c .`" would do. It opens a dired buffer in a new frame. I have a shell script called "ec" that starts a new emacs client, but it's easy to do it with a zsh alias:

```
alias ec="emacsclient -c -a ''"
```
This starts a server if there is not one already, then opens a new client. So, typing `ec .` should then open a Dired buffer in a new frame.
