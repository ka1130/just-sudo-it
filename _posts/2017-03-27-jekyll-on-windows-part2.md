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
feature_image: feature-jekyll-2
show_related_posts: true
comments: true
square_related: recommend-jekyll-2
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

As you will see in the `Build settings` section, the default template is *minima*: that’s what you can see at the moment once you run `jekyll serve` and open up your browser on `http://localhost:4000`.

## Pushing your blog to GitHub pages

Now let’s create a new repository on GitHub. As mentioned above, I decided to go for a *testjekyll* name. Check the `Initialize this repository with a README` box, otherwise you’ll be directed to the setup page. 

![Starting a new repository](img/post-assets/repo-init.jpg){:class="img-responsive"}

At this point my exemplary repo lives under this address:

{% highlight javascript %}
https://github.com/ka1130/testjekyll
{% endhighlight %}<br>
Now push the project to GitHub pages (remember to change the address to the one of your blog!):

{% highlight javascript %}
git remote add origin https://github.com/ka1130/testjekyll
{% endhighlight %}<br>
Next, add a special branch that has to be called `gh-pages`:

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

Time for some work with the visual part of your project. As mentioned before, you can style it all by yourself and there are many nice walkthroughs to check, such as
+ 1
+ 2
+ 3

However you might choose to go for a ready-to-go theme, just as I did, since I was running out of time and needed something “here and now”. In this case you can opt for a free or premium template. I personally recommend you the second option, simply from my own experience. I might have had bad luck but having tried to install a free theme, I failed. The first problem was the outlook: as a (more or less former) designer, I just couldn’t bear something I found ugly in terms of fonts, layout, colors etc. ;) This point is kind of funny in a coding world, I know - but wait, there’s more! The tricky thing is that free templates are often not-that-great in terms of documentation and adjustability. For me, being very fresh to Jekyll, that was a pain in the ass. A few hours wasted and I moved back to the good old [Theme Forest](https://themeforest.net/tags/jekyll). Don’t yell at me, I know their downsides but, on the other hand, their themes are well tested, you get almost immediate support for any issue - and they simply look good. Again, presumably no one will write your template better than yourself but… yeah, you know my *but*. ;)

So here’s the deal: once you get your theme (you choose the source, it may well be true, that there are far better options that Theme Forest, I’ll be happy to get to know them!), you need to get familiar with the Jekyll’s structure. At this moment your project’s structure looks probably like this:

+ .git 		    // *folder*
+ _posts 		// *folder*
+ _site		    // *folder*

+ _config.yml	// *file*
+ about.md	    // *file*
+ Gemfile	    // *file*
+ Gemfile.lock	// *file*
+ index.md	    // *file*

I have bolded the files and folders that need to stay where they are, the rest will be replaced with your theme files. In my case, that was enough to get the template up and running. If you chose a free theme, it may end up being a bit more tricky so choose wisely - paid or not, your theme should have clear installation guides, unless you already are a Jekyll ninja. :)

Now what are these folders for exactly? Let’s have a look at an exemplary basic structure of a Jekyll site:

├── _config.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.md
|   └── on-simplicity-in-technology.md
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.md
|   └── 2009-04-26-barcamp-boston-4-roundup.md
├── _sass
|   ├── _base.scss
|   └── _layout.scss
├── _site
└── index.html // or index.md

We already know what `_config.yml` is. And we’ll come back to some more adjustments here in just a moment.

The `_drafts` folder is optional. As its name suggests, here’s where you store draft files for your posts. You will not see them published on your public blog but you can preview them locally once you run jekyll serve command on your console.

The `_includes` folder stores the partials such as footer or sidebar. These are the sections that get duplicated on respective sites.

The `_layouts` keeps, you guessed it, the layouts for individual sites, such as home, page, post, contact or category. You may well have only the default.html and post.html here, all up to you and/or the theme chosen.

The `_posts` are also pretty self-explanatory. It’s basically post files, each of them keeping a single post with its date, title and contents.

If you’re working with Sass, it will be no surprise to you to encounter the `_sass` folder. In case you don’t know this preprocessor (I strongly recommend you to familiarize yourself with Sass, it will enhance your workflow tremendously), these are the source files for your stylesheets. Something like CSS on steroids. ;)

And finally the `_site` folder where the whole generated site is placed. Stay away from fiddling with this one, it’s not where you edit things, it’s just the final outcome to display in the browser.

## Formatting your posts with Markdown

Lorem ipsum

## Using a custom domain with Jekyll

Lorem ipsum

## Final word


