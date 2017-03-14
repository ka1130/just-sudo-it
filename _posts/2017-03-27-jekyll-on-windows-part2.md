---
layout: post-sidebar
title: "Strange case of Dr Jekyll and Mr Windows / part II"
date: 2017-03-27 15:21:07
categories: dsp2017
author_name : Kamila
author_url : /author/kamila
author_avatar: kamila
show_avatar : true
read_time : 20
feature_image: feature-jekyll-1
show_related_posts: true
comments: true
square_related: recommend-jekyll-1
---

Now that we have the basic setup for Jekyll blog, it’s time for some customization. You will probably want to adjust the layout of the blog, install a theme that you like (you can also style your blog completely from scratch but we’re not going to cover this case here), add custom domain etc. Let’s see how to do it.

## Basic configuration

First, we’ll have a look at the `_config.yml` file that lives in your project’s root. Open it up with your editor. Change the default values of the `title`, `email`, `description`, `url` and `baseurl` (the subpath of your site, e.g. /blog). 

The `url` will be your GitHub .io home page and the `baseurl` will be the name of the repository which we’ll create later on. Here’s how it looks in my case:

{% highlight javascript %}
baseurl: "/testjekyll"
url: "https://ka1130.github.io/" 
{% endhighlight %}<br>
You can find a very extensive explanation of all the configuration options on the [Jekyll documentation page](http://jekyllrb.com/docs/configuration/) but you probably won’t need most of this stuff. Good to know, however. 

As you will see in the Build settings section, the default template is minima: that’s what you can see at the moment once you run jekyll serve and open up your browser on `http://localhost:4000`.

## Pushing your blog to GitHub pages

Now let’s create a new repository on GitHub. As mentioned above, I decided to go for *testjekyll* name. Check the `Initialize this repository with a README` box, otherwise you’ll be directed to the setup page. At this point my exemplary repo lives under this address:

{% highlight javascript %}
https://github.com/ka1130/testjekyll
{% endhighlight %}<br>
Now push the project to GitHub pages (remember to change the address to the one of your blog!):

{% highlight javascript %}
git remote add origin https://github.com/ka1130/testjekyll
{% endhighlight %}<br>
Next, add a special branch that has to be called gh-pages:

{% highlight javascript %}
git checkout -b gh-pages
{% endhighlight %}<br>
Still on gh-pages branch, make your first commit:

{% highlight javascript %}
git add .
git commit -m “Initial commit.”
{% endhighlight %}<br>
And finally, push the commit to GitHub pages:

{% highlight javascript %}
git push origin gh-pages
{% endhighlight %}<br>
In your browser, navigate to the new project:

{% highlight javascript %}
https://ka1130.github.io/testjekyll/
{% endhighlight %}<br>
No need to add that in the address there will be your username instead of ka1130, and the uri will be the name of your project. :) Here we are, your blog in already online, hosted on GitHub pages. Cool!

## Setting up your theme

Lorem ipsum

## Formatting your posts with Markdown

Lorem ipsum

## Using a custom domain with Jekyll

Lorem ipsum

## Final word


