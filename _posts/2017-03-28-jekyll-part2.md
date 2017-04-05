---
layout: post-sidebar
title: "Strange case of Dr Jekyll and Mr Windows / Part II"
date: 2017-03-28 12:21:17
categories: dsp2017 coding
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

If you follow me along on "Just sudo IT", you remember [the post about setting up Jekyll](http://just-sudo-it.pl/jekyll-on-windows-part1). We have ended up with a basic set-up of a default Minima-themed blog. Great for beginning but now time has come to customize it to your liking. You will probably want to adjust the layout, install a chosen template (you can also style your blog completely from scratch but we’re not going to cover this case here), add custom domain etc. Let’s see how to do it.

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

Time for some work with the visual part of your project. As mentioned before, you can style it all by yourself and there are many nice walkthroughs to check, like for example:
+ [A series of **video tutorials**, far beyond customizing your blog only](http://jekyll.tips/)
+ [A nice guide from **Pixel Cog** by Mike Greiling](http://pixelcog.com/blog/2013/jekyll-from-scratch-core-architecture/)
+ [An in-depth tutorial on **Pluralsight**](https://app.pluralsight.com/library/courses/custom-jekyll-theme-2372/table-of-contents). By the way, you can get a **free Pluralsight account** for as long as **3 months**! Tons of great knowledge to grab, expert tutors, highly recommended stuff.

However you might choose to go for a ready-to-go theme, just as I did, since I was running out of time and needed something “here and now”. In this case you can opt for a free or premium template. I personally recommend you the second option, simply from my own experience. I might have had bad luck but having tried to install a free theme, I failed. The first problem was the outlook: as a (more or less former) designer, I just couldn’t bear something I found ugly in terms of fonts, layout, colors etc. ;) This point is kind of funny in a coding world, I know - but wait, there’s more! The tricky thing is that free templates are often not-that-great in terms of documentation and adjustability. For me, being very fresh to Jekyll, that was a pain in the ass. A few hours wasted and I moved back to the good old [Theme Forest](https://themeforest.net/tags/jekyll). Don’t yell at me, I know their downsides but, on the other hand, their themes are well tested, you get almost immediate support for any issue - and they simply look good. Again, presumably no one will write your template better than yourself but… yeah, you know my *but*. ;)

So here’s the deal: once you get your theme (you choose the source, it may well be true, that there are far better options that Theme Forest, I’ll be happy to get to know them!), you need to get familiar with the Jekyll’s structure. At this moment your project’s structure looks probably like this:

+ **.git** 		    // *folder*
+ _posts 		// *folder*
+ _site		    // *folder*
+ **_config.yml**	// *file*
+ about.md	    // *file*
+ **Gemfile**	    // *file*
+ **Gemfile.lock**	// *file*
+ index.md	    // *file*

I have bolded the files and folders that need to stay where they are, the rest will be replaced with your theme files. In my case, that was enough to get the template up and running. If you chose a free theme, it may end up being a bit more tricky so choose wisely - paid or not, your theme should have clear installation guides, unless you already are a Jekyll ninja. :)

Now what are these folders for exactly? Let’s have a look at an exemplary basic structure of a Jekyll site:

{% highlight javascript %}
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
{% endhighlight %}<br>
We already know what `_config.yml` is. And we’ll come back to some more adjustments here in just a moment.

The `_drafts` folder is optional. As its name suggests, here’s where you store draft files for your posts. You will not see them published on your public blog but you can preview them locally once you run `jekyll serve` command on your console.

The `_includes` folder stores the partials such as footer or sidebar. These are the sections that get duplicated on respective sites.

The `_layouts` keeps, you guessed it, the layouts for individual sites, such as home, page, post, contact or category. You may well have only the default.html and post.html here, all up to you and/or the theme chosen.

The `_posts` are also pretty self-explanatory. It’s basically post files, each of them keeping a single post with its date, title and contents.

If you’re working with Sass, it will be no surprise to you to encounter the `_sass` folder. In case you don’t know this preprocessor (I strongly recommend you to familiarize yourself with Sass, it will enhance your workflow tremendously), these are the source files for your stylesheets. Something like CSS on steroids. ;)

And finally the `_site` folder where the whole generated site is placed. Stay away from fiddling with this one, it’s not where you edit things, it’s just the final outcome to display in the browser.

Now basically how you modify the way your sites display is by editing the so-called [YAML front matter](https://jekyllrb.com/docs/frontmatter/). This section is always at the beginning of the file containing your page or post and it allows you to control how Jekyll processes and builds pages. The YAML front matter is put between triple-dashed lines and can look like so:

{% highlight javascript %}
---
layout: default
title: My first post
date: 2017-03-15 10:34
author: John Smith
---
{% endhighlight %}<br>
In the above example we ask Jekyll to display this specific post using the `default.html` layout, to give it a specific title and author, and to publish it on a specific date. 
These are just four examples of predefined global variables that you can use at this point. Some of the others are:

+ **permalink**: allows you to override the default permalink settings
+ **category** or **categories**: puts your post into a specific category / categories (simply put as an array with spaces; no brackets, no commas)
+ **comments**: a boolean (true/false) stating whether or not you want the comments to be displayed; [Disqus](https://disqus.com/) is a recommended solution for introducing comments' feature on a Jekyll blog
+ **published**: another boolean value that allows you to keep your post unpublished, if set to false
+ **tags**: pretty much like comments, tags allow the posts to fall under a given tag
+ and more

Depending on your theme and needs you will probably mainly need to adjust only front matter. When it comes to styling the contents, it boils down to mastering (joking, some basics will do) Markdown. I will cover some of its syntax in the next section.

Done with the fundamentals of Jekyll structure, let's switch back to the `_config.yml` file for a minute. You may want to manage how to handle permalinks here. Most often, you will want them to point at the post's title. In this case go ahead and add this line:

{% highlight javascript %}
permalink: :title
{% endhighlight %}<br>
You can also set up your top navigation and footer here. In my case, here is the final `_config.yml` for this blog:

![Final _config.yml](img/post-assets/config-yml.jpg){:class="img-responsive"}

Don't forget that you need to re-serve jekyll if you introduce any changes to the `_config.yml`, otherwise you won't be able to track the changes. 

{% highlight javascript %}
jekyll serve
{% endhighlight %}<br>
Meanwhile, I run up against two really promising FREE Jekyll themes. Seem to be well documented and hopefully they will prove to be a counterexample of my former thesis on the supremacy of premium themes. Check them out, I will be happy to hear your feedback!

+ [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/)
+ [So Simple](https://mmistakes.github.io/so-simple-theme/)


## Formatting your posts with Markdown

The actual content of your Jekyll posts and pages is written in Markdown, a simple text formatting engine that you probably got familiar with when creating your README.md file for your GitHub repositories. However, in case you did not, here are some basics:

+ **Headers**<br>
You simply use hashtags for that. The numbers of hashtags determines the size of the header. You can think of adding hashtags as incrementing the number in your <h…></h...> tags. For instance, if you write `# Header1` the result will be a big header, `##  Header` will be a bit smaller and so on. <br>Note two things:
    - The single hashtag headers (the biggest ones, equivalent to `<h1></h1>`) are reserved for blog titles, don’t use them in your content.
    - Make sure there is a space after the hashtag. For some reason Jekyll cares about that.
+ **Inline markup styles**<br>
    - To make a phrase render as *italics* you put it in between of single asterisks: `*italics*`.
    - To make a phrase **bold** you need to put it in between of double asterisks, like so: `**bold**`.
    - To make your phrase render like `code()`, you put it in between of backticks: `` `code()` ``.
+ **Lists**<br>
    - **Unordered lists**<br>
    Unordered lists’ items start with `*` or `+` or `-` . Don’t forget the **space** afterwards!
        - **Nested list items**<br>
        For a nested list item hit `Tab` followed by `-` and **space**. You can exchange `-` with `+` or `*` or even **number** (followed by **dot** and, of course, **space**)
    - **Ordered lists**<br>
        This one is simple: press **number** followed by **dot** and **space**, like so: `1. list element`. That’s it!
+ **Links**
    To create a link put its title inside square brackets first, then the actual address inside round brackets, like so: <br>
    `[Google](http://google.com)`
+ **Images**
    Placing images follows a rule similar to the links, you only need to precede the whole stuff with an exclamation mark. In the round brackets you either put a relative path to the image on your server, or an absolute path to an image hosted elsewhere. Example:<br>
    `![Image title](img/my-image.jpg)`

That was just some very basics of Markdown, enough for the very beginning but in the nearest future you might need a more extensive resource. In this case, have a look at what I found for you:
	
+ [Markdown cheatsheet on GitHub](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
+ [A great video series by Wes Bos](https://masteringmarkdown.com/). 
    You might have known the guy before, he’s the author of fabulous courses on JavaScript, Flexbox and more. Some of them are free, the others are paid. I purchased the one on [EcmaScript6](http://wesbos.com/es6-for-everyone/) and it proved a great value for money.

## Using a custom domain with Jekyll

The last thing I’m going to cover is setting up a custom domain for your Jekyll blog. Once you've purchased your domain there are three steps to follow in order to redirect your blog which is currently hosted under `your-login.github.io/your-project`.

1. In your project’s root create a new empty file and save it as `CNAME` (with no extension). Inside of this file enter your domain’s name. For the sake of this example I have got myself a free jekyll.cf domain and that’s exactly and only thing that goes into the `CNAME` file. No http://, www or so, just the plain name.
2. Now login to your GitHub account and navigate to your project. Choose the **Settings** panel (top right option). Once you’re there, scroll down to the **GitHub Pages** section. You will find here a place to type in your **Custom domain** like on the image below:
![Custom domain on GitHub Pages](img/post-assets/custom-domain.jpg){:class="img-responsive"}
3. Point your DNS to GitHub Pages. Login to your domain provider’s panel. Add a **new CNAME record** and target it at your base user’s github.io site. Here is how it looks like in my case:
![DNS](img/post-assets/dns.jpg){:class="img-responsive"} <br> Wait for the DNS to propagate. You’re there, nice and simple. :)

## Final word

Whew, you’ve done that! If you’ve read through both parts, congratulations, you are a patient reader. A great feature for a programmer! If you stumble upon any issues (pretty sure you will as every project is different, our needs too), the best places to dive deeper into Jekyll are:
+ [Jekyll’s official site](http://jekyllrb.com/)
+ [GitHub Pages help](https://help.github.com/categories/customizing-github-pages/)
+ and, as always, invaluable **StackOverflow**, god bless the dudes!

Have fun working on your project. :)
