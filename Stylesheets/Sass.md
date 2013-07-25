# Sass

Promoting the "Resource Way" of writing awesome Sass. "Stay Sassy, Resource"

## Table of Contents

1. [Definitions](#definitions)
1. [Commenting](#Commenting)
1. [Imports and Partials](#Imports)
1. [Variables](#Variables)
1. [Interpolation](#Interpolation)
1. [Sass Script Functions](#Sass Script Functions)
1. [Mixin](#Mixin)
1. [Mixin Pitfalls](#Mixin Pitfalls)
1. [Extend](#Extend)
1. [Extend Pitfalls](#Extend Pitfalls)
1. [Placeholder selectors](#Placeholder selectors)
1. [Content Directive](#Content Directive)
1. [Functions](#Functions)
1. [If/Else](#If/Else)
1. [Each](#Each)
1. [For/While](#For/While)
1. [Formatting](#Formatting)
1. [Line Breaks](#Line Breaks)
1. [The Inception Rule](#Inception)
1. [References](#references)

### <a name='definitions'>Definitions</a>  
The semantics in this document build off of the [Css](https://github.com/LukeAskew/Front-End-Standards/blob/master/Stylesheets/CSS.md) standards for this project.

There are two styles of syntax: .sass and .scss. The .sass style is a "looser" style that omits brackets {} and semi-colons. This document outlines usage of the .scss style. For more on why .scss is our preferred style check out the following articles - [SASS-lang docs](http://SASS-lang.com/docs/yardoc/file.SASS_REFERENCE.html#syntax) [Sass vs Scss](http://thesassway.com/articles/SASS-vs-scss-which-syntax-is-better)

Any reference made to "SASS" moving forward is in respect to the .scss notation. This is because saying "Sass" out loud is easier than "Scss", which just sounds like a snake hissing.


##### <a name='Commenting'>Commenting</a>
- // and /**/

```SCSS      

// Good
// This comment will not be output to the compiled Css file.

// Good
/**
 * Multiple Lines. And will be output
 * to the Css file
 */

```


##### <a name='Imports'>Imports and Partials</a>
- Keep @import rules at the top of your file. This makes it easier to find what is included.
- @import partials as you need for styling resuable components.
- More on @imports here [SASS Lang #directives](http://SASS-lang.com/docs/yardoc/file.SASS_REFERENCE.html#directives)

```SCSS
// Bad
@import "base.scss";

// Good
@import "base";
```

- Adding an underscore at the beginning of a filename creates a partial. Partials can then be imported.

Example file name:
_buttons.scss

```SCSS
@import "buttons";
@import "base";
```


##### <a name='Variables'>Variables</a>
- Name you variables in a modular way. Use dashes to separate multiple words in a declaration.

```SCSS
// Bad
$blue;
$dark-blue;
$darkest-blue;
$light-blue;

// Instead, group variables that share relationships and commonalities.
// Good
$blue;
$blue-dark;
$blue-darkest;
$blue-light;
```


##### <a name='Interpolation'>Interpolation</a>
- Use the Ruby-esque #{} to "shim" variables into your rules.

```SCSS
@mixin highlight($color, $side) {
	border-#{$side}-color: $color;
}

.btn-a {
	@include highlight(#f00, right);
}

// Css output
.btn-a {
	border-right-color: #ff0;
}
```


##### <a name='Sass Script Functions'>Sass Script Functions</a>
- Use of Sass Script Functions (functions native to SASS) is a great way to make your SASS more DRY. 

[SASS Script Functions Reference](http://SASS-lang.com/docs/yardoc/SASS/Script/Functions.html)

```SCSS
// Good
$blue = #054dc3;
$blue-light; = lighten($blue, 25%);

.blue {
	background-color: $blue;
}

.blue-light {
	background-color: $blue-light;
}
```


##### <a name='Mixin'>Mixin<a/>
- @mixin's allow you to define styles that can be re-used throughout the stylesheet. 
- Be sure your Mixin block comes before the @include statement. 
- Use camelCase to define them. 
- Comment code that may be unfamiliar to other developers.

```SCSS
// Good
$blue = #054dc3;

// lightens an object. uses SASS Script core function
// @params - a color and the percentage
@mixin lightenIt($color, $p) {
	background-color: lighten($color, $p);	
	color: ligten($color, $p);
}

.callout-light {
	@include lightenIt($blue, 25%);
}
```

##### <a name='Mixin Pitfalls'>Mixin Pitfalls</a>
- Be careful when calling a Mixin with multiple arguments.

```SCSS
// Bad
@mixin button($radius, $color) {
	border-radius: $radius;
	color: $color;
}

.btn-a {
	@include button(4px);	// Syntax error: Mixin button is missing argument $color
}
```

- Define a value for optional arguments to avoid errors.

```SCSS
// Good. Optional $color param is defined here as black.
@mixin button($radius, $color: #000) {
	border-radius: $radius;
	color: $color;
}

.btn-a {
	@include button(4px);	
}

// Css output
.btn-a {
	border-radius: 4px;
	color: #000;
}
```
- Avoid unecessary duplication with @mixin

```SCSS
// Bad
@mixin button {
	background: #777;
	border: 1px solid #ccc;
	font-size: 1em;
	text-transform: uppercase;
}

.foo {
	@include button;
}
 
.bar {
	@include button;
	color: #000;
}

// Css output
// Bad. Unecessary duplication.
.foo {
	background: #777;
	border: 1px solid #ccc;
	font-size: 1em;
	text-transform: uppercase;
}

.bar {
	background: #777;
	color: #000;
	border: 1px solid #ccc;
	font-size: 1em;
	text-transform: uppercase;
}
```


##### <a name='Extend'>Extend</a>
- Avoid duplication by using the @extend directive for lumping shared styles together. 
- @extend adds the properties of an existing class to where you're extending.

```SCSS
// Good
.btn-a {
	background: #777;
	border: 1px solid #ccc;
	font-size: 1em;
	text-transform: uppercase;
}

.btn-b {
	@extend .btn-a;
	background: #ff0;
}

// Css output
// Sass will track and automatically combine selectors for us.
.btn-a,
.btn-b {
	background: #777;
	border: 1px solid #ccc;
	font-size: 1em;
	text-transform: uppercase;
}

.btn-b {
	background: #ff0;
}
```


##### <a name='Extend Pitfalls'>Extend Pitfalls</a>
- Since .btn-b extends .btn-a, every instance that modifies .btn-a also modifies .btn-b. This creates stylesheet bloat, if these styles aren't needed.

```SCSS
.btn-a {
	background: #777;
	border: 1px solid #ccc;
	font-size: 1em;
	text-transform: uppercase;
}

.btn-b {
	@extend .btn-a;
	background: #ff0;
}

.sidebar .btn-a {
	text-transform: lowercase;
}

// Compiled Css below:
.btn-a,
.btn-b {
	background: #777;
	border: 1px solid #ccc;
	font-size: 1em;
	text-transform: uppercase;
}

.btn-b {
	background: #ff0;
}

// Bad. .btn-b is also scoped here
.sidebar .btn-a,
.sidebar .btn-b {
	text-transform: lowercase;
}
```


##### <a name='Placeholder selectors'>Placeholder selectors</a>
- Counteract stylesheet bloat with %placeholder selectors.
- Extend common blocks to avoid extra Html classes

```SCSS
// Good
%btn {
	background: #777;
	border: 1px solid #ccc;
	font-size: 1em;
	text-transform: uppercase;
}

.btn-a {
	@extend %btn;
}

.btn-b {
	@extend %btn;
	background: #ff0;
}

.sidebar .btn-a {
	text-transform: lowercase;
}

// Css output
.btn-a,
.btn-b {
	background: #777;
	border: 1px solid #ccc;
	font-size: 1em;
	text-transform: uppercase;
}

.btn-b {
	background: #ff0;
}

.sidebar .btn-a {
	text-transform: lowercase;
}
```


##### <a name='Content Directive'>Content directive</a>
- Use the @content directive to pass a block of styles to a mixin for placement within the styles included by the mixin.

```SCSS
// Good
@mixin media($type) {

	@if $type == tablet {
		@media all and (min-width: 768px) and (max-width: 991px) {
		  @content;
		}
	}

	@else if $type == mobile {
		@media all and (max-width: 767px) {
		  @content;
		}
	}

}

.content {
	width:960px;

	@include media(tablet) {
		width: 720px;
	}

	@include media(mobile) {
		width: 90%;
	}
}

// Css output
.content {
	width: 960px;

	@media all and (min-width: 768px) and (max-width: 991px) {
		width: 720px;
	}

	@media all and (max-width: 767px) {
		width: 90%;
	}
}
```


##### <a name='Functions'>Functions</a>
- Use functions when you need to calculate a value that may be reused somewhere else.
- Use camelCase for longer function names.

```SCSS
// Good
@function fluidize($target, $context) {
	@return ($target / $context) * 100%;
}

.sidebar {
	width: fluidize(350px, 1000px);
}

// Css output
.sidebar {
	width: 35%;
}
```


##### <a name='If/Else'>If/Else</a>
- Use @if and @else to conditionally output code.

```SCSS
// Good
$pink = #f09ccd;
$pink-light = #fbe6f3;
$pink-dark = #8b1459;

$theme: $pink;

header {
	@if $theme == $pink-dark {
		background: $pink-dark;
	} @else if $theme == $pink {
		background: $pink;
	} @else {
		background: $pink-light;
	}
} 

// Css output
header {
	background: #f09ccd;
}

```

- Example @if with @mixin

```SCSS
@mixin button($color, $rounded: false) {
	color: $color;

	@if $rounded {
		border-radius: $rounded;
	}
}

// $rounded false
.btn-a {
	@include button(#000);
}

// $rounded true
.btn-b {
	@include button(#333, 4px);
}

// Css output
.btn-a {
	color: #000;
}

.btn-b {
	color: #333;
	border-radius: 4px;
}
```


##### <a name='Each'>Each</a>
- Use the @each directive to loop through items in a list

```SCSS
// Good
$authors = kevin luke mark alex adam;

@each $author in $authors {
	.author-#{$author} {
		background-image: url(author-#{$author}.jpg);
	}
}

// Css output
.author-kevin {
	background-image: url(author-kevin.jpg);
}

.author-luke {
	background-image: url(author-luke.jpg);
}

.author-mark {
	background-image: url(author-mark.jpg);
}

.author-alex {
	background-image: url(author-alex.jpg);
}

.author-adam {
	background-image: url(author-adam.jpg);
}
```


##### <a name='For/While'>For/While</a>
- Use the @for or @while directive to save yourself manual work of repeating similar Css rules;

```SCSS
// @for example
// Good
$columns: 4;

@for $i from 1 through $columns {
	.cols-#{$i} {
    	width: ((100 / $columns) * $i) * 1%;
  	}
}

// Css output
.cols-1 {
	width: 25%;
}

.cols-2 {
	width: 50%;
}

.cols-3 {
	width: 75%;
}

.cols-4 {
	width: 100%;
}


// @while example
// Good
$i: 1;

.item {
	position: absolute;
	right: 0;

	@while $i < 4 {
		&.item-#{$i} {
			top: $i * 30px;
		}
		i$: $i + 1;	// @while requires manually updating the index
	}
}

// Css output
.item {
	position: absolute;
	right: 0;
}
.item.item-1 {
	top: 30px;
}
.item.item-2 {
	top: 60px;
}
.item.item-3 {
	top: 90px;
}
```


##### <a name='Formatting'>Formatting</a>
Keep indentation consistent to your project. If you're using 2 spaces, use 2 spaces. If you're using tabs, use tabs. End each object

```SCSS
// Bad
.foo {
	...
	.bar { 
		...
		.baz { ... } } }

// Good
.foo {
	...
	.bar { 
		...
		.baz { 
		    ...
		}
	}
}
```


##### <a name='Line Breaks'>Line Breaks</a>
Keep related modules/component declarations together. Adding a line break to each new declaration. One Css rule per line.

```SCSS
// Good 
.module {
  color: black;
  width: 100%;

  	.shrim {
  		color: green;
  		font-size: 16px;
  	}

  	.spaghett {
  		color: red;
  		font-size: 12px;
  	}
}

.next-module {
	color: white;
	width: 50%;

	.foo {
		color: black;
		text-align: left;
	}
}
```

```SCSS
// Bad
.module {
  color: black;
  width: 100%;
  	.shrim {
  		color: green;
  		font-size: 16px;
  	}
  	.spaghett {
  		color: red;
  		font-size: 12px;
  	}
}
.next-module {
	color: white;
	width: 50%;
	.foo {
	    color: black;
		text-align: left;
	}
}
```

##### <a name='Inception'>The "Inception Rule"</a>
Nesting too deep is getting away from a modular approach to writing Css. Thinking about context before writing your rules is a good start. See the [References](#references) section in this document for more on modular Css and avoiding deeply nested selectors.

**Four contextual examples to keep in mind to avoid over-nesting:**

**1) Site Context**
- Elements lacking a class or id. One level. e.g. h1-h6, body, ul, p

**2) Page Context**
- Styling the layout (elements that vary depending on the page). Usually two levels.

```SCSS
.cart {
    .sidebar { 
  	    width: 150px; 
    }
	.content { 
	    width: 850px; 
    }
}
```

**3) Objects**
- An element, alone or with children, identifed by class or id

```SCSS
.special-widget {
	li { 
		... 
	}

	a { 
		... 
	}
}
```

**4) Interaction State**
- Covers anything that changes when you interact with an object. This usually gets close to a fourth indentation, and is "ok". If you find yourself with lots of four-level-nested components consider revising and/or using the [@extend](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#extend) directive to get back to less than four levels.

```SCSS
.special-widget {
	background-color: blue;
	.super-special { 
		background-color: red;	
		a {
			border: 2px solid yellow;
			&:hover {
				text-decoration: underline;
			}
		}
	}
}
```

### <a name='references'>References</a>
- [Sass Reference Docs](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html)
- [The Sass Way](http://thesassway.com/)
- [Assembling Sass Course](http://www.codeschool.com/courses/assembling-sass)
- [Sass @extend Intro](http://awardwinningfjords.com/2010/07/27/sass-extend-introduction.html)
- [@extend your Sass](http://blog.kiskolabs.com/post/5445752361/extend-your-sass)
- [Handy Advanced Sass](http://12devs.co.uk/articles/handy-advanced-sass/)
- [Pure Sass Functions](http://thesassway.com/advanced/pure-sass-functions)
- [The Inception Rule](http://thesassway.com/beginner/the-inception-rule)
- [More Modular Css](http://thesassway.com/intermediate/avoid-nested-selectors-for-more-modular-css)
- [Modular Variables](http://webdesign.tutsplus.com/tutorials/htmlcss-tutorials/quick-tip-name-your-sass-variables-modularly/)
- [Unlease the power of @each](http://shoogledesigns.com/blog/blog/2012/10/01/unleash-the-power-of-each-within-sass/)
- [Sass Style Guide](http://css-tricks.com/sass-style-guide/)
- [Boost Sass/Compass Efficiency](http://www.netmagazine.com/tutorials/boost-sass-compass-efficiency)
- [Passing Content To Mixins](http://mikefowler.me/thoughts/passing-content-to-mixins-in-sass/)
- [Gist: passing content blocks to mixin](https://gist.github.com/chriseppstein/1215856)