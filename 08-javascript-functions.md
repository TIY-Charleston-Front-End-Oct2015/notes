# Day 8 - Javascript Functions

Today we covered javascript functions in more detail:

- Function Declaration vs Function Expression
- Parameters
- For Loops
- Javascript Built-In Functions
  - forEach

## Function

In javascript, a function is something that simply execute a set of instructions.  It can have a name, some parameters (values you can pass to the function), a body (the instructions you give the function), and returns a value. For example:

```js
function whyHelloThere(name) {
  console.log('Why Hello There, ' + name + '!!');
}
```
In this function, whyHelloThere is the function name. We also pass it a value, in this case <name>.  Finally it has a body, that prints out "Why Hello There <name>!!" to the console. To call the function,

```js
whyHelloThere("Jim");
```

### Function Declaration vs Function Expression

Quickly, what's the different between

```js
whyHelloThere(name);
function whyHelloThere(name) {
  console.log('Why Hello There, ' + name + '!!');
}
```

And

```js
whyHelloThere(name);
var whyHelloThere = function(name) {
  console.log('Why Hello There, ' + name + '!!');
}
```

The answer is the first one will run, while the second one will throw an error.  This is something in javascript called 'Hoisting', where the function declaration gets placed at the top of its scope, so it can actually be called in a program body before it is 'declared'.  Function Expressions cannot do this. We will get more in depth with hoisting and scope in a future lecture.

A little more to add, the second example is an anonymous function.  Our variable points to it, so the interpreter will know what we are talking about, but the function itself is anonymous.

###Parameters

Parameters are values, or arguments, you can pass to a function. In the above example, the name you pass to the function is an argument.  The function can use that value inside it's body.  Pretty awesome! You can give multiple arguments to a function.

```js
function addMeUp(x,y,z) {
  return x + y + z;
}
addMeUp(1,2,3);
```

This will return 6, 1 + 2 + 3.  But what if we do not know how many arguments we are going to have?  In this case, we want to take the arguments object.
```js
function addMeIfYouCan() {
  var args = Array.prototype.slice.call(arguments);
  console.log(args);
  console.log(args.length);
}
addMeIfYouCan(1,2,3,4,5,6);
```

While this function won't add anything, it will print out to the console every single argument as an array as well as how many arguments you gave it. If you give it a different number of arguments, it will return that amount of arguments as an array.

###For Loops

For loops are integral part of javscript, and in programming in general.  Let's take a look.

```js
for(var i=0; i<10; i++) {
  console.log(i);
}
```
What's happening here? First, we tell javascript we are going to use a for loop.  The for loop takes 3 arguments. The first, the var i = 0, is the initializer.  We are declaring a variable inside the for loop. The second, i<10, is the conditional.  It checks if 'i' is less than 10, and if it is, it runs the for loop body, console.log(i).  The last is the iterator.  When you see i++, it means it is adding 1 to itself.  You can think of it as the same as:

```js
i = i + 1
```

Every time the function runs, it'll add 1 to itself.  So on the second run through, it checks if i < 10.  Well, 'i' now = 1, because we just incremented it with i++, so 'console.log(i)' happens again.  Increment, i++, then check.  It goes all the way up to i = 10, and then it does not execute because i < 10 returns false. So the output?

```js
0
1
2
3
4
5
6
7
8
9
```

### forEach().

The forEach loop is the most primitive of what are called Higher-Order functions.  It is a higher-order, because it takes another function as an argument.  You commonly see forEach like so:

```js
var arr = [0,1,2,3,4,5,6,7,8,9];

arr.forEach(function(element,index,array) {
  console.log(element);
})

Similar to the for-loop above, this loop will print out 0 through 9 to the console. This method however, is called on an array. The forEach loop takes a callback, which is just another function it is waiting on, and that function can have three arguments: the element, the index, and array.

The element is each item in the array.  On the first run-through, element === 0, then 1, 2..etc.  The index is the array-based location of the element.  In this case, it will be the exact same as the element, but if we changed the array to

```js
var arr = [5,6,7,8,9]
```
and called

```js
arr.forEach(function(element,index,array) {
  console.log(element);
  console.log(index);
});
```

console.log(index) will print 0,1,2,3,4...but console.log(element) will print 5,6,7,8,9.

The last of the three is the array that .forEach is being called on. In the above case, it will always be [5,6,7,8,9].  Awesome!

You will also see .forEach take an entire function instead of declaring it inside itself. For example

```js
function callbackReplacement(element,index,array){
  console.log(element);
  console.log(index);
}

arr.forEach(callbackReplacement)
```

This will operate the exact same as arr.forEach(function(element,index,array) {}) above.  Try them out!

Lastly, the element, index, array arguments... All of them are optional arguments.  You do not have to use them. You could write

```js
arr.forEach(function(element){
  console.log(element);
})
```

and it would work just fine.  However, if you only want to use the index, be careful.

```js
var arr = [5,6,7,8,9]
arr.forEach(function(index){
  console.log(index);
})
```

You might think this will print out 0,1,2,3,4... but it won't! Why not? because the order of the arguments that .forEach is expecting.  The first one is the element, so the example above is simply calling the element argument index, and it will print out 5,6,7,8,9. To use just the index, you can do something like

```js
arr.forEach(function(_,index) {
  console.log(index);
});
```

You need to set a place holder for the argument you are not using.  Otherwise, javascript will expect that you want to use the element.

That's all for today! We will get into more javascript functions tomorrow. Happy coding!!

#Resources

[MDN - Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions)
[Expression vs Declaration](https://javascriptweblog.wordpress.com/2010/07/06/function-declarations-vs-function-expressions/)
[For-Loops](http://webcheatsheet.com/javascript/loops.php)
[MDN - forEach](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)


