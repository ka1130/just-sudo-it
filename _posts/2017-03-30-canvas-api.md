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

Two posts ago I promised to tell you something more about the HTML5 technology that I use to draw and animate Boids, that is the `<canvas>` element. As you have probably guessed, it is basically just an HTML tag - but its possibilities are truly impressive. With the use of the simple `<canvas>` element and JavaScript you can create advanced games, multimedia applications and charting. This is because canvas is very fast and efficient so it can perform complicated calculations and animations. Since canvas is pixel-based API, you can go as far as pixel manipulation, creating for instance some impressive filters for your photos. The possibilities are endless!

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



