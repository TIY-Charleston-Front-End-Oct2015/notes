# Day 10 - Intro to the DOM api w/ native js and jQuery

And the fun continues!

Today we covered:

- The Document Object Model
- native js dom traversal/manipulation
- Introduction to jquery dom traversal/manipulation


### Native JavaScript DOM Traversals

## DOM - Document Object Model

From the MDN:
<blockquote>
The Document Object Model (DOM) is a programming interface for HTML, XML and SVG documents. It provides a structured representation of the document (a tree) and it defines a way that the structure can be accessed from programs so that they can change the document structure, style and content. The DOM provides a representation of the document as a structured group of nodes and objects that have properties and methods. Nodes can also have event handlers attached to them, and once that event is triggered the event handlers get executed. Essentially, it connects web pages to scripts or programming languages.
</blockquote>

The DOM is the means by which we will be interacting with our HTML in javascript.  This is how are are able to bind events and manipulate tags and markup on our page.

When a web page has loaded in the browser, you have access to the elements via the document object.  This document object has methods by which we can query different parts of the page to traverse and manipulate markup.

Today we covered a few of those methods:

### document.querySelectorAll()

`document.querySelectorAll(selectors)` can take any tag/class/id and it will return a set of matched elements.

Given the following page:
```html
<html>
  <head>
    <title>My Page</title>
  </head>
  <body>
   <header>
    <nav>
      <ul>
        <li>
          <a href="/home">Home</a>
        </li>
        <li>
        <a href="/about">About</a>
        </li>
        <li>
        <a href="/blog">Blog</a>
        </li>
      </ul>
    </nav>
  </header>

  </body>
</html>
```

And using `document.querySelectorAll()`

```js

document.querySelectorAll("a");

// would yield:
// [<a href="/home">Home</a>,<a href="/about">About</a>,<a href="/blog">Blog</a>]

```

### `document.querySelector()`

Using `document.querySelector(selector)` will only return a single element (the first matched element), even if there are more than one that matches your selector.

So, given some markup:

```html

<div>This is cool.</div>
<div>This is even cooler.</div>
<div>This is the coolest ever!</div>

```

Using `document.querySelector()`:

```js

document.querySelector("div");

// will only yield:
// <div>This is cool.</div>

```

## jQuery DOM traversal/manipulation

As we'll see over the coming week, jQuery will allow us to do things in the DOM with a much more compact api.  jQuery is a powerful and widely used library that allows developers around the world to easily work with the DOM.

For more practice, you can visit a quite a few resources and online tutorials, namely:

[Learn jQuery](http://learn.jquery.com)
[Try jQuery Online Course](http://try.jquery.com)

We covered quite a few methods in class today:

- `$(document).ready(function() {});`
- $(DOM Element) - our main way to grab a DOM element, then we can perform methods on it.

#### Traversing UP the DOM from $(selector)
  - .parent()
  - .parents()
  - .closest()

#### Traversing DOWN the DOM from $(selector)
  - .children()
  - .find()
  - .filter()

#### Traversing PEERs in the DOM from $selector
  - .siblings()
  - .next()
  - .prev()

[There are many more](http://api.jquery.com/category/traversing/tree-traversal/)

We also talked about:
  - .eq()
  - .text()
  - .html()
  - .append()
  - .prepend()
  - .click()

### Install bower package manager

[Bower](http://bower.io/)

In terminal:

`$ npm install -g bower`

Using the bower package manager, we can now install many available frontend javascript libraries into our projects.

###Underscore.js

If you like manipulating data, and you like javascript, then Underscore.js will become your best friend.  It gives you a huge library of helper functions that you can use in your own .js files.  First, `cd` into your folder of choice.  If you have bower installed,

`bower install underscore`

This should install the underscore package into your current directory. If you look at the documentation on [Underscore.js](underscorejs.org), it has a plethora of new functions for you to peruse.  Let's take a look at one of my favorites. `_.contains(array, value)`  This function checks to see if the array you given contains a certain value.  Sounds pretty simple, let's check it out!.

```js
var arrayOfArrays = [[1,2,3,'no'],[1,2,3,'yes'],[1,2,3,'no']]
var arrayOfArrays.filter(function(elm) {
  return _.contains(elm,'yes');
});
//returns [1,2,3,'yes']
```

This time, we have an array of arrays, similar to what you might see in a json object.  So the `elm` is referring to an array, not the items in the arrays.  I want to look only return arrays that have the value 'yes' inside the array.  The first array does not have a 'yes', but the second one does, so filter returns that entire array.  Pretty awesome.  Imagine if you wanted to only look at posts on etsy that contain the word 'cashmere' (I don't know why you would), BUT NOW YOU CAN!

# Resources

[Underscore.js](underscorejs.org)
[jQuery Docs](http://api.jquery.com)
[MDN Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)

