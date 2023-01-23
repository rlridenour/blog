---
comments: true
date: '2016-07-12T15:07:12Z'
tags:
- jekyll
title: Automating Jekyll with Fish
url: "/2016/07/12/automating-jekyll-with-fish/"

---
[Last month](http://randyridenour.net/2016/06/23/emacs-on-the-ipad/), I wrote about my experiment with iOS and a remote server from [Digital Ocean](http://wwww.digitalocean.com). It's working very well, but Emacs can feel a bit sluggish at times, served up remotely over a crowded public wi-fi network. Vim is speedy, and since I use Evil on Emacs, it's not too painful to switch occasionally. Any pain comes from the loss of the automation with all of those Emacs functions I've written and collected over the years.

I thought about writing some scripts in Elisp, but settled on functions in the [Fish](http://fishshell.com/) Shell. The first function creates an appropriately named Markdown file with YAML front-matter. The important parts come from [Marc Ransome](https://gist.github.com/marcransome/6096005):

``` fish
function draft -d "Open default editor with date prepended filename and specified title for jekyll posts."

cd ~/Dropbox/blog-drafts

# Create file
  set title (date +"%Y-%m-%d")
  
  switch (count $argv) 
    case 0
      echo "No post title was specified."
      return 1
    case 1
      set lower_arg (echo $argv[1] | tr A-Z a-z)
      set title $title-$lower_arg.md
    case \*
      for arg in $argv
        set lower_arg (echo $arg | tr A-Z a-z)
        set title $title-$lower_arg
      end
      set title $title.md
  end
  
# Append YAML
echo "---" >> $title
echo "layout: post" >> $title
echo "title: " $argv >> $title
echo "tags:" >> $title
echo "- " >> $title
echo "comments: true" >> $title
echo "date:" (date +"%Y-%m-%d %H:%M:%S") >> $title
echo "---" >> $title

# Open file in VIM
  EDITOR $title
end
```

The other two functions were very simple – one to move a completed draft to the _posts folder, and another to commit the new post and push to Github with the imaginative commit message, "New post":

``` fish
function post
   mv $argv ~/Sites/rlridenour.github.io/_posts
end

function publish
 cd ~/Sites/rlridenour.github.io
 git add .
 git commit -m "New post."
 git push
end
````
