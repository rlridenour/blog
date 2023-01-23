---
comments: true
date: '2015-11-15T17:18:41Z'
tags:
- emacs
- latex
title: LaTeX-Skim Sync
url: "/2015/11/15/latexskim-sync/"

---
I recently started using John Wiegley's [use-package](https://github.com/jwiegley/use-package ) for my Emacs init files. For Auctex, I used

{{< highlight lisp >}}
(use-package tex
    :ensure auctex)
{{< / highlight >}}
and everything worked except for sync with Skim on OS X. ```C-c v``` would not launch the Skim, even though I was confident that the Skim was set to be the default viewer. Instead, no viewer would launch, and I'd see "View command: dvi2tty -q -w 132" in the minibuffer.

After seeing that some others had used a slightly different configuration, I changed mine to

{{< highlight lisp >}}
(use-package tex-site
    :ensure auctex)
{{< / highlight >}}
	
and everything started working fine. I still have no idea why, but it may help someone else.
