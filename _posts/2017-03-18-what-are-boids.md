---
layout: post-sidebar
title: "What the Boids?"
date: 2017-03-18 18:20:02
categories: dsp2017
author_name : Kamila
author_url : /author/kamila
author_avatar: kamila
show_avatar : true
read_time : 15
feature_image: feature-laptop
show_related_posts: true
comments: true
square_related: recommend-laptop
---
## What is this project about?

Ever heard about artificial life programs? Sure you have, Internet is full of information, projects and games based on natural life’s simulation. Consider [Conway’s Game of Life](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life), for instance, which simulates “colonies” growing or dying depending on how crowded or lonely the single cells are. It is still purely math-based but it very believably resembles a kind of natural life patterns, where cells are forming generations connoting almost a kind of collective intelligence, especially if they are given a really big space to colonize. Since I have lately programmed [JavaScript implementation of Game of Life](https://ka1130.github.io/Game-of-Life/src/), I decided to challenge myself with something presumably much more demanding.

## The “Boids” idea

As per [Wikipedia’s definition](https://en.wikipedia.org/wiki/Boids), Boids is an artificial life program, developed by Craig Reynolds in 1986, which simulates the flocking behaviour of birds. I have encountered two derivations of the term “boids”. One says it is a shorthand for “bird-oid”, in other words, “bird-like” objects. The other suggests it stems from the way that New Yorkers pronounce the word “birds”. Leaving aside the story of the term, Reynold’s Boids model (also referred to as flocking algorithm) follows three simple rules:

+ **separation**: steer to avoid crowding
+ **alignment**: steer towards the average heading of local flockmates
+ **cohesion**: steer to move toward the average position of local flockmates

What is phenomenal about Reynold’s model is that using these plain rules only on single units it generates behaviour strongly resembling a real flock’s one. Just as in the Game of Life the result is surprisingly complex and realistic. Boids are one of many experiments in the field of so-called swarm intelligence(https://en.wikipedia.org/wiki/Swarm_intelligence) characterized by the lack of centralized control agent: each boid follows its own rules, still resulting in a surprising group behaviour.

Here is a nice visualization and further explanation of the idea:

(https://www.youtube.com/watch?v=QbUPfMXXQIY&t=36s)

##My goal

The purpose of my project is to create a JavaScript implementation of boids. I know I am definitely not the first one to try - there even are whole libraries and scripts available to use freely. However, I will try to figure the thing out myself, preferably with pure Vanilla JS. We’ll see what I’ll end up with. Keep your fingers crossed, I will report you soon about the project’s state!