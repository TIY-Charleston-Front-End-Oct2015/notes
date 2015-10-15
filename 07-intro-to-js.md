# Day 7 - Intro to Javascript

And so it begins :)  The day is here where we talk about javascript.

Today we covered:

- Datatypes
  - strings
  - numbers
  - booleans
  - objects
  - arrays
  - functions

## Datatypes

### Number

In javascript, there is only one type of number, which is double precision floating-point or binary floating point.

<blockquote>
According to the ECMAScript standard, there is only one number type: the double-precision 64-bit binary format IEEE 754 value (number between -(253 -1) and 253 -1). There is no specific type for integers. In addition to being able to represent floating-point numbers, the number type has three symbolic values: +Infinity, -Infinity, and NaN (not-a-number).
</blockquote> - [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)

### String

Strings in javascript are used for textual information and cannot be altered (immutable).

You can add multiple strings together to make a new string, as well as alter a string using  `substr()` method, but these operations only create a new string, not altering the original.

```js

// original string
"Hello, I am a string".substr(0,4);
// "Hello" which is a new string

"I like ".concat("to code.");
// "I like to code."

```

### Boolean

<blockquote>
Boolean represents a logical entity and can have two values: true, and false.
</blockquote> - [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)

### Array

[From the Cyberwizard Institute](https://github.com/cyberwizardinstitute/workshops/blob/master/javascript.markdown)

Arrays are ordered lists of values.
You can make an array with square brackets:

``` js
var arr = [ 3, 2, 5 ]
console.log(arr)
```
---
#### arrays: indexing

To get at individual elements, use square brackets and an
integer index starting from zero:

``` js
var arr = [ 1, 4, 9 ];
console.log('first:', arr[0]);
console.log('second:', arr[1]);
console.log('third:', arr[2]);
```

outputs:

```
first: 1
second: 4
third: 9
```
---
#### arrays: indexing with variables

You can use variables for indexing too, not just constant
integers:

``` js
var arr = [ 1, 4, 9 ];
var n = 2;
console.log(arr[n]);
```

prints:

```
9
```

Any expression inside the square brackets will work.

#### arrays: length

To get the length of an array, just use `.length`:

``` js
var arr = [ 1, 4, 9 ];
console.log(arr.length);
```

which is the same as:

``` js
console.log([ 1, 4, 9 ].length);
```
---
#### arrays: push

To add an item to the end of an array,
use `arr.push()`:

``` js
var arr = [ 8, 1 ];
arr.push(5);
console.log(arr);
```

prints:

```
[ 8, 1, 5 ]
```
---
`arr.push()` is an example of a builtin
method, a function you can call that has
been defined by the language itself.

Later we'll see how to inspect what
methods are available.

---
#### arrays: pop

You can also remove an element from the
end of an array with `arr.pop()`:

``` js
var xs = [ 10, 6, 3 ];
console.log('popped:', xs.pop());
console.log('now xs=', xs);
```

prints:

```
popped: 3
now xs= [ 10, 6 ]
```
---
#### arrays: shift

Remove an element from the beginning of an array with shift:

``` js
var xs = [ 1, 2, 3 ];
console.log('shifted:', xs.shift());
console.log('xs=', xs);
```
---
#### arrays: slice

Return a new array between a start index and an end index.
If you don't provide an end index, the array length is used.

``` js
var xs = [ 'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i' ];
console.log(xs.slice(2, 3));
console.log(xs.slice(2));
```

prints:

```
[ 'c', 'd', 'e' ]
[ 'c', 'd', 'e', 'f', 'g', 'h', 'i' ]
```
---

#### arrays: more!

To see everything you can do with arrays, visit:

http://mzl.la/14BlbiN


### Object

[From the Cyberwizard Institute](https://github.com/cyberwizardinstitute/workshops/blob/master/javascript.markdown)

Objects map keys to values.

Like how a phone book maps names to telephone numbers:

```
key                     value
----------------------|---------
Benjamin Franklin     | 123-4142
Alexander Graham Bell | 214-6821
Marie Curie           | 615-2904
```
---
#### objects

To create the same structure in javascript we could do:

``` js
var phonebook = {
  'Benjamin Franklin': '123-4142',
  'Alexander Graham Bell': '214-6821',
  'Marie Curie': '615-2904'
};
```
---
#### objects

If a key is only letters, numbers, underscores, and dollar
signs (but doesn't start with a number), you can leave off
the quotes:

``` js
var obj = {
  abc: 555,
  def: 123,
  x1: 1000,
  y1: 5000,
  $x: 4444,
  "x y z": 12 // otherwise you'll need to use quotes
}
```

This way of building objects is sometimes called
"object literal" syntax.

---
#### objects: pick out a single record

Once an object exists, you can reference an individual value
by its key using a `.` followed by the key name. Here we use
`obj.y` to get at the `y` key:

``` js
var obj = { x: 7, y: 8, z: 9 };
console.log(obj.y);
```

will print:

```
8
```
---
#### objects: create a new record

Reference a key with a `.` followed by a key then use an
equal sign to create a new value under that key:

``` js
var obj = { a: 3, b: 4 };
obj.c = 5;
console.log(obj);
```

prints:

```
{ a: 3, b: 4, c: 5 }
```
---
#### objects: update an existing record

The same `obj.c = 5` syntax works even if a key already
exists:

``` js
var obj = { x: 500, y: 200 };
obj.y = 300;
console.log(obj);
```

prints:

```
{ x: 500, y: 300 }
```
---
#### objects: assignment operators

All of the assignment operators work for object keys just
like for variables!

``` js
var obj = { x: 500, y: 200 };
obj.y += 1000;
obj.x *= 3;
console.log(obj);
```

prints:

```
{ x: 1500, y: 1200 }
```
---
#### objects: square brackets

Using the `.` operator to access keys is handy, but what
about special characters in keys?

We can use square brackets with a string to reference
keys with special characters:

```
var obj = { 'a b c': 123, 'x#y*z': 456 };
console.log(obj['a b c']);
```

prints:

```
123
```
---
# objects: square brackets

We can also use square brackets to reference dynamic keys.
For example, if we want to load a key from a variable:

``` js
var key = 'def';
var obj = {
  abc: 555,
  def: 333,
  xyz: 222
};
console.log(obj[key]);
```

prints:

```
333
```

Everything we can do with dot (updates, assignment
  operators, etc) works with square bracket notation.

  ---
  # objects: delete

  To delete items from an object, use the `delete` keyword:

  ``` js
  var obj = { a: 4, b: 5, d: 700, x: 6 };
  delete obj.d;
  console.log(obj);
  ```

  prints:

  ```
  { a: 4, b: 5, x: 6 }
  ```

  If you try to delete a key that doesn't exist, nothing
  happens.

  ---
  # Object.keys

  Use `Object.keys()` to get an array of all the keys that an
  object has:

  ``` js
  var obj = { x: 5, y: 6, abc: 3 };
  console.log(Object.keys(obj));
  ```

  prints:

  ```
  [ 'x', 'y', 'abc' ]
  ```

### Function

## Control Flow

### comparison operators

The comparison operators all return a boolean:

* `===` - strict equality
* `!==` - not strict equality
* `<` - less than
* `<=` - less than or equal to
* `>` - greater than
* `>=` - greater than or equal to

You might also see coercive equality operators:

* `==` - coercive equality
* `!=` - not coercive equality

but you should avoid these operators until
learning about type coercion.

### comparison operators: example

```
var x = 5;
console.log(x < 6);
console.log(x === 2);
console.log(x !== 5);
console.log(x >= 5);

// output:

// true
// false
// false
// true

```
### logical operators

* `&&` - AND
* `||` - OR
* `!` - NOT (the opposite truth value)

`!` is a "unary" operator like `++` and `--`
because it binds to a single value.

`&&` and `||` are "binary" operators
because they bind to two values:
one on the left and one on the right.
---
### logical operators: example

``` js
var x = true
var y = false
console.log(x && y) // false
console.log(x || y) // true
console.log(!(x || y)) // false
console.log(!y) // true

// outputs:

// false
// true
// false
// true
```
### comments

By the way, `//` is the comment operator.
Anything that follows `//` on a line is
ignored by the computer.

You can even have whole blocks of comments
by putting text between `/*` and `*/`:

``` js
// this is a comment
console.log('beep boop'); // wow
/*
and this is a comment that
spans multiple
lines
*/
```
---
### if

You can make a block of code execute when
a conditional expression is true using an
`if` statement.

The conditional expression is the expression
surrounded by parenethesis following the word
`if`:

``` js
var x = 5;
if (x < 10) {
  console.log('wow');
}

// this program will print:

// wow
```
---
but if we change the program to be:

``` js
var x = 11;
if (x < 10) {
  console.log('wow');
}
```

then it won't print anything since the
conditional expression evaluated to false:

#### else

You can put an `else` statement after an
`if` statement to tell the computer what
to do if the `if` conditional expression
wasn't true:

``` js
var x = 11;
if (x < 10) {
  console.log('wow');
}
else {
  console.log('cool');
}

// will print:
// cool
```

# else if

Use `else if` to chain together fall-through cases:

``` js
var x = 22;
if (x < 10) {
  console.log('wow');
}
else if (x === 22) {
  console.log('twotwo');
}
else {
  console.log('cool');
}
```

#### nesting conditionals

``` js
var x = 5;
if (x < 5) {
  console.log('lt');
}
else {
  var y = x * 333 + 22;
  if (y > 1000) {
    console.log('y > 1000!!!');
  }
  else {
    console.log('y otherwise...');
  }
}
```

#### indentation

Now is a good time to talk about indentation.

First, you'll need to pick an amount of indentation to use
for each level.

4 spaces, 2 spaces, and tabs are all common amounts of
indentation.

#### 4 spaces

```
if (true) {
  if (true) {
    if (true) {
      // ...
    }
  }
}
```
#### 2 spaces

```
if (true) {
  if (true) {
    if (true) {
      // ...
    }
  }
}
```
#### first rule of indentation

However you choose to indent, be consistent!

Your code will be much easier for others and yourself to
read.

Remember to line up closing braces at the same level as
opening statements!


## Loops/Iteration

### for loop

For loops are like while loops but provide a place for
initialization and an expression to advance the loop.

```
for (var i = 0; i < 4; i++) {
  console.log(i);
}
```

prints:

```
0
1
2
3
```
---
Or you can jump by tens starting from 50:

``` js
for (var i = 50; i < 100; i += 10) {
  console.log(i);
}
```

prints:

```
50
60
70
80
90
```
---
#### looping over an array

A very common use-case for `for` loops is to loop over each
element in an array:

``` js
var xs = [ 'a', 'b', 'c', 'd' ];
for (var i = 0; i < xs.length; i++) {
  console.log(xs[i]);
}
```

prints:

```
a
b
c
d
```
## Resources

(MDN - Data Structures)[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures]
