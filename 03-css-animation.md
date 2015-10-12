# CSS Transitions and Keyframe animation

Our ability to create animations in CSS is relatively new still, but incredibly powerful and can provide enhancements to create a better user experience as well as for other reasons, like new shapes, pictures, and even games.

Today we focused more specifically on how to use the CSS transition property and the basics of using @-keyframes in css.

Today we covered:

- did some layout review
- git review
- CSS transition property
- @-keyframes animation property

### Note about vendor prefixes

Vendor prefixes are ways in which to write CSS property rules based on which browser's particular support.

The main vendor prefixes are:

- -webkit- Google Chrome and Safari
- -ms- Microsoft Internet Explorer
- -moz- Mozilla Foundation's Firefox

The use of the `transition:` property can be used without a vendor prefix, but when using `@keyframes`, you must use a vendor prefix at this time, eg. `@-webkit-keyframes`

## CSS Transitions

From the MDN Docs:
<blockquote>
CSS transitions let you decide which properties to animate (by listing them explicitly), when the animation will start (by setting a delay), how long the transition will last (by setting a duration), and how the transition will run (by defining a timing function, e.g. linearly or quick at the beginning, slow at the end).
</blockquote>

HTML
```html
<body>
<p>The box below combines transitions for: width, height, background-color, transform. Hover over the box to see these properties animated.</p>
<div class="box"></div>
</body>

```
CSS
```css
.box {
  border-style: solid;
  border-width: 1px;
  display: block;
  width: 100px;
  height: 100px;
  background-color: #0000FF;
  -webkit-transition:width 2s, height 2s, background-color 2s, -webkit-transform 2s;
  transition:width 2s, height 2s, background-color 2s, transform 2s;
}
.box:hover {
  background-color: #FFCCCC;
  width:200px;
  height:200px;
  -webkit-transform:rotate(180deg);
  transform:rotate(180deg);
}

```
In the case of our above example, we are animating (on a per property basis) width, height, and background color.

Setting up the transition property within our origin class ensures that all of these change definitions using transition are included in one place.

the format is also commonly written in shorthand:

`transition: <css property name> <animation duration> <timing function such as ease>`

## @keyframes animation

```css
@-webkit-keyframes backgroundColors {
  0% { background: #1ABC9C; }
  30% { background: #2ECC71 ; }
  60% { background: #3498DB ; }
  100% { background: #9B59B6 ; }
}

@keyframes backgroundColors {
  0% { background: #1ABC9C; }
  30% { background: #2ECC71 ; }
  60% { background: #3498DB ; }
  100% { background: #9B59B6 ; }
}

```

## Resources

[CSS Animation Tricks](http://css-tricks.com/css-animation-tricks/)

[Keyframe browser support](http://caniuse.com/#search=keyframes)

[CSS Transitions](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Using_CSS_transitions)

[MDN Docs for @keyframes](https://developer.mozilla.org/en-US/docs/Web/CSS/@keyframes)
