# Day 9 - Map, Filter and Reduce

We left off last time learning about javascript functions, for loops, and most fun of all, .forEach.  Today, we covered some more higher-order functions, namely -

- .map
- .filter

We also will take a look at Underscore.js, an awesome javascript library that provides a ton of other functions that make our lives as programmers all the better.

-------------------

We'll go over this in more detail, but first, what are Higher Order Functions?  Higher Order functions must do one of two things (or both):

1. Take a function as an input, or
2. Return a function as an output.

Higher Order function sounds like an esoteric concept, but really it's that simple.  When we looked at forEach, we saw that it always takes a callback as input, and we know that callbacks are functions.  So javascripts `.forEach(callback){ <body> }` is a Higher Order function because it takes a function as an argument.  As we'll see soon, .map, .filter, .reduce and most (if not all) of the underscore library are Higher Order Functions for that reason.  Also, all of the functions above are called on arrays.

### Map

Javascript's map is an amazing function for data manipulation, and is used in a host of other programming languages as well.  It operates likes this:

1. It takes the array it is called upon and loops over each element in that array
2. It looks at the first element
3. Performs whatever function you tell it to perform on that element
4. Adds that element to a new array
5. Looks the next element, performs 3. and 4., the next element, performs 3. and 4., until it is out of elements
6. And Returns a new array

That's Great!!  Let's walk through each of the pieces of `.map`

```js
var arr = [1,2,3,4,5];
arr.map(function(element,index,array) {
  return element * 2;
});
```

Let's walk through the steps to see what we think will come back.  It takes the arr, `[1,2,3,4,5]`, and looks at the first element, 1.  It performs the function body on our element, `1 * 2`, and adds it to a new array, `[2]`. It then looks at the next element in `[1,2,3,4,5]`, which is 2, performs the body of the function `element * 2`, and puts that in our new array, `[2,4]`.  It repeats this all the way up to 5, sees there are no more elements in the original array, and returns our new array [2,4,6,8,10].

Now for the callback function, the function inside of map.  It's just like .forEach from last time.  That function has access to

1. element
2. index
3. array

You can name them whatever you want though! I see `function(elm, idx, arr) { }` quite a bit, but you could just as easily do `function(app,mcDonalds,tesla) {} `.  Best of all, if you want to use only the element, you can just say `function(elm) { return elm * 2 }`.  Pretty neat.

You can also declare the "callback function" outside of .map.  For instance, the below would work the exact same as the above.
```js
var arr = [1,2,3,4,5];
function multiplyByTwo(elem) {
  return elm * 2;
}
arr.map(multiplyByTwo);
```

This is very useful when you want to reuse functions (or callbacks) and pass them around.  Also, like we talked about in the .forEach, be careful when you want only the index, or only the arr in `function(elm,idx,arr)`  You need to leave a _ to keep track of the item you aren't using.

```js
var arr = [1,2,3,4,5]
arr.map(function(_,idx) {
  //I only care about logging the index.
  console.log(idx);
});
```

###Filter

.filter is almost the same as .map, but instead of performing the function's body on the array, it checks to see if the body is true or false on the element.  If it's true, it'll add the element to a new array and go to the next element.  If it's false, it'll just go to the next element.  Let's take a look at this.

```js
var arr = [1,2,3,4,5];
arr.filter(function(elm,idx,arr){
  return elm % 2 === 0
});
```

Here, I'm checking if each element is even (i.e., if the remainder of the element divided by 2 is equal to 0).  It looks at 1, nope! Then 2, yep, [2]. 3, nope!. 4, yep! [2,4]. 5, nope!. Done. So what's returned? `[2,4]`.  That's it.

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

##Resources

[.map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
[.filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
[Underscore.js](underscorejs.org)
[jQuery Docs](http://api.jquery.com)
[MDN Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)

Until next time,

Dominathan


