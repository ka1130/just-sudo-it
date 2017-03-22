---
layout: post-sidebar
title: "The canvas API"
date: 2017-03-30 09:02:13
categories: dsp2017
author_name : Kamila
author_url : /author/kamila
author_avatar: kamila
show_avatar : true
read_time : 40
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
<canvas id="myCanvas" width="400" height="400"
	Your browser does not support canvas
</canvas>
{% endhighlight %}<br>
No need to say that the above id, width, height and fallback text is up to you. You might be tempted to omit width and height and choose to style those in CSS but don’t do that, it won’t work. You need to define width and height directly in the `<canvas>` tag - or in JavaScript. Anyways, it’s best to start from setting initial values here, in HTML. I would also suggest adding some basic styling to the canvas so that you can see clearly where it is. Let’s move to the stylesheet and add some CSS declarations like:

{% highlight javascript %}
#myCanvas {
    border: 1px solid black;
}
{% endhighlight %}<br>
Now that we have our bare canvas placed on the layout, it’s time to jump into the JavaScript file. First, we need to catch our canvas to a variable. Let’s make use of the new variable declarations introduced by ES6 (more on that in the future post, I plan to show you all the ES6 features I use in the project). 

{% highlight javascript %}
const canvas = document.getElementById("myCanvas");
{% endhighlight %}<br>
Now we need to define the context in which we want to work. In most of the cases, you will need a 2D context. The canvas element has a special method for that called `getContext`.

{% highlight javascript %}
const ctx = canvas.getContext("2d");
{% endhighlight %}<br>
Finally, let’s draw something simple like a rectangle:

{% highlight javascript %}
ctx.fillRect(200, 200, 100, 100);
{% endhighlight %}<br>
The `fillRect()` method takes four parameters: `x`, `y`, `width` and `height`. The x and y coordinates define the rectangle’s upper-left corner's position. The default color is black, that’s why you can see a black rectangle on your canvas now even though you didn’t set any styling. Actually if you do want to style your components anyhow, you should define the visual side first. Let’s add some colour to our rectangle, say, orange for example. Now the code will look like this:

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

Last thing I’m gonna show you is a simplest animation that will show you some concepts of moving elements around on canvas. Basically, drawing on canvas consists in sequential clearing the canvas and redrawing the element on a new position. In case you perform any transformations on the element while animating it, you will also need to store and restore the canvas. We won’t transfigure our circle anywise so we can skip these steps.

To schedule the updates you can use one of the following functions: `setTimeout(fn, delay)`, `setInterval(fn, delay)` or` requestAnimationFrame(callback)`. I suggest you go for the thirs option since it’s best in terms of performance of your animation. 

To schedule the updates you can use one of three functions: `setTimeout(fn, delay)`, `setInterval(fn, delay)` or` requestAnimationFrame(callback)`. I suggest you go for the thirs option since it’s best in terms of performance of your animation. Paul Irish explained very nicely [the way `requestAnimationFrame()` method works](https://www.paulirish.com/2011/requestanimationframe-for-smart-animating/) and why to choose it over `setTimeout()` or `setInterval`. The post is old but still valid, just the support of the browser is now almost complete, it’s just Opera Mini that doesn’t understand the deal. Anyways, has anyone of you ever used Opera Mini? Personally, I don’t even know how dude looks like!. ;)

OK, so how to use the `requestAnimationFrame()` method? We use it on a global object (that is, in our case, window) and we pass it a callback function which will run each time the browser performs drawing on the screen. So here’s the basic syntax:
window.requestAnimationFrame(callbackFunction);
Which is, as you know, the same thing as:
requestAnimationFrame(callbackFunction);
With that in mind, let’s write a core fore our animate() function which will run the `requestAnimationFrame()` method, calculate next position and then re-draw it.

{% highlight javascript %}
function animate() {
    requestAnimationFrame(animate);
        // calculate next position
    draw();
}
{% endhighlight %}<br>
Next, let’s define the `draw()` function. It will run in a multiple sequence so the first thing you need to do is clearing the canvas before redrawing the element on the next position. To clear the canvas, you will use the `clearRect()` method on the canvas’ context (as you remember, we keep it in a variable called `ctx`). The `clearRect()` method takes the following parameters:
+ **x** (the x-coordinate of the upper-left corner of the rectangle to clear)
+ **y** (the y-coordinate of the upper-left corner of the rectangle to clear)
+ **width** (of the rectangle to clear, in px: in our case this will be the width of the whole canvas)
+ **height**

Now, the foundation of your `draw()` function will look like this:
{% highlight javascript %}
function draw() {
	ctx.clearRect(0, 0, canvas.width, canvas.height);
		//drawing goes here
}
animate();
{% endhighlight %}<br>
Having this basis, let’s think of how we will actually deal with moving our element around. For the very beginning, we’ll move the element on x-coordinate only asking it to revert the direction of the movement once the element hits the border of the canvas. We need three variables:` x` and `y` for initial position and `speed` for… yeah, the speed. :)
Let’s declare these at the very beginning, above the `animate()` and `draw()` functions:

{% highlight javascript %}
let x = 40;
let y = 40;
let speed = 5;
{% endhighlight %}<br>
At this moment we can complete the `draw()` function and make it draw a circle like we did before in this tutorial:

{% highlight javascript %}
function draw() {
	ctx.clearRect(0, 0, canvas.width, canvas.height);
	ctx.fillStyle = "#bcd664";

	ctx.beginPath();
	ctx.arc(x, y, 40, 0, calculateRadians(360));
	ctx.fill();
	ctx.closePath();
}
{% endhighlight %}<br>
Finally, we will move the circle on the x-axis by incrementing the x variable which defines the circle’s horizontal position:

{% highlight javascript %}
function animate() {
    requestAnimationFrame(animate);
    x += speed;

    if (x <= 40 || x >= 360) {
        speed = -speed;
    }

    draw();
}
{% endhighlight %}<br>
OK, what’s going on here and where are these `40` and `360` values come from?








