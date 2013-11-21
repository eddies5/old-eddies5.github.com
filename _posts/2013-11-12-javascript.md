---
layout: post
title: "JavaScript Object Hierarchy & Inheritance: The Reaction."
categories: [School]
tags: [CS371P]
---

I chose to read [Object Hierarchy and Inheritance in JavaScript](http://www.cs.rit.edu/~atk/JavaScript/manuals/jsobj/) for CS371P's Paper Blog credit. I'm fortunate enough to have been exposed to JavaScript before, and I was interested in really learning more about the idiosyncrasies of it.

I think I've realized something and I want to share my realization with you, but in order to do that let me set up some facts:

* JavaScript is an object-oriented language based on _prototypes_ not classes like Java.
* A prototypical object is simply a base template object.
* It's said that JavaScript simply has objects.
* At runtime you can add/remove properties from an object in JavaScript.

I think it's because you can add/remove properties from an object at runtime that there are no classes in JavaScript. Classes don't change during an execution for Java, so that's why it makes sense that Java has classes. Since you can add/remove properties from an object in JavaScript it makes sense that there are no classes.

An Employee/Manager object inheritance structure example was given in the paper. The example simply defined a constructor function; there is no special constructor method like there is in Java. I had a question while looking at these constructors: Why is it that these constructor functions don't return anything, yet when they are called we are guaranteed to have an object be returned? Thankfully, the paper addresses this in the "More Flexible Constructors Section." When you call a constructor function:

{% highlight javascript %}
var e = new Employee()
{% endhighlight%}

The `new` keyword creates a generic object and that object is passed to the Employee constructor function as the value of the `this` keyword. On return from the Employee constructor the object that was created is assigned to the `e` variable.

The inheritance hierarchy was created by setting the prototype properties to other constructor functions:

{% highlight javascript %}
Manager.prototype = new Employee;
{% endhighlight%}

I had to go run some tests too see what was happening here:

{% highlight javascript %}
function Mammal() {
	console.log('Mammal()');
}
function Cat() {
	console.log('Cat()');
}
Cat.prototype = new Mammal;
t = new Cat();
{% endhighlight%}

Output:

`
Mammal()
Cat()
`

So it appears that when you create a new Cat, the Mammal's constructor function gets called first and then the Cat constructor function gets called. I still have one unanswered question: Why is it `new Mammal` and not `new Mammal()`? I tried both versions and there seemed to be no effect on the output.

Another neat thing about JavaScript is that when you search for a property of an object, the search doesn't stop if the property is not found in that object. The search continues up the "prototype chain." During runtime one is allowed to add properties to a JavaScript object. I also learned that when you add a property to the prototype of an object all objects that inherit from that prototype inherit that property.

I have used JavaScript in a professional setting and I did not know all of these details about JavaScript. The JavaScript I've used hasn't really been object oriented (I think). Most of my JavaScript has leaned more towards functional programming, so I'm glad I was able to see how JavaScript can be object oriented. This was a very good article; it provided some of the details that I'd expect Downing to provide when teaching a language. Overall I recommend you read the article.
