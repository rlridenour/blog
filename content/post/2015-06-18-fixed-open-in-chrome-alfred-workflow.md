---
comments: true
date: '2015-06-18T02:31:39Z'
tags:
- osx
- utilities
title: Fixed Open in Chrome Alfred Workflow
url: "/2015/06/18/fixed-open-in-chrome-alfred-workflow/"

---
I use Andrew Curtis-Black's "Open in Chrome" [Alfred workflow](http://www.alfredforum.com/topic/1875-open-current-safari-tab-in-chrome-improved/) whenever I need to view a page that uses Flash.
After installing Parallels to run Windows on my Mac [^1], the workflow began misbehaving. It would start Parallels, then open Chrome in Windows, which is certainly not what I wanted to happen.

I took a hint from [this script](https://github.com/lhagan/Open-in-Chrome/blob/master/ChromeHelper.applescript ) and fixed the problem today. Search for the applescript "open_in_chrome.scpt", then change the line

`tell application "Google Chrome"`

to

`tell application id "com.google.chrome"`

and all is fixed.

[^1]: I know, I feel dirty. Believe me, it was only so I could run some essential Army forms software.
