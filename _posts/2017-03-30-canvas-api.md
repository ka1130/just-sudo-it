---
layout: post-sidebar
title: "The canvas API"
date: 2017-03-30 12:02:13
categories: dsp2017
author_name : Kamila
author_url : /author/kamila
author_avatar: kamila
show_avatar : true
read_time : 10
feature_image: feature-canvas
show_related_posts: true
comments: true
square_related: recommend-canvas
---

Two posts ago I promised to tell you something more about the HTML5 technology that I use to draw and animate Boids, that is the `<canvas>` element. As you have probably guessed, it is basically just an HTML tag - but its possibilities are truly impressive. With the use of the simple `<canvas>` element and JavaScript you can create advanced games, multimedia applications and charting. This is because canvas is very fast and efficient so it can perform complicated calculations and animations. Since canvas is pixel-based API, you can go as far as manipulating pixels, creating for instance some impressive filters for your photos. The possibilities are endless!

## Overview

The canvas API itself is not really complicated in terms of the amount of knowledge to grasp. All the methods and properties are nicely put together on the [w3schools reference](https://www.w3schools.com/tags/ref_canvas.asp). Yes, I am aware of the [controversy behind w3schools](https://www.impressivewebs.com/w3schools-ugly-bad-good/) and I admit it’s definitely not the ultimate choice for learning but when it comes to getting to know HTML5, especially if you’re fresh to some of its features, it’s a nice start. Having said that, you should definitely check out the [MDN documentation for canvas](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API) which provides you with in-depth information on all the API’s features.

Basically, canvas API consists of a set of **functions** and **properties**. **Functions** can be divided as per their purpose like so:
+ **line and shape** functions (for example: `arc`, `fill`, `rect`, `stroke` etc.)
+ **text** functions (`fillText`, `measureText`, `strokeText`)
+ **transform** functions (`save`, `restore`, `rotate`, `scale`, `transform`, `translate`)

In addition to the functions, canvas API provides you with a set of **properties** that are basically designed to let you style the elements before they get drawn on canvas. Some of these properties are: `width`, `height`, `font`, `fillStyle`, `globalAlpha`, `globalCompositeOperations`. OK, let’s get down to actual coding so that you can check yourself how to make use of canvas. Once you get the knack of it, I promise, you’ll have fun!

## Basic usage

First, let’s insert canvas on our website. In a place of your choice simply put:

{% highlight javascript %}
<canvas id=”myCanvas” width=”400” height=”400”>
	Your browser does not support canvas
</canvas>
{% endhighlight %}<br>
No need to say that the above id, width, height and fallback text is up to you. You might be tempted to omit width and height and choose to style those in CSS but don’t do that, it won’t work. You need to define width and height directly in the `<canvas>` tag - or in JavaScript. Anyways, it’s best to start from setting initial values here, in HTML.

OK, you have canvas in our layout but still, you won’t see anything at this point. The canvas is there but nothing’s going on on it. Time to jump into your JavaScript file.

First, we need to catch our canvas to a variable. Let’s make use of the new variable declarations introduced by ES6 (more on that in the future post, I plan to show you all the ES6 features I use in the project). 

{% highlight javascript %}
const canvas = document.getElementById(“myCanvas”);
{% endhighlight %}<br>
Now we need to define the context in which we want to work. In most of the cases, you will need a 2D context. The canvas element has a special method for that called `getContext`.

{% highlight javascript %}
const ctx = canvas.getContext(“2d”);
{% endhighlight %}<br>
Finally, let’s draw something simple like rectangle:

{% highlight javascript %}
ctx.fillRect(200, 200, 100, 100);
{% endhighlight %}<br>
The `fillRect` method takes four parameters: `x`, `y`, `width` and `height`. The X and y coordinates are where the rectangle’s upper-left corner is. The default color is black, that’s why you can see a black rectangle on your canvas now even though you didn’t set any styling. Actually if you do want to style your components anyhow, you have to define the visual side first. Let’s add some colour to our rectangle, say, orange for example. Now the code will look like this:

{% highlight javascript %}
ctx.fillStyle = "#ffa500";
ctx.fillRect(200, 200, 100, 100);
{% endhighlight %}<br>
The same way, you can create a rectangle with a stroke, defining its color first:

{% highlight javascript %}
ctx.fillStyle = "#ffa500";
ctx.strokeStyle = "#005aff";
ctx.fillRect(200, 200, 100, 100);
ctx.strokeRect(200, 200, 100, 100);
{% endhighlight %}<br>
This will add a blue stroke to your initial rectangle. You might want to alter the stroke’s width - and that’s simple too. The only thing it takes is a `lineWidth` method where you define the line’s width in pixels and pass it as a numeric value like so:

{% highlight javascript %}
ctx.fillStyle = "#ffa500";
ctx.strokeStyle = "#005aff";
ctx.lineWidth = 10;
ctx.fillRect(200, 200, 100, 100);
ctx.strokeRect(200, 200, 100, 100);
{% endhighlight %}<br>
Cool, you get the point! The very introduction is behind us, let’s move on to other shapes.

## Run rings around the squares!

Time for something slightly more complex: curves. In the case of Boids I initially wanted to represent them as simple circles. To do that, we need the `arc` method that lets you draw curves, ovals and circles. As you remember, we need to define styles first. How about some spring colors and stroke of 5px?

{% highlight javascript %}
ctx.fillStyle = "#bcd664";
ctx.strokeStyle = "#54a244";
ctx.lineWidth = 5;
{% endhighlight %}<br>
Now we need a method to start the path:

{% highlight javascript %}
ctx.beginPath();
{% endhighlight %}<br>
...and draw a curve using the canvas `arc` method. The `arc` method takes 5 obligatory parameters and 1 optional. These are:
+ **x** (the x-coordinate of the center of the circle)
+ **y** (the y-coordinate of the center of the circle)
+ **r** (the radius)
+ **sAngle** (the starting angle, in radians, where 0 is at the 3 o'clock position of the arc's circle)
+ **eAngle** (the ending angle, in radians)
+ **counterclockwise** (this one is optional and takes a boolean value)

Let’s imagine we’d like the arc to be drawn in the middle of the canvas, with the radius of 20px, taking 90 degrees. Calculating radians may be a bit counterintuitive for you (it is for me!) so why not get ourselves a little helper function that will take degrees and return radians? Like so:

{% highlight javascript %}
function calculateRadians(degrees) {
    return degrees * Math.PI / 180;
}
{% endhighlight %}<br>
Now let’s move back to our arc and draw it!

{% highlight javascript %}
ctx.beginPath();
ctx.arc(canvas.width / 2, canvas.height / 2, 80, 0, calculateRadians(90));
ctx.stroke();
ctx.closePath();
{% endhighlight %}<br>
A riddle for you: how to draw a circle with fill only, no stroke, as in the case of rough-and-ready Boids. Yeah, I know that you know. :)

{% highlight javascript %}
ctx.fillStyle = "#bcd664";

ctx.beginPath();
ctx.arc(canvas.width / 2, canvas.height / 2, 40, 0, calculateRadians(360));
ctx.fill();
ctx.closePath();
{% endhighlight %}<br>

## Basic animation

Last thing I’m gonna show you is a simplest animation that will show you some concepts of moving elements around on canvas. 





