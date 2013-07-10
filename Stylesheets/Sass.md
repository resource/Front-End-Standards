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


### <a name='references'>References</a>
- [Sass Reference Docs](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html)
- [The Sass Way](http://thesassway.com/) 

