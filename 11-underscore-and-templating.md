# Day 11 - Underscore and Templating

We left off yesterday going back in tothe realm of the index.html - This is dandy stuff, being able to move around the DOM seamlessly with jQuery, or even some native javascript.  We picked right back up where we left off, using Underscore.js templating to make our lives as coders even easier.  We covered:

- More jQuery
- Underscore's _.template

## What is Templating?

Let's say you have a ream of JSON data, e.g., you went to www.reddit.com/r/javascript.json which returns a huge chunk.  Or, even simpler, you have a list of restaurant objects and their rating on a 1-5 scale.

```json
var restaurants = [
  {
    name: "Five Loaves",
    rating: 5
  },
  {
    name: "The Kickin Chicken",
    rating: 2
  },
  {
    name: "Chik-Fil-A",
    rating: 4
  },
  {
    name: "Hominy Grill",
    rating: 3
  }
]
```
and an HTML page

```HTML
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Template Practice</title>
    <link rel="stylesheet" href="styles.css" media="screen" title="no title" charset="utf-8">
  </head>
  <body>
    <h1>Hey, here's the content!</h1>
    <div class="content">
      <ul class="restaurants">
      </ul>
    </div>
  </body>
</html>
```

What if we wanted to stick all those variables in the markup as a list item? We could a do direct transfer, something like...

```HTML
<ul>
  <li>Five Loaves<span>Rating: 5</span></li>
  <li>Chik-Fil-A<span>Rating: 4</span></li>
  <li>Kicken Chicken<span>Rating: 2</span></li>
  <li>Hominy Grill<span>Rating: 3</span></li>
</ul>
```
This is all fine and dandy if you want a static page, but what if the restaurants change?  What if you're pulling this from an external source, like YELP reviews, and you want it to update on the fly?

Enter Templating.

Client-side templating let's you merge data into your HTML without having to hardcode it (like I did above).  We can give our HTML a template to read, and underscore will convert any data we give it into HTML.  Let's look at an example.

```HTML
<li><%= name %><span>Rating: <%= rating %></span></li>
```

This should look similar to the list item above, but we've replaced the hard coded restaurants with the same attributes that are in our restaurants variable.  `<%= name %>` means Underscore.js will look for any properties called 'name', and feed it the value it finds.  We'll get to this more in a minute, but first, let's put this line in a template.

```HTML
<script type="text/template" id="myRestaurantTemplate">
  <li><%= name %><span>Rating: <%= rating %></span></li>
</script>
```

We've wrapped our HTML / Javascript Markup inside a script tag.  We've told the browser that the type is going to be a text/template, and we've given it an ID so we can use it later.  Let's finish by embedding this into your HTML `<head>`.

```HTML
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Template Practice</title>
    <link rel="stylesheet" href="styles.css" media="screen" title="no title" charset="utf-8">
    <script type="text/template" id="myRestaurantTemplate">
      <li><%= name %><span>Rating: <%= rating %></span></li>
    </script>
  </head>
  <body>
    <h1>Hey, here's the content!</h1>
    <div class="content">
      <ul class="restaurants">
      </ul>
    </div>
  </body>
  <script type="text/javascript"></script>
</html>
```

Alright, so we have our template inside our HTML...now what do we do?  Our goal is to loop over the resturants, all four of them, and using the template, inject the names and the ratings back onto the HTML page when it loads.

Let's start by just appending one.  If you take a look at [Underscore.js Templates](http://underscorejs.org/#template), you'll see it looks like `_.template(templateString, [settings])`.  It wants to take an argument as a template to compile it.  So! Let's create a variable and give it the text/template we made.

```HTML
<script type="text/javascript">
  var restaurantTemplate = _.template( $(myRestaurantTemplate).html() )
</script>
```
All we're doing here is taking the _.template function, and giving it, via jQuery, the template we defined in the header. Then we use .html() to get the raw HTML out of the template. If you console.log(restaurantTemplate), you'll see it just tells tells us we have `function template(data)`. That tells us we've made a variable that is pointing to a function, called template, that is expecting data.  We know we've already got our data in `var restaurants` from the tippy top of the page, so let's get the first restaurant, and then append it to the page.

```HTML
<script type="text/javascript">
  var restaurants = [
      {
        name: "Five Loaves",
        rating: 5
      },
      {
        name: "The Kickin Chicken",
        rating: 2
      },
      {
        name: "Chik-Fil-A",
        rating: 4
      },
      {
        name: "Hominy Grill",
        rating: 3
      }
    ]

  var restaurantTemplate = _.template( $(myRestaurantTemplate).html() );

  var mergedRestaurant = restaurantTemplate(restaurants[0]);
  console.log(mergedRestaurant);
  $('.restaurants').append(mergedRestaurant);
</script>
```

We took the restaurantTemplate, and we fed it the first object in our restaurants array.  The last line simply appends the result of that function to our `class="restaurants"` element.  If you refresh the page, you will see the Five Loaves Rating: 5 on the page.  Pretty cool.  Now, how do we add all of them at the same time.  More Underscore to the rescue! Let's loop over all the elements in var restaurants, add them to our templating function, and then append them to the page!
```HTML
<script type="text/javascript">
  var restaurants = [
      {
        name: "Five Loaves",
        rating: 5
      },
      {
        name: "The Kickin Chicken",
        rating: 2
      },
      {
        name: "Chik-Fil-A",
        rating: 4
      },
      {
        name: "Hominy Grill",
        rating: 3
      }
    ]

  var restaurantTemplate = _.template( $(myRestaurantTemplate).html() );

  _.each(restaurants, function(elm) {
    $('.restaurants').append( restaurantTemplate(elm) )
  });
</script>
```

That's it.  Now it will loop over each of our restaurants, then append the render `restaurantTemplate(elm)` to `$('.restaurants')`.  Awesome how that works. If we had an external call to Yelp, or to reddit, or to a database that people were inputting their own restaurants and ratings, we wouldn't have to update the HTML every time wtih the new restaurants.  Underscore will do that for us.  MAGIC!

Next time, we'll get into $.ajax to show how it'll magically update by itself.

Until next time,

Dominathan


FINAL

```HTML
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Template Practice</title>
    <link rel="stylesheet" href="styles.css" media="screen" title="no title" charset="utf-8">
    <script type="text/template" id="myRestaurantTemplate">
      <li><%= name %><span>Rating: <%= rating %></span></li>
    </script>
  </head>
  <body>
    <h1>Hey, here's the content!</h1>
    <div class="content">
      <ul class="restaurants">
      </ul>
    </div>
  </body>
  <script type="text/javascript">
    var restaurants = [
        {
          name: "Five Loaves",
          rating: 5
        },
        {
          name: "The Kickin Chicken",
          rating: 2
        },
        {
          name: "Chik-Fil-A",
          rating: 4
        },
        {
          name: "Hominy Grill",
          rating: 3
        }
      ]

    var restaurantTemplate = _.template( $(myRestaurantTemplate).html() );

    _.each(restaurants, function(elm) {
      $('.restaurants').append( restaurantTemplate(elm) )
    });
  </script>
</html>
```















