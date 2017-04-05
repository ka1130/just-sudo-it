---
layout: post-sidebar
title: "A Gulp of Node.js"
date: 2017-04-04 13:10:14
categories: dsp2017 coding
author_name : Kamila
author_url : /author/kamila
author_avatar: kamila
show_avatar : true
read_time : 45
feature_image: feature-gulp
show_related_posts: true
comments: true
square_related: recommend-gulp
---

Working on a website project is not only about writing code in HTML, CSS and JS. When it comes to deployment or using preprocessors for instance, you need some tasks to be done repeatedly, like:
+ concatenating and minifying CSS and JavaScript files
+ compiling Sass to CSS (I highly recommend writing in Sass rather than pure CSS, especially if you work on a little bit bigger project)
+ reloading your browser each time you introduce changes to your styles
+ compressing images
+ watching Sass for changes
+ ...and so on :)

This is when tools like Gulp or Grunt come in handy. In this tutorial I will show you some basics of Gulp which I find easier than Grunt, with API is a bit cleaner and faster performance. That doesn’t mean it’s overall better, it’s just what I work with on a daily basis and can tell you something about.

## All cool but what is Gulp actually?
In simplest terms, Gulp is an automation tool, or a JavaScript task runner, that takes tons of tedious, repetitive work off your hands. It is built on Node.js so you will define your task in JavaScript in so-called gulpfile.js. Pretty nice for a Front-End Developer.

## Let’s get started

You will get a clear impression of how it all works if you just try yourself - and it’s pretty simple. What we need to do is install Node first. Node is a platform that lets you run JavaScript outside of a browser. Node itself is a C++ program but don’t worry about that, you only need JavaScript to handle your tasks. What’s cool about Node is its modules which you can also refer to as kind of plugins or files that keep specific functions to run them when needed. 

Now let’s go ahead and install Node. It is possible you already have Node on your machine so open up your console and run:

{% highlight javascript %}
node --version
{% endhighlight %}<br>
If your console answers with a version number, you’re good to go. If not, go to the [Node.js website](https://nodejs.org/en/), download and install Node. The Node Package Manager (npm) should have been installed too, so run this command to check it:

{% highlight javascript %}
npm -v
{% endhighlight %}<br>
As before, your console should answer with the npm’s version number.

## Installing Gulp

Now that we have our Node platform ready, let’s proceed and install Gulp. Simply type this in your console:

{% highlight javascript %}
npm install -g gulp
{% endhighlight %}<br>
to install Gulp globally. If you are on Mac or Linux you should precede this command with `sudo`. This is something you do once and for good. You will also need to install Gulp locally in your project’s folder, so navigate there in your console (nice trick: type `cd + space` and then simply drag & drop your folder inside the console; hit enter and you’re there!). 

Gulp is a Node Package Manager module so let’s initialize npm like this: 

{% highlight javascript %}
npm init
{% endhighlight %}<br>
Given this command, the console will ask you a series of questions. You can give them specific answers or simply keep hitting Enter for the defaults until the process is finished. You will probably need to stop the task manually once you see this line:

{% highlight javascript %}
Is this ok? (yes)
{% endhighlight %}<br>
Hit `Ctrl + C` to finish. Alternatively, if you want to go with the defaults and omit the questions’ part, simply run:

{% highlight javascript %}
npm init --yes 
{% endhighlight %}<br>
At this point in your directory’s root your will see a new file called **package.json**, containing initial .json configuration. Here’s where next modules required will be added as so-called dependencies. This will help you build reusable package.json file that will install all the dependencies in your next projects once you simply run `npm init`. This is also why you will need to add `--save-dev` to the following installations commands. I will show you exactly how in a moment.

Now let’s move on to install Gulp locally in your project. Go ahead with the command below:

{% highlight javascript %}
npm install --save-dev gulp 
{% endhighlight %}<br>
If you take a look at your package.json file, you’ll notice Gulp added to devDependencies. Good, let’s create our first task!


## “Hello World” with Gulp

In order to create Gulp tasks we need a special file called gulpfile.js. Open your editor, ask it for a new file and save it as `gulpfile.js`. As per the old programming tradition, let’s build a “Hello World” task to get acquainted with the environment. In order to define it, go ahead and type this at the beginning of your gulpfile.js:

{% highlight javascript %}
var gulp = require(“gulp”); 
{% endhighlight %}<br>
The string in the parenthesis stands for the name of the plugin. This way we are asking Node to look inside the `node_modules` (you will notice this folder created in your project’s file once you’ve installed Node) and search for a given module (in this case it’s Gulp). Now to actually set our task we need the following syntax:

{% highlight javascript %}
gulp.task();
{% endhighlight %}<br>
There will be two parameters inside this function:
1. the name of a task as a string (the name is up to you)
2. the function to perform

So, if we would like to log “Hello World” in the console and we want to call the task “hello”, this is how we will build our task:

{% highlight javascript %}
gulp.task(“hello”, function() {
	console.log(“Hello World!”);
});
{% endhighlight %}<br>
Try it out! In your console run:

{% highlight javascript %}
gulp hello
{% endhighlight %}<br>
And the console will answer logging “Hello World!” just as expected.

Below you can see a table explaining 4 simple Gulp APIs. <br>
Isn't it super nice and easy?
<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:bold;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg .tg-yw4l{vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-yw4l">API</th>
    <th class="tg-yw4l">Purpose</th>
  </tr>
  <tr>
    <td class="tg-yw4l">gulp.task</td>
    <td class="tg-yw4l">Define a task</td>
  </tr>
  <tr>
    <td class="tg-yw4l">gulp.src</td>
    <td class="tg-yw4l">Read files in</td>
  </tr>
  <tr>
    <td class="tg-yw4l">gulp.dest</td>
    <td class="tg-yw4l">Write files out</td>
  </tr>
  <tr>
    <td class="tg-yw4l">gulp.watch</td>
    <td class="tg-yw4l">Watch files for changes</td>
  </tr>
</table>
<br>

Now that you have the basic knowledge of creating tasks in Gulp, let’s try something more practical.

## Compiling Sass to CSS 

If you work with preprocessors like Sass or Less, you need your .scss files to be compiled to .css so that the browser understands what you want. It can be easily done with Gulp. First, you need to install the special module for that:

{% highlight javascript %}
npm install --save-dev gulp-sass
{% endhighlight %}<br>
Now in your gulpfile.js after the first gulp variable declaration add another one:

{% highlight javascript %}
var sass = require(“gulp-sass”);
{% endhighlight %}<br>
Let’s define our task. I called mine “sass”. Here’s how it looks like in my case, we will go through this snippet in a second:

{% highlight javascript %}
gulp.task("sass", function() {
    gulp.src("src/scss/main.scss")
        .pipe(sass())
        .pipe(gulp.dest("src/css/"));
});
{% endhighlight %}<br>
In the `gulp.src()` you put your input path. In my case I have following structure `project_folder` **>** `src` (a folder where I put my working files which I then deploy for production into the dist folder) **>** `scss` (where I keep my Sass folders and main.scss file) **>** `main.scss` (keeping all the imports from Sass folders). Adjust the path to match your project’s structure.

The `pipe` method is used to chain multiple tasks together. The consecutive “pipes” are put in new lines for readability.

The `gulp.dest()` part defines where your final .css file will go.

Once you’ve set the task ask the console to compile your Sass like this:

{% highlight javascript %}
gulp sass
{% endhighlight %}<br>
The `sass` method can take a configuration object as a parameter. Let’s do that:

{% highlight javascript %}
gulp.task("sass", function() {
    gulp.src("src/scss/main.scss")
        .pipe(sass({
            outputStyle: 'expanded',
            errLogToConsole: true
        }))
        .pipe(gulp.dest("src/css/"));
});
{% endhighlight %}<br>
What’s happening here is we ask Gulp to compile Sass files to expanded style in .css and we also want to see errors in our console, if they occur. So what is this output style issue? It is simply how our final .css will look like: whether it will be minified or more human-friendly.
We have four options to choose from:
+ :nested
+ :compact
+ :expanded
+ :compressed

[Here is](http://inchoo.net/dev-talk/tools/sass-output-styles/) how each of them looks like.

I usually go for expanded style which seems most legible to me but the choice is completely up to you.

## Sourcemaps

The next thing I’m going to cover is sourcemaps. Having sourcemaps built into your sass task is a must when it comes to debugging your code. Imagine having an issue in your .css file and trying to fix it with your browser’s Dev Tools. If you try to inspect an element on your website now, you will see a specific line in the .css file. This may not be what you want, especially if you use a compressed output style. You'd rather wish the Dev Tools to point out the .scss file and specific line number inside. This is what you need sourcemaps for. Let’s install them and add to devDependencies:

{% highlight javascript %}
npm install gulp-sourcemaps --save-dev
{% endhighlight %}<br>
Now we need to rebuild the “sass” task like this:

{% highlight javascript %}
gulp.task("sass", function() {
    gulp.src("src/scss/main.scss")
        .pipe(sourcemaps.init())
        .pipe(sass({
            outputStyle: 'expanded',
            errLogToConsole: true
        }))
        .pipe(sourcemaps.write())
        .pipe(gulp.dest("src/css/"));
});
{% endhighlight %}<br>
Once you’re done, try to inspect a chosen element of your site with Dev Tools. You should see them pointing to the source .scss file and a code line inside of it.

## Listening for changes

When working on your Sass project you probably wouldn’t like to be forced to run gulp sass each time you save changes to the stylesheet. I assume you’d rather have your changes introduced to the .css file each time you change one of your .scss stylesheets. You can achieve this with a Gulp watcher that will keep track of the changes and introduce them immediately into the destination .css.

Let’s define this task:

{% highlight javascript %}
gulp.task("watch", function() {
    gulp.watch("src/scss/**/*.scss", ["sass"]); 
});
{% endhighlight %}<br>
As you have probably guessed, the first parameter is a source path ( `**` means I want Gulp to look for all of the files in my scss folder and then get all of the files with the .scss extension). The second parameter is an array of tasks for the watcher to keep track of. In our case, we only want to watch for “sass”.

You already know how to run this task:

{% highlight javascript %}
gulp watch
{% endhighlight %}<br>
This way we start the watch mode. If you want to stop it, hit `Ctrl + C`.

## Synchronized browser testing

The last thing I am going to cover is something which I hope you’ll find really neat: live reloading your web project on your browser. We can handle this with a BrowserSync plugin. It is not a Gulp module but it doesn’t matter, we can use it anyhow. Let’s install it:

{% highlight javascript %}
npm install browser-sync gulp --save-dev
{% endhighlight %}<br>
...and define as a variable in our gulpfile.js:

{% highlight javascript %}
var browserSync = require(“browser-sync”);
{% endhighlight %}<br>
Time to create a task called “sync” (or anything you like) which will look like this:

{% highlight javascript %}
gulp.task("sync", function() {
    browserSync.init({
        server: "src/"
    });
});
{% endhighlight %}<br>
Inside the `browserSync.init()` function we define a configuration object which in this case contains simply the path to our project. Since I usually keep all my source files in a folder called “src” (as mentioned above), I have declared `server: src/`. If you decided to put all your files directly within your main project’s directory, your task may look like this:

{% highlight javascript %}
gulp.task(“sync”, function() {
    browserSync.init({
        server: {
            baseDir: "./"
        }
    });
});
{% endhighlight %}<br>
The last thing to do here is adding browserSync to our chain in “sass” task:

{% highlight javascript %}
gulp.task("sass", function() {
    gulp.src("src/scss/main.scss")
        .pipe(sass({
            outputStyle: 'expanded',
            errLogToConsole: true
        }))
        .pipe(gulp.dest("src/css/"))
        .pipe(browserSync.stream()); 
});
{% endhighlight %}<br>
Let’s try it out! Run:

{% highlight javascript %}
gulp sync
{% endhighlight %}<br>
You’ll notice your website open up in a new tab of your default browser, on `localhost:3000`. Try entering any changes to your stylesheet - they will be introduced immediately without the need to reload your page. Cool, isn’t it?

## Default series of tasks

Or maybe you want to run more than one task at a time? No problem, you can do this with a `default` task (this time the name of the task does matter, it has to be called “default”). Let’s give it a try and define a default to run “sass”, “sync” and “watch” in a row. It’s a simple one-liner:

{% highlight javascript %}
gulp.task("default", ["sass", "sync", "watch"]);
{% endhighlight %}<br>
Guess what? Now you simply run:

{% highlight javascript %}
gulp
{% endhighlight %}<br>
and that’s all, Gulp will perform the array of tasks one by one. 

## Summary

OK, so here’s the final contents of your gulpfile.js if you followed along. The paths and tasks’ names may differ, of course, but you get the idea:

{% highlight javascript %}
var gulp = require("gulp");
var sass = require("gulp-sass");
var browserSync = require("browser-sync");
var sourcemaps = require("gulp-sourcemaps");

gulp.task("sass", function() {
    gulp.src("src/scss/main.scss")
        .pipe(sourcemaps.init())
        .pipe(sass({
            outputStyle: 'expanded',
            errLogToConsole: true
        }))
        .pipe(sourcemaps.write())
        .pipe(gulp.dest("src/css/"))
        .pipe(browserSync.stream());
});

gulp.task("sync", function() {
    browserSync.init({
        server: "src/"
    });
});

gulp.task("watch", function() {
    gulp.watch("src/scss/**/*.scss", ["sass"]); //table with a list of tasks
});

gulp.task("default", ["sass", "sync", "watch"]);
{% endhighlight %}<br>
Note that if you followed this tutorial and saved all dependencies in your package.json file, then in your next projects, given that you will need the same npm modules, you can simply copy `package.json` to the project’s root, navigate to the main project’s folder in your console and run `npm init` to install all the modules. Then, of course, you’ll need an analogous `gulpfile.js` - just remember to check all the paths, folder and tasks names to avoid errors.

I am aware I covered just a small part of what Gulp is capable of. What you can do more is, for example, optimizing your images, concatenating and minifying your files, preventing your watcher from stopping on error and much more. At this point however I believe you’re tired enough. :) If not, take a look at the documentation, really nice and clear:

+ <http://gulpjs.com/>
+ <https://www.npmjs.com/package/gulp>

That’s it for today, hope you enjoyed fiddling with Gulp. Test it yourself, play with the variety of possibilities, learn by trial and error: this way you’ll get best understanding and courage, both indispensable in any aspect of developer’s job. See you soon, happy coding! :)







