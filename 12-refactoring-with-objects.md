# Refactoring with Object Literals

Yesterday, we made our lives simpler by using underscore.js templates.  We were able to remove a lot of the duplication of copy and pasting HTML by using templates to loop through our data objects.  This, in essence, is what refactoring is all about...making things simpler and cleaner.

You may have noticed, though, that our [jQueryDemo](https://github.com/TIY-Charleston-Front-End-May2015/demos/blob/master/jqueryDemo/main.js) is starting to look like what is called **Spaghetti Code**.  What if something is broken, and you have to go hunt down where the bug is originating in this code? Or the project keeps growing, and gets even more unruly? Or you want to use some of this functionality on a different application you are working on?  All of these things are can be very difficult to do when you don't have structure to your code.  Enter (what's the queue music command?)

##Object Literal Pattern for Refactoring

The object literal pattern may sound complicated, but all it really means is grouping your code by behavior.  Let's begin with `var myPage = {}`. We have a simple object, myPage.  Whenever I am structuring a single object to interact with a page, I use the same generic template.

```js
Document.ready(function() {
  myPage.init()
})

var myPage = {
  //init will be called after the entire
  //document has loaded above.  init will
  //call be the point of entry.
  init: function() {

    //I'm telling the page
    //to call the styling
    //and events in here,
    // and call init when
    //the document is ready.
    myPage.initStyling();
    myPage.initEvents();
  },

  //styling will contain functions
  //that move content around the page.
  initStyling: function() {

  },

  //Events will house all events, e.g.,
  //('body').on('click', myPage.doSomething);
  initEvents: function() {

  },

  //Everything else that is an independent
  //function will be called by either initStyling,
  //or initEvents, and will be below.
  anotherFunction: function() {},
  maybeAnotherFunctionStill: function() {}
}
```
Doesn't that look a hell of a lot nicer? Yea, it may be a bit more code...(and we haven't even added the main functionality yet), but what it lacks in brevity it makes up for in the long-term maintainability.

Looking at our previous jQuery example (for reference...https://github.com/TIY-Charleston-Front-End-May2015/demos/tree/master/jqueryDemo), we have a list of things we need to happen for a user to have a good experience with our blog.

+ Compile a template that accepts data
+ Append the compiled template to the correct spot on the page with data
+ Grab values from the page to use as
+ Load the correct template.

Ok, let's tackle these one at a time.  It looks like add the very least, we'll want ad make the loadTemplate as a function, that takes a template, data, and a place to append the compiled template.

```js
  //...Everything from before.

  loadTemplate: function(tmplName, data, $target) {
    var compiledTmpl = _.template(templates[tmplName])
    $target.append(compiledTmpl(data));
  };
}
```

Looks pretty good, we take the compiledTmpl, feed it some data, and append it.  But now we need a way to grab the data from the page, and give it to the template.  Let's make another function to grab the data!

```js
//...Everything from before.

  getPostData: function() {
    var newPost = {
      title: $('input[name="title"]').val(),
      content: $('textarea').val(),
      author: $('input[name="author"]').val()
    };
  }
}
```

That looks pretty simple, it looks like the last thing we need to do is have a function that calls these two functions so we can add things to the DOM!

```js
//...Everything from before.

  addPostToDOM: function(post) {
    myPage.loadTemplate('post',post,$('.blog > .content'));
  };
}
```

Ok, so here we load our templates['post'], we take some random data we have not given it yet in `post`, and append it to the first child of `.blog` that is `.content`.  Let's put it all together.

```js
Document.ready(function() {
  myPage.init()
})

var myPage = {
  init: function() {

    myPage.initStyling();
    myPage.initEvents();
  },

  initStyling: function() {

  },

  initEvents: function() {

  },

  loadTemplate: function(tmplName, data, $target) {
    var compiledTmpl = _.template(templates[tmplName])
    $target.append(compiledTmpl(data));
  },

  getPostData: function() {
    var newPost = {
      title: $('input[name="title"]').val(),
      content: $('textarea').val(),
      author: $('input[name="author"]').val()
    };
  },

  addPostToDOM: function(post) {
    myPage.loadTemplate('post',post,$('.blog > .content'));
  };

}
```

Not half bad.  Our code looks like it has some great structure that we can maintain... we could even use these functions to compile templates and append to the DOM from somewhere else.  That's pretty awesome.  The problem is, we have no where at the moment in our javascript code that is listening for an event to actually add the post.  Let's do that

```js
  initEvents: function() {
    $('body').on('click', '.newBlogSubmit', myPage.addPostToDOM(myPage.getPostData));
  },
```

Now, when you refresh the browser, type in some content, and hit the submit button, our new post magically loads to the page.  Well, it's not magic, it's javascript! It's the same basic functionality we had before, but now the code looks way better.  Let's compare old version:

```js

var tmplString;

$(document).ready(function() {

var compiledTmpl = _.template(templates.post);
  tmplString = "";

posts.forEach(function(el) {
  console.log(compiledTmpl(el));
  tmplString += compiledTmpl(el);


});
$('.blog > .content').append(tmplString);
loadTemplate("about", {}, $('.about'));

$('.newBlogSubmit').on('click', function (event) {
  var newPost = {
    title: $('input[name="title"]').val(),
    content: $('textarea').val(),
    author: $('input[name="author"]').val()
  };
   loadTemplate("post", newPost, $('.blog > .content'));
  $('input, textarea').val("");
});

});

 function loadTemplate(name, data, $target) {
   var compiledTmpl = _.template(templates[name]);
   $target.append(compiledTmpl(data));
 }
```

to our new, smoother, structurally sound version:

```js
Document.ready(function() {
  myPage.init()
})

var myPage = {
  init: function() {

    myPage.initStyling();
    myPage.initEvents();
  },

  initStyling: function() {

  },

  initEvents: function() {
    $('body').on('click', '.newBlogSubmit', myPage.addPostToDOM(myPage.getPostData));
  },

  loadTemplate: function(tmplName, data, $target) {
    var compiledTmpl = _.template(templates[tmplName])
    $target.append(compiledTmpl(data));
  },

  getPostData: function() {
    var newPost = {
      title: $('input[name="title"]').val(),
      content: $('textarea').val(),
      author: $('input[name="author"]').val()
    };
  },

  addPostToDOM: function(post) {
    myPage.loadTemplate('post',post,$('.blog > .content'));
  };

}
```

Don't know about you, but if I were working on a codebase, and I saw the first version, I'd run for the hills.  The second is way better!

Pretty neat, huh? But what if we want have some posts load before you ever submit one... or even better if we want to grab the data from another url? We'll talk about that next time, with AJAX.

##Resources

+ [Using Objects to Refactor Your Code](http://rmurphey.com/blog/2009/10/15/using-objects-to-organize-your-code/)
+ [Working With Objects - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects)
