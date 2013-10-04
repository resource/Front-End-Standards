# Resource jQuery Style Guide

The "Resource Way" of writing performant and maintainable jQuery.

## Table of Contents
   
1. [Variable Naming](#variables)  
1. [Re-query](#re-query)  
1. [Sizzle](#sizzle)  


### <a name="variables">Variable Naming</a>
Prefix jQuery object variables with a `$`.

```javascript
// bad
var sidebar = $(".sidebar");

// good
var $sidebar = $(".sidebar");
```

### <a name="re-query">Re-query</a>
Cache jQuery lookups.

```javascript
// bad
var setSidebar = function() {
	$(".sidebar").hide();

	$(".sidebar").css({
		"background-color": "pink"
	});
}

// good
var setSidebar = function() {
	var $sidebar = $(".sidebar");
	
	$sidebar.hide();

	$sidebar.css({
		"background-color": "pink"
	});
}
```

### <a name="sizzle">Sizzle</a>

Use performant selectors. Sizzle reads [right-to-left](http://css-tricks.com/efficiently-rendering-css/) like native CSS, so much of the same rules apply.

```javascript
// bad
var $sidebar = $(".main > .column .sidebar");

// good
var $sidebar = $(".sidebar");
```

Use `find` with scoped jQuery object queries (rather than context).

```javascript
// bad
$("ul", ".sidebar").hide();

// bad
$(".sidebar ul").hide();

// good
$(".sidebar").find("ul").hide();
```
