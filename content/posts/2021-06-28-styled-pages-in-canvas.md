---
title: "Styled Pages in Canvas"
draft: false
categories: []
tags:
- Teaching
comments: true
date: "2021-06-29T11:17:13"
highlight: true
markup: ""
math: true
url: ""
---

My [method](https://randyridenour.net/posts/2019-01-08-arguments-html/) of formatting philosophical arguments in HTML works fine when writing web pages on my own site, but not so well when I don't have access to the site's CSS, or so I thought. I tell students to format arguments in what is usually called "standard form" --- a list with numbered premises and a line separating the premises from the conclusion. So, it should look like this:

1. First premise
2. Second premise
3. Conclusion
{.arg}

This is simple to do in \\(LaTeX\\) with this:

```tex
\begin{enumerate}
\item First Premise
\item \underline{Last Premise}
\item [] Conclusion
\end{enumerate}
```

As I explained [earlier](https://randyridenour.net/posts/arguments-in-html/), it's also easy to in HTML by declaring a CSS class. Unfortunately, I see nowhere in Canvas, the learning management system used by our university, to put an external style sheet. So, my options seemed to be, first, to put the premises in a list and the conclusion on a separate line following the list. That would produce something like this:

<ol>
    <li>First premise</li>
    <li><u>Second premise</u></li>
</ol>

Conclusion

The premises are fine, but the conclusion is a new paragraph. A better option would be to put the conclusion as a numbered item in the list:

<ol>
<li>First premise</li>
<li><u>Second premise</u></li>
<li>Conclusion</li>
</ol>

This looks better, although I don't really like the separation between the list items. Unfortunately, since the conclusion is also numbered, it's easy to mistake the conclusion for another premise.

The best option seemed to be to produce handouts as PDF's with \\(LaTeX\\). They would be formatted correctly, but difficult to read on small mobile devices. Still, there had to be a better way. Pages in Canvas are just HTML documents, although the rich text editor hides the code from most users. There is an option to use an HTML editor when editing a page, though. My first thought was to reference an external style sheet in a document head in the usual way, like this:

```html
<!doctype html>
<html>
		<head>
				<link rel="stylesheet" href="mystyle.css">
				<meta charset="utf-8" />
		</head>
		<body>
				<ol class="arg">
						<li>First premise</li>
						<li>Second premise</li>
						<li>Conclusion</li>
				</ol>
		</body>
</html>
```

That would have been nice and simple, if it had worked. I then tried internal CSS:

```html
<!doctype html>
<html>
		<head>
				<meta charset="utf-8" />
				<style>
				 .arg li:last-child {list-style: none;}
				 .arg li:nth-last-child(2) {text-decoration: underline;}
				 .arg li {margin: 0px;}
				</style>
		</head>
		<body>
				<ol class="arg">
						<li>First premise</li>
						<li>Second premise</li>
						<li>Conclusion</li>
				</ol>
		</body>
</html>
```

Success! That is, until I clicked "Edit" again, and Canvas stripped away everything outside the body tags. Finally, I tried inline CSS:

```html
<ol class="arg">
		<li style="margin: 0px;">First premise</li>
		<li style="margin: 0px; text-decoration: underline;">Second premise</li>
		<li style="margin: 0px; list-style: none;">Conclusion</li>
</ol>
```
That finally worked. Unfortunately, it meant that the CSS had to be explicitly declared on every item that needed styling, every time that the item was used on the page. Then, I discovered CSS Inliners. An inliner is a tool that takes externally styled HTML as input, and outputs HTML with all inline CSS. Evidently, these are used by people who want to control the formatting of their HTML emails. [Mailchimp's Inline Tool](https://templates.mailchimp.com/resources/inline-css/) works well. I'm using an inliner tool called "Juice" that can be installed using the Node package manager. That way, I can automate the process with a simple shell script. Here's the function I use in [fish](https://templates.mailchimp.com/resources/inline-css/):

```fish {linenos=true}
function canvas
		juice canvas.html canvas.html
		find . -type f -name "canvas.html" -print0 | xargs -0 sed -i '' -e 's/body>/div>/g'
		pbcopy < "canvas.html"
		rm canvas.html
end
```

Line 2 runs the inliner on a file named "canvas.html" and overwrites that file. Line 3 changes the body tags to div tags, which prevents Canvas from deleting any text outside the body tags. Finally, line 3 copies the resulting file to the clipboard, ready to be pasted into the Canvas HTML editor, and line 4 then deletes the HTML file. 

I delete the HTML file, because, since I use Emacs, the handouts themselves are written in Org mode. So, any changes are made to the Org document, which would then need to be exported again to HTML. The Org document header contains these lines:

```orgmode {linenos=true}
#+AUTHOR: Randy Ridenour
#+LANGUAGE: en-us
#+EXPORT_FILE_NAME: canvas.html
#+HTML_DOCTYPE: html5
#+OPTIONS: toc:nil
#+OPTIONS: html-style:nil
#+HTML_HEAD: <link rel="stylesheet" type="text/css" href="https://randyridenour.net/css/canvas.css"/>
```

Line 3 ensures that the output file is named `canvas.html`. That makes the shell script easier to write, and it doesn't need a unique name since it will just be deleted immediately after being copied to the clipboard. Line 5 prevents a table of contents from being generated. If the handout is long enough to warrant a TOC, then just change that to `toc:true`. Line 6 prevents the Org exporter from adding its usual CSS, and line 7 adds the reference to 
an external stylesheet located on my personal website.

Everything is tied together with a very simple Emacs function:

```elisp
(defun canvas-copy ()
  "Copy html for canvas pages"
  (interactive)
  (org-html-export-to-html)
  (shell-command "canvas")
)
```


