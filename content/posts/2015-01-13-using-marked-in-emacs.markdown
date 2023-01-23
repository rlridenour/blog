---
comments: true
date: '2015-01-13T17:08:20Z'
tags:
- emacs
title: Using Marked in Emacs
url: "/2015/01/13/using-marked-in-emacs/"

---
[Brett Terpstra][terpstra] makes some great tools, and gives away many of them for nothing. So, I'm very happy to return a small amount by paying for [Marked][marked], his great tool for previewing Markdown files. The preview auto-updates with each save, and the new version validates external links and provides a wealth of useful statistics about the document.

I have been calling Marked from Emacs using this function that I found in various places on the internet:

{{< highlight lisp >}}
   ;; C-c m previews Markdown files in marked  
   (defun markdown-preview-file ()  
        "run Marked on the current file and revert the buffer"  
        (interactive)  
        (shell-command  
        (format "open -a /Applications/Marked.app %s"  
           (shell-quote-argument (buffer-file-name))))  
   )  
   (global-set-key "\C-cm" 'markdown-preview-file)
{{< / highlight >}}

With the most recent update, the application name changed from "Marked" to "Marked 2"&mdash;a small change that broke the function. That should be easy enough to fix, though. So, I changed the application name, and escaped the space with a backslash:

        (format "open -a /Applications/Marked\ 2.app %s"

The open command worked fine from the terminal, but when I tried it from Emacs, I got the following error message:

    FSPathMakeRef(/Applications/Marked2.app) failed with error -43.

Notice that there's no space between "Marked" and the "2," and as much as I tried, I couldn't call the application. It turns out that, although the shell requires escaping the space with a backslash, Lisp requires escaping the backslash with another backslash. So, two slashes fixed the problem:

        (format "open -a /Applications/Marked\\ 2.app %s"

[marked]: http://marked2app.com

[terpstra]: http://brettterpstra.com



