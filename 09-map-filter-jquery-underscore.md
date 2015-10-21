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


##Resources

[.map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
[.filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

Until next time,

Dominathan


