# Resource jQuery Style Guide

The "[Resource](https://github.com/resource) Way" of writing performant and maintainable jQuery.

## Table of Contents
   
1. [Variable Naming](#variables)  
1. [Re-query](#re-query)  
1. [Sizzle](#sizzle)  

***

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
	
	$(".sidebar").addClass("hidden-visually");
	
	// ...stuff...

	$(".sidebar").removeClass("hidden-visually");

}

// good
var setSidebar = function() {
	
	var $sidebar = $(".sidebar");
	
	$sidebar.addClass("hidden-visually");
	
	// ...stuff...

	$sidebar.removeClass("hidden-visually");

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

Use `find` to select scoped jQuery object queries.

```javascript
// bad
var $sidebarList = $("ul", ".sidebar");

// bad
var $sidebarList = $(".sidebar ul");

// good
var $sidebarList = $(".sidebar").find("ul");
```
