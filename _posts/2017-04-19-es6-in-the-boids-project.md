---
layout: post-sidebar
title: "6 ES6 features I use in the Boids project (and work great anywhere!)"
date: 2017-04-19 09:00:12
categories: dsp2017 coding
author_name : Kamila
author_url : /author/kamila
author_avatar: kamila
show_avatar : true
read_time : 30
feature_image: feature-es6
show_related_posts: true
comments: true
square_related: recommend-es6
---
The introduction of ECMAScript 2015 standard, also known as ES6, is a quantum leap for JavaScript that the language hadn’t seen since 2009. I didn’t realize the significance of the changes until very recently when I started to learn the new ES6 features. Some of them are pretty self-explanatory, the others took me more time to comprehend - and there’s still a bunch of stuff I have only blurry idea about. Since the best way of learning to code is actually… to code, I decided to introduce ES6 to the Boids project. And you know what, it considerably simplified and clarified the work. So I decided to share some insight with you. Here are the 6 ES6 features I have used when programming Boids.

## 1. Block-Scoped Constructs: Let and Const

ES6 has introduced two new ways of defining variables. Apart from `var` we have also now `let` and `cost`. Now what are `let` and `const` for and why was `var` not enough? 

The main problem with `var` was its scope, which is a function scope, whereas `let` and `const` are block-scoped. It means they only exist within the current block represented by a pair of curly braces: `{}`: it may be a block within an `if` statement, a loop - or you can simply create one and put your `let` or `const` inside. This helps avoid common developers’ problems and makes JavaScript behave more predictably to those used to work in other languages, such as Java, C or C++.

Also, when using `let` and `const` you do not fall into the hoisting trap, which you may welcome with relief as many people find the hoisting idea pretty distressing. This is because `let` and `const` remain uninitialized until they are declared. The timespan before `let` or `const` initialization is called “Temporal Dead Zone” (TDZ). For more in-depth explanation, have a look [here](https://ponyfoo.com/articles/es6-let-const-and-temporal-dead-zone-in-depth).

Next, `let` and `const` declarations cannot be reassigned. So you won’t accidentally overwrite your variables. You can only update the value of `let`. By contrast, `const` declaration is created to keep values that will not be changed. Some programmers say it’s best to use `const` by default and `let` only in special cases, when the value of the variable is bound to be changed (such as the counter in your `for` loop).

Last but not least, `let` and `const` do not become properties of the global object, in case you defined them globally (which you should never do by the way). The same is true for the new ES6 Classes - and I’ll tell you more about them later in this post.

Of course, you can still use `var` if you want, there's nothing wrong with that. Just be aware of it's characteristics and give the new constructs a try too see if you feel commfortable working with them.

## 2. Arrow Functions

A cool new feature of ES6 are arrow functions, also referred to as fat-arrow functions. Their name stems from the token they use: `=>` which looks… well, like a fat arrow. Arrow functions are just a more concise syntax for writing function expressions. They also handle `this` bindings in functions in a different way which takes two issues. First, they
don’t rebind the value of `this` when you use an arrow function inside of another function. Second, the value of `this` inside of a function can never be changed. 

Let’s see how it works in practice. We’ll use a `map` method on an array of numbers to sum them up:

{% highlight javascript %}
var nums = [10, 20, 30];

nums.map(function(num) {
return num + num;
});
{% endhighlight %}<br>
Now with the use of ES6 standard we can simplify it to just:

{% highlight javascript %}
var nums = [10, 20, 30];

nums.map(num => num + num);
{% endhighlight %}<br>
Whoaa, what has just happened here? Well, first, we’ve got rid of the `function` keyword. Next, we’ve replaced the `{}` curly braces with the fat-arrow token: `=>`. Then, we’ve made use of the fact that arrow function have so-called implicit returns, which means that we could omit the `return` keyword if it was a simple one-liner. We couldn’t have done this if the `return` expression had multiple lines. And last, since we’ve had just one parameter in the function, we could omit the parentheses around it as well. Doesn’t it look gorgeously nice and clear?

What you need to bear in mind when using arrow functions is the behaviour of `this` that I mentioned in the beginning of this section. So, remember that in an arrow function `this` does not get rebound, it is just inherited from its parent’s scope. Imagine for instance a situation when you want to trigger an event on an element using the `addEventListener()` method. You pass this method a function as a second parameter and `this` in such function gets rebound to an element on which the event was performed. If you tried now to exchange the regular function expression inside of an `addEventListener()` method and printed `this` to the console, you may find out, it directs you to the `Window` object! This would be true if you created a function in a global scope. Conclusion: when working with events or whenever you WANT `this` to get rebound, go for a regular function expression. 
On the other hand, in situations when you’d write something like `var self = this`, thus needed a fixed `this`, using an arrow function will makes things much cleaner.

And the last thing to remember about arrow functions: they are really handy when working with **anonymous** functions. You cannot use this shorthand if your function is named.

## 3. Default Parameters

Another cool new feature of ES6 are default functions parameters. By declaring the defaults for a function you initialize it with default values of your choice. They get passed to a called function when an argument is either omitted or `undefined`. 

Let’s say you want to initialize a simple `sum` function with default values. This is how you do it:

{% highlight javascript %}
function sum(a=10, b=2) {
  console.log(a+b);
}
sum(5, 4); // => 9
add(); // => 12
{% endhighlight %}<br>
That simple! You just assign the default values to the function you declare with the use of an equal sign. Nice, easy and really handy at times.

## 4. Template Literals 

This one is easy to grasp as well. You have surely done things like this in the past:

{% highlight javascript %}
function hello(name) {
    console.log("Hello " + name + ", nice to meet you");
}
{% endhighlight %}<br>
The `+` thing looks pretty awkward especially to the newbies. Now we can handle such issues much simpler using string interpolation (you may be familiar with this idea if you use Sass). What you need is a pair of backticks `` `code` `` to wrap your expression and a dollar sign followed by a pair of curly brackets which keep an expression (of any kind), parameter or variable. The above code could thus be rewritten like so:

{% highlight javascript %}
function hello(name) {
    console.log(`Hello ` ${name}, nice to meet you`);
}
{% endhighlight %}<br>
Moreover, template literals support multiliners. That means you no longer need to write weird things like:

{% highlight javascript %}
var helloEs5 = 'Hello\n' +
'  World\n';
{% endhighlight %}<br>
ES6 will understand you’d like to keep line breaks if you rewrote the above declaration in this way:

{% highlight javascript %}
const helloEs6 = `Hello
  World
`;
{% endhighlight %}<br>
Again, clean, simple and self-explanatory snippet of code. And again, just a piece of syntactic sugar, yet since most of us like sweets - why not help yourself? :)

## 5. Destructuring

At this point I actually ended up dropping out destructuring from the project but who knows where the further work will bring me. Anyways, destructuring is a really nifty way of extracting data from arrays and objects and assign them to variables. Let’s have a look at the following example:

{% highlight javascript %}
let names = ["Sally", "James", "Ben"];
let [name1, name2, name3] = names;

console.log(name1);  //"Sally"
console.log(name2);  //"James"
console.log(name3);  //"Ben"
{% endhighlight %}<br>
Instead of referring each object in the array with the use of its index value, we can simply destructure the array, passing to the square brackets the names of the variables. If we passed less names than the amount of elements in the array, nothing will happen - the excess elements will be ignored.

Destructuring works pretty the same way with objects.

{% highlight javascript %}
const person = {
  firstname: "John",
  lastname: "Smith",
  country: "Canada" 
  }

let { firstname, lastname, country } = person;

console.log(firstname);  //"John"
console.log(lastname);  //"Smith"
console.log(country);  //"Canada"
{% endhighlight %}<br>

## 6. Classes


## Babel


## Summing Up & Learning Resources


