---
comments: true
date: '2016-06-08T11:04:07Z'
tags:
- jekyll
title: Pull Quotes
url: "/2016/06/08/pull-quotes/"

---
Here is my attempt at pull quotes in the Lanyon/Poole theme for Jekyll:

``` css
.pquote {
    float: right;
    width: 15rem;
    color: #979797;
    font-size: 1.5rem;
    line-height: 1.8rem;
    font-style: italic;
    padding: 1rem;
	quotes: "\201C""\201D""\2018""\2019";
}
```

I just learned that Kramdown makes it easy to specify classes and attributes. So, this produces the pull quote:

``` markdown
> This is some quoted text.
{:.pquote}
```

The final result looks like this:[^1]

<!-- Donec id elit non mi porta gravida at eget metus. Donec id elit non mi porta gravida at eget metus. Vestibulum id ligula porta felis euismod semper. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam id dolor id nibh ultricies vehicula ut id elit. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor. Cras mattis consectetur purus sit amet fermentum. -->

>"Pull quotes are easy to code and add a nice touch to the site."
{:.pquote}

Donec id elit non mi porta gravida at eget metus. Donec id elit non mi porta gravida at eget metus. Vestibulum id ligula porta felis euismod semper. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam id dolor id nibh ultricies vehicula ut id elit. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor. Cras mattis consectetur purus sit amet fermentum. Donec id elit non mi porta gravida at eget metus. Donec id elit non mi porta gravida at eget metus. Vestibulum id ligula porta felis euismod semper.

[^1]: It is easy to add quotation marks automatically, using the "before" and "after" class selectors. I decided not to do this for the sake of flexibility.
