---
layout: post-sidebar
title: "Strange case of Dr Jekyll and Mr Windows / Part I"
date: 2017-03-21 11:30:51
categories: dsp2017 coding
author_name : Kamila
author_url : /author/kamila
author_avatar: kamila
show_avatar : true
read_time : 30
feature_image: feature-jekyll-1
show_related_posts: true
comments: true
square_related: recommend-jekyll-1
---

For many years I have been using Wordpress as an obvious choice when choosing a blogging platform. Wordpress is by far the most popular CMS on the market, supported and developed for 14 years, powering around 8% of all pages in World Wide Web. That speaks for itself. However, since I’ve been keeping my projects on GitHub pages for the last few months, I’ve discovered it might be much easier to run the next blogging project directly on GitHub server and make use of Jekyll due to its native support in GitHub pages.

## So what is Jekyll?
As the recurring definition states, Jekyll is a simple, blog-aware, static site generator based on Ruby language. By saying “static” we mean it’s flat-file and ready for deployment. No databases needed, no security headaches, no maintenance issues. It’s ultra-fast, cheap (your blog can be hosted for free on GitHub pages) and manageable. The contents are written simply in HTML/CSS/Markdown so if you’ve had any blogging experience, switching to Jekyll should be duck soup. :) At least when you’re running it on Mac OS or Linux platform.

## ...but I am not.

And here’s where things go a little bit trickier. As the majority of Poles, I am a more or less happy user of a mundane Windows 7 (yes, 7, in 2017 I find it funny too). As it turned out, running Jekyll on Microsoft’s child was not as smooth as I hoped. I will try to guide you through the process and prevent you from running  into some stumbling blocks I’ve needed to force through myself. 

Some of the steps below look probably alike on systems other than Windows, however, since I have tested the process on Win7 only, I can not specify the exact differences.

## Step 1. Ruby installation

Assuming that you have some basic knowledge of command line and are familiar with Git (and have Git ready to use on your platform), you can proceed with setting up our GitHub-hosted, Jekyll-powered website. First, we need to install Ruby. It is likely you already have Ruby on your machine so go ahead and type in your console:

{% highlight javascript %}
ruby -v
{% endhighlight %}<br>
In my case I got the following answer:

{% highlight javascript %}
ruby 2.3.3p222 (2016-11-21 revision 56859) [x64-mingw32]
{% endhighlight %}<br>
If your version is lower than 2.0.0, you can update it. If you don’t have Ruby yet, just visit [this place](http://rubyinstaller.org/downloads/) and download the most suitable installer as per suggestions on the right-hand side. Don’t close the tab yet, we’ll go back to this page in a minute. 

Now simply run the .exe files and keep clicking “next” until you see the screen below.

![ruby-installer](img/post-assets/ruby-installer.jpg){:class="img-responsive"}

Make sure to check the option in the middle, “Add Ruby executables to your PATH”. Click “install” and you’re done! Restart your console and run

{% highlight javascript %}
ruby -v
{% endhighlight %}<br>
again to ensure you're good to go.

## Step 2. Ruby Dev Kit

Since Ruby was not built to be used on Windows (although it is, surely, possible), it can be difficult to install some of the Gems (which you can think of, generally speaking, as a specific kind of library or plugin; more in-depth description [here](http://guides.rubygems.org/what-is-a-gem/)). Go back to the Ruby Installer page and scroll it down. On the left-hand site there is a “Development Section.” Choose the one appropriate for your system’s version and download it. Create a new folder called **RubyDevKit** directly in your **C:\ ** directory. Select to extract Ruby Dev Kit's .exe file in **C:\RubyDevKit** (the folder you have just created). Now navigate to this path in your command line:

{% highlight javascript %}
cd C:\RubyDevKit
{% endhighlight %}<br>
Then go ahead and run the commands below:

{% highlight javascript %}
ruby dk.rb init
ruby dk.rb review
ruby dk.rb install
{% endhighlight %}<br>
If you encounter any trouble at this point, check up [this place](https://labs.sverrirs.com/jekyll/1x-ruby-and-devkit-error.html) for a solution.
That’s it! If all went fine, you’re ready to proceed and install Jekyll Gem.

## Step 3. Setting up Jekyll and Bundler

To get your Jekyll up and ready you simply run:

{% highlight javascript %}
gem install jekyll
{% endhighlight %}<br>
You will need a package manager called Bundler to get all Jekyll dependencies installed properly. Your console needs the following commands:

{% highlight javascript %}
gem install bundler
bundle install
{% endhighlight %}<br>
There you go! You can now start your first Jekyll project. That simple.

## Step 4. Get your Jekyll blog

Assuming that you know the basics of Git and GitHub, choose a path on your machine where you want to keep your new Jekyll project. Navigate there in your console. Now if for instance your project will be called coolblog, you need to run the following command:

{% highlight javascript %}
jekyll new coolblog
{% endhighlight %}<br>
Move to this directory...

{% highlight javascript %}
cd coolblog
{% endhighlight %}<br>
...and intialize your Git repo:

{% highlight javascript %}
git init
{% endhighlight %}<br>
In your project’s folder you will find a file called “Gemfile” (with no extension), open it up and comment the following snippet by simply putting **#** before:

{% highlight javascript %}
# gem "jekyll", "(your version here)"
{% endhighlight %}<br>
Now uncomment the "github-pages" gem below by deleting the **#** from the beginning of the line:

{% highlight javascript %}
gem "github-pages", group: :jekyll_plugins
{% endhighlight %}<br>
...and have a look at the end of the file which should say something like this:

{% highlight javascript %}
# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]

gem 'wdm', '>= 0.1.0' if Gem.win_platform?
{% endhighlight %}<br>
At this point bundler needs to be updated so run:

{% highlight javascript %}
bundle update
{% endhighlight %}<br>
You are now ready to get your blog life. Go ahead and type in in your console:

{% highlight javascript %}
jekyll serve
{% endhighlight %}<br>
to put Jekyll in kind of “watch” mode where all your changes to the blog’s files (apart from .yml configuration files) will be instantly introduced.

Now, in your browser go to `http://localhost:4000`. You will see your freshly created blog which will look like this:

![your-awesome-blog](img/post-assets/your-awesome-blog.jpg){:class="img-responsive"}

Congratulations! You’re ready to go!

Bear in mind that once you hit Ctrl + C or close the console, Jekyll server will stop and you will be unable to see your site on localhost. I myself was not aware of this initially and lost much too much time stack-overflowing why my blog stopped working. ;)


## Further reading and tips

This has been a long post, however you may find it insufficient. To learn more about working with Jekyll I encourage you to visit the following places:
+ Very insightful yet easy to follow [documentation](https://jekyllrb.com/)
+ [Nice guide for Windows users](http://jekyll-windows.juthilo.com/)
+ Another [Jekyll installation guide](http://yizeng.me/2013/05/10/install-jekyll-3-on-windows/) with a very helpful part about troubleshooting
+ For those unfamiliar with GitHub, [here](https://guides.github.com/activities/hello-world/) is a friendly and straightforward overview
+ Using Windows command line only? This may not always be the best idea. Check out [Git Bash](https://git-for-windows.github.io/)

In the next post we will take a look at customizing your blog and running it on your own domain if you preferred it over the Git Hub default one.

Now get down to work, I keep my fingers crossed for your awesome project! :)





