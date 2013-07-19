# Sass

Promoting the "Resource Way" of writing awesome Sass. "Stay Sassy, Resource"

## Table of Contents

1. [Definitions](#definitions)
1. [Formatting](#formatting)

1. [References](#references)

### <a name='definitions'>Definitions</a>  
The semantics in this document build off of the [Css](https://github.com/LukeAskew/Front-End-Standards/blob/master/Stylesheets/CSS.md) standards for this project.

There are two styles of syntax: .sass and .scss. The .sass style is a "looser" style that omits brackets {} and semi-colons. This document outlines usage of the .scss style. For more on why .scss is our preferred style check out the following articles - [SASS-lang docs](http://SASS-lang.com/docs/yardoc/file.SASS_REFERENCE.html#syntax) [Sass vs Scss](http://thesassway.com/articles/SASS-vs-scss-which-syntax-is-better)

Any reference made to "SASS" moving forward is in respect to the .scss notation. This is because saying "Sass" out loud is easier than "Scss", which just sounds like a snake hissing.


### <a name='formatting'>Formatting</a>
##### Commenting
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


##### Imports and Partials
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


##### Variables
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


#### Variable Interpolation
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

##### SASS Script Functions
- Use of SASS Script Functions (functions native to SASS) is a great way to make your SASS more DRY. 

[SASS Script Functions Reference](http://SASS-lang.com/docs/yardoc/SASS/Script/Functions.html)

```SCSS
// Good
$blue = #054dc3;
$blue-light; = lighten($blue, 25%); // [Lighten instance method](http://SASS-lang.com/docs/yardoc/SASS/Script/Functions.html#lighten-instance_method)

.blue {
	background-color: $blue;
}

.blue-light {
	background-color: $blue-light;
}
```


##### @mixin
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

#### @mixin Pitfalls
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
@mixin pinkBox {
	float: left;
	display: block;
	color: pink;
	width: 100px;
	height: 100px;
}

.foo {
	@include pinkBox;
}
 
.bar {
	@include pinkBox;
	font-size: 2em;
}

// Css output
// Bad. Unecessary duplication.
.foo {
	float: left; 
	display: block; 
	color: pink; 
	width: 100px; 
	height: 100px;
}

.bar {
	float: left; 
	display: block; 
	color: pink; 
	font-size: 2em;
	width: 100px; 
	height: 100px;
}
```


##### @extend
- Use the @extend directive for lumping shared styles together. 
- @extend adds the properties of an existing class to where you're extending. 
- Use @extend to avoid unecessary duplication.

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

#### @extend Pitfalls
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


##### Placeholder selectors
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

##### Functions
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

##### If/Else
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
@mixin button($color, $rounded: false {
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


##### Indentation and Bracket location
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


##### Line Breaks
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

##### The "Inception Rule"
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
- [Pure Sass Functions](http://thesassway.com/advanced/pure-sass-functions)
- [The Inception Rule](http://thesassway.com/beginner/the-inception-rule)
- [More Modular Css](http://thesassway.com/intermediate/avoid-nested-selectors-for-more-modular-css)
- [Modular Variables](http://webdesign.tutsplus.com/tutorials/htmlcss-tutorials/quick-tip-name-your-sass-variables-modularly/)
- [Sass Style Guide](http://css-tricks.com/sass-style-guide/)
- [Boost Sass/Compass Efficiency](http://www.netmagazine.com/tutorials/boost-sass-compass-efficiency)