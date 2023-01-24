---
title: 'Emacs Org-Capture'
date: Tue, 12 May 2020 22:28:43 +0000
draft: false
tags: ['emacs', 'org']
---

When trying to post to a journal for the first time in an embarrassing number of months, I received an error that I had never had in the past: “org-capture-select-template: Symbol’s function definition is void: org-mks.” A quick search revealed that it’s clearly defined in org.el, and I was successfully using org mode for other things, so I could see no reason for the error. A Google search revealed that several had the problem, but none of the proposed solutions worked.

In the end, it was a problem with my .emacs.d. I use an org-mode file, that is bootstrapped with an initialization file that requires org-install and on-tangle. Moving (package-initialize) to the first line of that file fixed the problem.

