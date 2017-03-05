---
layout: post-sidebar
title: "Strange case of Dr Jekyll and Mr Windows / part I"
date: 2017-03-18 12:30:55
categories: dsp2017
author_name : Kamila
author_url : /author/kamila
author_avatar: kamila
show_avatar : true
read_time : 32
feature_image: feature-fire
show_related_posts: true
square_related: recommend-fire
---

For many years I have been using Wordpress as an obvious choice when choosing a blogging platform. Wordpress is by far the most popular CMS on the market, supported and developed for 14 years, powering around 8% of all pages in World Wide Web. That speaks for itself. However, since I’ve been keeping my projects on GitHub pages for the last few months, I’ve discovered it might be much easier to run the next blogging project directly on GitHub server and make use of Jekyll due to its native support in GitHub pages.

## So what is Jekyll?
As the recurring definition states, Jekyll is a simple, blog-aware, static site generator based on Ruby language. By saying “static” we mean it’s flat-file and ready for deployment. No databases needed, no security headaches, no maintenance issues. It’s ultra-fast, cheap (your blog can be hosted for free on GitHub pages) and manageable. The contents are written simply in HTML/CSS/Markdown so if you’ve had any blogging experience, switching to Jekyll should be duck soup. :) At least when you’re running it on Mac OS or Linux platform.

## ...but I am not.

And here’s where things go a little bit trickier. As the majority of Poles, I am a more or less happy user of a mundane Windows 7 (yes, 7, in 2017 I find it funny too). As it turned out, running Jekyll on Microsoft’s child was not as smooth as I hoped. I will try to guide you through the process and prevent you from running  into some stumbling blocks I’ve needed to force through myself. 

Some of the steps below look probably alike on systems other than Windows, however, since I have tested the process on Win7 only, I can not specify the exact differences..

## Step 1. Ruby installation

Assuming that you have some basic knowledge of command line and are familiar with Git (and have Git ready to use on your platform), you can proceed with setting up our GitHub-hosted, Jekyll-powered website. First, we need to install Ruby. It is likely you already have Ruby on your machine so go ahead and type in your console:

{% highlight javascript %}
{
ruby -v
}
{% endhighlight %}

In my case I got the following answer:
{% highlight javascript %}
{
ruby 2.3.3p222 (2016-11-21 revision 56859) [x64-mingw32]
}
{% endhighlight %}

If your version is lower than 2.0.0, you can update it. If you don’t have Ruby yet, just visit:

(http://rubyinstaller.org/downloads/)



