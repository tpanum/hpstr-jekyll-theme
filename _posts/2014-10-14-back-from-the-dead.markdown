---
layout: post
title: 'Back from the dead'
date: '2014-10-14 17:57:42 +0200'
tags: [coding, emacs, workflow]
image:
  feature: ergodox.jpg
---

This post signals the reincarnation of my ancient WordPress blog. I replaced the engine, and the site is now running on [jekyll](http://jekyllrb.com/) (the layout is still WIP). I did this primarily based on the elegant simplicity that [jekyll](http://jekyllrb.com/) is based on. 

This allows me to write and publish new posts directly from my Emacs. I even created this handy little command for creating post files with proper naming and YAML Front Matter:

{% highlight lisp %}
(defun tpanum/create-jekyll-post
  (title)
  "Creates a new buffer and file for a blog post"
  (interactive "sTitle of blog post: ")
  (let
      ((filename
        (concat
         (format-time-string "%Y-%m-%d-")
         (replace-regexp-in-string " " "-"
                                   (downcase
                                    (replace-regexp-in-string "[^0-9a-zA-Z ]" "" title))))))
    (switch-to-buffer
     (generate-new-buffer filename))
    (insert
     (concat
      (mapconcat 'identity
                 '("---" "layout: post")
                 "\n")
      "\n" "title: '" title "'\n" "date: '"
      (format-time-string "%Y-%m-%d %H:%M:%S %z")
      "'\n" "---\n"))
    (if
        (boundp 'blog-home)
        (write-file
         (concat blog-home "/_posts/" filename ".markdown")))))
{% endhighlight %}

It prompts for a title for the post, and automatically creates a file in the ```_posts``` directory of your blog, based on the variable ```blog-home```. This variable should contain the local path to the root of your jekyll blog.

My workflow have changed a lot during the last two years. I've learned Vim-fu, and for the past year I've been using Emacs as my one-and-only editor (with recent addition of evil-mode).

Through this experience I can truly say that Emacs is an editor of a lifetime, and will be the last text editor I'll ever use.

You can find my Emacs config [here](https://github.com/tpanum/dotfiles), which is heavily influenced by principles of [@jeg2](https://github.com/jeg2) described in his [hangout](https://twitter.com/JEG2/status/368201878191865856).
