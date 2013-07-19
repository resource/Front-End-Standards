# Sass (Syntactically Awesome StyleSheets)

Promoting the "Resource Way" of writing awesome Sass. "Stay Sassy, Resource"

## Table of Contents

1. [Definitions](#definitions)
1. [Formatting](#formatting)
1. [References](#references)

### <a name='definitions'>Definitions</a>  
The semantics in this document build off of the [CSS](https://github.com/LukeAskew/Front-End-Standards/blob/master/Stylesheets/CSS.md) standards for this project.

There are two styles of syntax: .sass and .scss. The .sass style is a "looser" style that omits brackets {} and semi-colons. This document outlines usage of the .scss style. For more on why .scss is our preferred style check out the following articles - [sass-lang docs](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#syntax) [Sass vs Scss](http://thesassway.com/articles/sass-vs-scss-which-syntax-is-better)

Any reference made to "Sass" moving forward is in respect to the .scss notation. This is because saying "Sass" out loud is easier than "Scss", which just sounds like a snake hissing. Just want to make sure we're all on the same page :)


### <a name='formatting'>Formatting</a>
##### Commenting
- // and /**/

```SCSS      
// Single line comment. Will not be output to the compiled CSS file.

/**
 * Multiple
 * lines. And will be output
 * to the CSS file
 */

```


##### Imports and Partials
- Keep @import rules at the top of your file. This makes it easier to find what is included.

```SCSS
// Bad
@import "foo.scss";

// Good
@import "foo";
```

- Use an underscore at the beginning of a filename for partials you don't want to compile to css. You can then import these files without using the underscore.

Example file name:
_somepartial.scss

```SCSS
@import "somepartial";
```

More on @imports here [Sass Lang #directives](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#directives)


##### Variable Naming
Name you variables in a modular way. Use dashes to separate multiple words in a declaration.

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


##### Sass Script Functions
Use of Sass Script Functions (functions native to Sass) is a great way to make your Sass more DRY. 

[Sass Script Functions Reference](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html)

```SCSS
// Good
$blue = #054dc3;
$blue-light; = lighten($blue, 25%); // [Lighten instance method](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html#lighten-instance_method)

.blue {
	background-color: $blue;
}

.blue-light {
	background-color: $blue-light;
}
```


##### @extend
Use the @extend directive. 

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

// Compiled CSS below:
// Sass will track and automatically combine selectors for us:

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
Since .btn-b extends .btn-a, every instance that modifies .btn-a also modifies .btn-b. This creates stylesheet bloat, if these styles aren't needed

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

// Compiled CSS below:
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

##### Mixin
Use Mixins for resuse. Be sure your Mixin block comes before the @include statement. Use camelCase to define them. Comment code that may be unfamiliar to other developers.

```SCSS
// Good
$blue = #054dc3;

// lightens an object. uses Sass Script core function
// @params - a color and the percentage
@mixin lightenIt($color, $p) {
	background-color: lighten($color, $p);	
	color: ligten($color, $p);
}

.callout-light {
	@include lightenIt($blue, 25%);
}
```

Be careful when calling a Mixin with multiple arguments.

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
Keep related modules/component declarations together. Adding a line break to each new declaration. One CSS rule per line.

```SCSS
// Good 
.module {
  color: black;
  width: 100%;

  	.shrim {
  		color: green;
  		font-size: 16px;
  	}

  	.taargus {
  		color: blue;
  		font-size: 14px;
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
  	.taargus {
  		color: blue;
  		font-size: 14px;
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
Nesting too deep is getting away from a modular approach to writing css. Thinking about context before writing your rules is a good start. See the [References](#references) section in this document for more on modular CSS and avoiding deeply nested selectors.

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
- [The Inception Rule](http://thesassway.com/beginner/the-inception-rule)
- [More Modular CSS](http://thesassway.com/intermediate/avoid-nested-selectors-for-more-modular-css)
- [Modular Variables](http://webdesign.tutsplus.com/tutorials/htmlcss-tutorials/quick-tip-name-your-sass-variables-modularly/)
- [Sass Style Guide](http://css-tricks.com/sass-style-guide/)
- [Boost Sass/Compass Efficiency](http://www.netmagazine.com/tutorials/boost-sass-compass-efficiency)