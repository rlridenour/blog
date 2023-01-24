---
title: 'Arguments in HTML'
date: "2021-06-24T08:50:55"
draft: false
tags: ['html', 'markdown', 'philosophy']
---

I have another post in a [WordPress blog](https://rlridenour.wordpress.com/2019/01/08/arguments-html/) about how to do this in WordPress. I'll replicate it here for Hugo. This post is not about arguments that occur on the internet, but about how to display philosophical/logical arguments in standard form on the internet. To put an argument in standard form:

1.  Write each premise on a separate, numbered line,
2.  Draw a line underneath the last premise, and
3.  Write the conclusion underneath the line.

I'll first show how to format an argument in HTML, then show an easier way in Markdown with Hugo.

## HTML


It's easy enough to produce an ordered list in HTML, but then the conclusion is numbered, which makes it look like another premise. This can be fixed with a trick in CSS, just add something like this to your stylesheet:

```css .list-arg li:last-child { list-style: none }```

If one doesn't need to post very many arguments in standard form, then it might not be worth it to clutter up the main stylesheet with another class. It's just as easy to add the style specification to each argument, like this:

```html
<ol>
  <li>
    First Premise
  </li>
  <li>
    <u>Last Premise</u>
  </li>
  <li style="list-style:none;">
    Conclusion
  </li>
</ol>
```

Both methods produce something that looks like this:

<ol>
  <li>
    First Premise
  </li>
  <li>
    <u>Last Premise</u>
  </li>
  <li style="list-style:none;">
    Conclusion
  </li>
</ol>


<ol class="arg">
  <li>
    First Premise
  </li>
  <li>
    <u>Last Premise</u>
  </li>
  <li>
  Conclusion
  </li>
</ol>

Sometimes, the last premise is significantly shorter than the others, and the underline doesn't look quite right. For example,

<ol>
  <li>
    P &#8835; Q
  </li>
  <li>
    <u>P</u>
  </li>
  <li style="list-style:none;">
    Q
  </li>
</ol>



That can be fixed with some non-breaking spaces. It looks ugly, but it does take care of the problem.

```
<ol>
  <li>
    P &#8835; Q
  </li>
  <li>
    <u>P&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<;/u>
  </li>
  <li style="list-style:none;">
    Q
  </li>
</ol>
```

That produces

<ol>
  <li>
    P &#8835; Q
  </li>
  <li>
    <u>P&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</u>
  </li>
  <li style="list-style:none;">
    Q
  </li>
</ol>

## Markdown

It is very easy to make lists in Markdown. Unfortunately, we have the same problem that we started with in HTML. That is, the conclusion is numbered:

1. First Premise
2. Second Premise
3. Conclusion

Since raw HTML can be used in Markdown, we could just use HTML. Since the Goldmark rendering engine that Hugo uses allows attributes and classes in Markdown, there is another, far simpler, option.

First, make sure that your site config.toml page has "unsafe = true" and "block = true" in the markup section. Mine looks like this:

```
[markup]
  [markup.goldmark]
  [markup.goldmark.parser]
      autoHeadingID = true
      autoHeadingIDType = "github"
      [markup.goldmark.parser.attribute]
        block = true
        title = true
    [markup.goldmark.renderer]
      unsafe = true
```


Now, add a new class to your stylesheet. I called it "arg" and styled it like this:

```
.arg li:last-child {
  list-style: none;
}

.arg li:nth-last-child(2) {
text-decoration: underline;
}

.arg li {
margin: 0px;
}
```

The first part removes the number at the line with the conclusion, and the second part underlines the last premise. Finally, I decided to tighten up the lines. Now, when you write your post, just use a normal Markdown ordered list with the class after the last item:

```
1. First premise
2. Second premise
3. Conclusion
{.arg} 
```

When published, that code produces this:


1. First premise
2. Second premise
3. Conclusion
{.arg} 

