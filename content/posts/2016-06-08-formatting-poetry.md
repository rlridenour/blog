---
comments: true
date: '2016-06-08T13:18:29Z'
tags:
- jekyll
- poetry
title: Formatting Poetry
url: "/2016/06/08/formatting-poetry/"

---
I have been browsing [Jekyll](http://jekyllrb.com/) themes lately, and found a very nice theme for academics, the [Ed. Theme](http://elotroalex.github.io/ed/documentation/#bibliographies). Its main purpose seems to be publishing classic texts and poetry on the web, and it includes some very handy tools. 

Getting indentation right is a problem with poetry on the web. For example, consider these lines from "The Code—Heroics" by Robert Frost.

Here is the Markdown source:

``` markdown
What was there wrong?
                     Something you said just now.
What did I say?
               About our taking pains.
```

Even though it contains the proper indentation, it renders like this:

What was there wrong?  
                     Something you said just now.  
What did I say?  
               About our taking pains.

Now, stripping out extra whitespace is generally a good thing, but I don't want it to happen with poetry. With help from the CSS in the .Ed theme, I can get the indentation right.

``` markdown
- What was there wrong?
- {:.indent-10}Something you said just now.
- What did I say?
- {:.indent-6}About our taking pains.
{:.poetry}
```

Ed. sets poetry as an unordered list, with each line as a list item. List style is set to "none" and the indented lines contain an "indent-x" attribute. This produces these properly indented lines:

- What was there wrong?
- {:.indent-10}Something you said just now.
- What did I say?
- {:.indent-65}About our taking pains.
{:.poetry}

Ed. also contains formatting tools for bibliographies. It's built on [Lanyon](https://github.com/poole/lanyon), the theme that I use, so it was easy for me to just add the CSS that I wanted to my existing site.

