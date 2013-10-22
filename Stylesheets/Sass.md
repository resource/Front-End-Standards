# Sass Style Guide

The "[Resource](https://github.com/resource) Way" of writing Sassy CSS. 

## Table of Contents

1. [Preface](#preface)
1. [White Space & Formatting](#white-space-formatting)
1. [Imports and Partials](#imports)
1. [Variables](#variables)
1. [Interpolation](#interpolation)
1. [Pure Sass Functions](#pure-sass-functions)
1. [Mixins](#mixins)
1. [Productivity](#productivity)
1. [Nesting](#nesting)
1. [References](#references)

***

## <a name='preface'>Preface</a>  
This document is a continuation of the [CSS Style Guide](https://github.com/resource/Front-End-Standards/blob/master/Stylesheets/CSS.md). As a baseline, Sass stylesheets should adhere to the CSS style guide.

The examples in this style guide use the `.scss` syntax. This is the preferred syntax when writing Sass. Avoid using the `.sass` syntax.


## <a name='white-space-formatting'>White Space & Formatting</a>
Style declarations should conform to the [Resource CSS standard](https://github.com/resource/Front-End-Standards/blob/master/Stylesheets/CSS.md#declaration-blocks).

Mixins and Functions should conform to the [Resource JavaScript standard](https://github.com/resource/Front-End-Standards/blob/master/JavaScript/JavaScript.md#formatting) as much as possible.


## <a name='imports'>Imports and Partials</a>
Group `@import` rules at the top of the document.

Denote partials with a leading underscore.

Use dashes and lowercase characters when naming files.

Avoid using the  ".scss" extension in the `@import` declaration.

```SCSS
// bad
@import "objects/progressBars.scss";
@import "helpers/spacing.scss"

// good
@import "objects/_progress-bars";
@import "helpers/_spacing";
```


## <a name='variables'>Variables</a>
Name you variables in a [modular way](http://webdesign.tutsplus.com/tutorials/htmlcss-tutorials/quick-tip-name-your-sass-variables-modularly/) - providing structure and logic.

Add modifiers to the end of the variable name.

```SCSS
// bad
$sm: 35em;
$lg: 82em;

// bad
$small-breakpoint: 35em;
$large-breakpoint: 82em;

// good
$breakpoint-small: 35em;
$breakpoint-large: 82em;	
```


## <a name='interpolation'>Interpolation</a>
Use the Ruby-esque `#{}` to "shim" variables into your rules.

```SCSS
@mixin highlight($color, $side) {
	border-#{$side}-color: $color;
}

.selector {
	@include highlight(#f00, right);
}

// CSS output
.selector {
	border-right-color: #ff0;
}
```


## <a name='pure-sass-functions'>Pure Sass Functions</a>
Use [Pure Sass Functions](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html) to enhance code [clarity and usability](http://thesassway.com/advanced/pure-sass-functions).

```SCSS
// bad
$blue: #3d7fdf;
$blue-dark: #2165c8;
$blue-light: #699ce6;

// good
$blue: #3d7fdf;
$blue-dark: darken($blue, 10%);
$blue-light: lighten($blue, 10%);
```

Use them to make your life easier...

```SCSS
// good
.selector {
	background-color: $blue;
}

.selector-alt {
	background-color: complement($blue);
}
```

Prefer "pure Sass" functions over external dependencies like [Compass](http://compass-style.org/) or [Bourbon](http://bourbon.io).


## <a name='mixins'>Mixins</a>
Use dash-delimited mixin names. 

Thoroughly document mixin behavior and expected parameters

Group mixins together at the top of the document; better yet, separate mixins into their own partials.

```SCSS
// good

/**
 * position-absolutely()
 * Applies absolute positioning to an element using directional values passed-in as arguments.
 * Arguments must be defined in units (e.g. "px", "%"").
 * @param [top]
 * @param [right]
 * @param [bottom]
 * @param [left]
*/
@mixin position-absolutely ($top: auto, $right: auto, $bottom: auto, $left: auto) {
	top: $top;
	right: $right;
	bottom: $bottom;
	left: $left;
	position: absolute;
}

.selector {
	@include position-absolutely(10px, 10px, 5px, 15px);
}


```

Define a value for optional arguments to avoid errors.

```SCSS
// bad
@mixin button($radius, $color) {
	border-radius: $radius;
	color: $color;
}

.selector {
	@include button(3px); // error
}

// good.
@mixin button($radius, $color: #000) {
	border-radius: $radius;
	color: $color;
}

.selector {
	@include button(3px); // all good
}

```




## <a name='productivity'>Productivity</a>
Avoid repetitive rule declarations by leveraging `@each`, `@for`, and `@while`.

Use the `@each` directive to loop through items in a list.

```SCSS
// good
$authors: kevin luke mark alex adam;

@each $author in $authors {
	.author-#{$author} {
		background-image: url(author-#{$author}.jpg);
	}
}

// CSS output
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


Use the `@for` or `@while` directive to iterate values.

`@for`:

```SCSS
// good
$columns: 4;

@for $i from 1 through $columns {
	.column-#{$i} {
		width: ((100 / $columns) * $i) * 1%;
  	}
}

// CSS output
.column-1 {
	width: 25%;
}

.column-2 {
	width: 50%;
}

.column-3 {
	width: 75%;
}

.column-4 {
	width: 100%;
}
```

`@while`:

```SCSS
// good
$i: 1;

.item {
	position: absolute;
	right: 0;
	
}
@while $i < 4 {
	.item-#{$i} {
		top: $i * 30px;
	}
	$i: $i + 1;
}

// CSS output
.item {
	position: absolute;
	right: 0;
}

.item-1 {
	top: 30px;
}

.item-2 {
	top: 60px;
}

.item-3 {
	top: 90px;
}
```


## <a name='nesting'>Nesting</a>
Use tabs when nesting.

```SCSS
// bad
.foo {
  ...
••.bar { 
    ...
••••.baz { 
      ...
    }
  }
}

// good
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


No empty lines between nested declaration blocks.

```SCSS
// bad
.selector {
	color: $black;
	width: 100%;
  	
  	.selector-child {
  		color: $green;
  		font-size: 16px;
  	}
  	
  	.selector-child-alt {
  		color: $red;
  		font-size: 12px;
  	}
}

// good 
.selector {
	color: $black;
	width: 100%;
  	.selector-child {
  		color: $green;
  		font-size: 16px;
  	}
  	.selector-child-alt {
  		color: $red;
  		font-size: 12px;
  	}
}
```

Adhere to [The Inception Rule](http://thesassway.com/beginner/the-inception-rule) when nesting.

Exception: it is OK to deeply nest interaction states.

```SCSS
// ok
.level-one {
	background-color: $blue;
	.level-two { 
		background-color: $red;	
		.level-three {
			border: 2px solid #000;
			&:hover {
				text-decoration: overline;
			}
		}
	}
}
```

## <a name='references'>References</a>
- [Resource CSS Standards](https://github.com/resource/Front-End-Standards/blob/master/Stylesheets/CSS.md)
- [Resource JavaScript Standards](https://github.com/resource/Front-End-Standards/blob/master/JavaScript/JavaScript.md)
- [Name Your SASS Variables Modularly](http://webdesign.tutsplus.com/tutorials/htmlcss-tutorials/quick-tip-name-your-sass-variables-modularly/)
- [Module: Sass::Script::Functions](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html)
- [Using pure Sass functions to make reusable logic more useful](http://thesassway.com/advanced/pure-sass-functions)
- [Nested Selectors: The Inception Rule](http://thesassway.com/beginner/the-inception-rule)

### Resources
- [The Sass Way](http://thesassway.com/)
- [Assembling Sass Course](http://www.codeschool.com/courses/assembling-sass)
- [Sass @extend Intro](http://awardwinningfjords.com/2010/07/27/sass-extend-introduction.html)
- [SASS @imports](http://SASS-lang.com/docs/yardoc/file.SASS_REFERENCE.html#directives)
- [@extend your Sass](http://blog.kiskolabs.com/post/5445752361/extend-your-sass)
- [Handy Advanced Sass](http://12devs.co.uk/articles/handy-advanced-sass/)
- [More Modular Css](http://thesassway.com/intermediate/avoid-nested-selectors-for-more-modular-css)
- [Unlease the power of @each](http://shoogledesigns.com/blog/blog/2012/10/01/unleash-the-power-of-each-within-sass/)
- [Sass Style Guide](http://css-tricks.com/sass-style-guide/)
- [Boost Sass/Compass Efficiency](http://www.netmagazine.com/tutorials/boost-sass-compass-efficiency)
- [Passing Content To Mixins](http://mikefowler.me/thoughts/passing-content-to-mixins-in-sass/)
- [Gist: passing content blocks to mixin](https://gist.github.com/chriseppstein/1215856)