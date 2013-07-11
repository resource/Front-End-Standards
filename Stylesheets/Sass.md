# Sass (Syntactically Awesome StyleSheets)

Promoting the "Resource Way" of writing awesome Sass. "Stay Sassy, Resource"

## Table of Contents

1. [Definitions](#definitions)
1. [Formatting](#formatting)
1. [References](#references)

### <a name='definitions'>Definitions</a>  
Sass is generally awesome and people that use it get free pancakes at IHOP.
There are two styles of syntax: .sass and .scss. The .sass style is a "looser" style that omits brackets {} and semi-colons. This document outlines usage of the .scss style. For more on why .scss is our preferred style check out the following articles - [sass-lang docs](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#syntax) [Sass vs Scss](http://thesassway.com/articles/sass-vs-scss-which-syntax-is-better)

Any reference made to "Sass" moving forward is in respect to the .scss notation. This is because saying "Sass" out loud is easier than "Scss", which just sounds like a snake hissing. Just want to make sure we're all on the same page :)

### <a name='formatting'>Formatting</a>
##### Commenting
- // and /**/

```SCSS      
// I'm a single-line comment that will not be output in the .css file. I am only visible in the .scss file

/* I'm a multi-line comment native to css that will be present
 * in both the .scss and output .css file
 */

```

##### Imports and Partials
- Keep @import rules at the top of your file. This makes it easier to find what is included.

```SCSS
// Ok (you don't need to include the extension)
@import "foo.scss";

// Better
@import "foo";
```

- Use an underscore at the beginning of a filename for partials you don't want to compile to css. You can then import these files without using the underscore.

```SCSS
@import "somepartial";
```

and _somepartial.scss would be imported.

More on @imports here [Sass Lang #directives](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#directives)

##### Variable Naming
Name you variables in a modular way.

```SCSS
// Too specific. Poor.
$blue;
$dark-blue;
$darkest-blue;
$light-blue;

// Instead, group variables that share relationships and commonalities.
// Get generic. Good.
$blue;
$blue-dark;
$blue-darkest;
$blue-light;
```

##### Indentation and Bracket location
Keep indentation consistent to your project. If you're using 2 spaces, use 2 spaces. If you're using tabs, use tabs. End each object

```SCSS
// Good. End each module where it starts
.foo {
	...
	.bar { 
		...
		.baz { ... }
	}
}

// Weird, bad bracket location
.foo {
	...
	.bar { 
		...
		.baz { ... } } }
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
  .sidebar { width: 150px; }
  .content { width: 850px; }
}
```

**3) Objects**
- An element, alone or with children, identifed by class or id

```SCSS
.special-widget {
	li { ... }
	a { ... }
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