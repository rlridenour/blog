---
comments: true
date: '2017-06-21T11:05:34Z'
tags:
- iOS
- jekyll
title: Publishing to Jekyll with Editorial on iOS
url: "/2017/06/21/jekyll-ios-workflow/"

---
As a blog platform, Jekyll has a number of positive features: 

1. The speed and security of a static site,
2. The convenience and future-proofing of plain text, and most importantly for educators,
3. Free hosting on GitHub.

For me, the one drawback has been finding a convenient way to post using my iPad. There are a number of good Markdown editors for iOS, so writing posts is very easy, but publishing them can be a challenge. [Working Copy](https://appsto.re/us/xONC1.i) works well to manage the Git repository, but it doesn't have the convenience that I wanted, and I really don't need to store my whole Jekyll repository on the iPad. I can post using [Prompt 2](https://appsto.re/us/PTVR2.i) and my Linux server on [Digital Ocean](https://www.digitalocean.com/).  Neither of these are the simple write-and-post workflows that the iPad calls for, though.

Yesterday, I found this [workflow](http://www.editorial-workflows.com/workflow/5838419494174720/XyeFJfsyXwE) by Max Jacobson. The first time it is run, it takes you to Github to generate an access token. After giving it the access token, the workflow will generate a file name in the correct format, prepare a commit message, and push the post to Github.[^1]

Now, I'm one step closer to being able to use the iPad as a desktop replacement.



[^1]: I did have to slightly modify the workflow by changing the "Request commit message from user" step to require a single line entry.
