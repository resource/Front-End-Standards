# Resource JavaScript Style Guide

The "[Resource](https://github.com/resource) Way" of writing good JavaScript.

## Table of Contents

### 1. [Formatting](#formatting)  
  1. [Comments](#comments)
  1. [Naming Conventions](#naming-conventions)  
  1. [Whitespace](#whitespace)   
  1. [Commas & Semicolons](#commas-and-semicolons)  
  1. [Blocks](#blocks)  

### 2. [Types](#types)
  1. [Strings](#strings)    
  1. [Booleans](#booleans)    
  1. [Arrays](#arrays)  
  1. [Objects](#objects)    
  1. [Functions](#functions)    

### 3. [Working With Types](#working-with-types)  
  1. [Variables](#variables)  
  1. [Constructors](#constructors)  
  1. [Properties](#properties)  
  1. [Conditional Expressions & Equality](#conditionals)  
  1. [For Loops](#for-loops)  
  1. [Readable Milliseconds](#readable-milliseconds)  


### 5. [Structure](#structure)  
  1. [File Naming Conventions](#file-naming-conventions) 

### 6. [Appendix](#appendix)  

***

## <a name="formatting">Formatting</a>  
### <a name="comments">Comments</a>  

Code should be thoroughly documented. The developer should strive to write logical and informative comments that contribute to code maintainability and developer collaboration.

Single-line comments should be written with two leading `//` followed by one space.

```javascript
// single-line comment
```

Comment blocks spanning multiple lines should be written using an opening `/**` and closing `*/`, with each line beginning with a single `*` surrounded by one leading and trailing space. 

```javascript
/**
 * Multi-line comment 
 */
```
   
### <a name="naming-conventions">Naming Conventions</a>
  
Avoid ambiguous names.

```javascript
// bad
var wSpecies;

// worse
var ws;

// good
var woodSpecies;
```

Use camelCase when naming objects, functions, and instances.

```javascript
// bad
var HardWoods = {};
var hard_woods = {};
var ChopDownTree = function() {};
var w = new wood({
    species: "Walnut"
});

// good
var hardWoods = {};
var chopDownTree = function() {};
var wood = new Wood({
    species: "Walnut"
});
```

Use PascalCase when naming constructors or classes.

```javascript
// bad
var wood = function(options) {
    this.species = options.species;
};

var aspen = new wood({
    species: "Aspen"
});

// good
var Wood = function(options) {
    this.species = options.species;
};

var aspen = new Wood({
    species: "Aspen"
});
```


### <a name="whitespace">Whitespace</a>  

Use liberal whitespace to enhance legibility.

Use tabs, not spaces.

```javascript
// bad
var plantTree = function() {
∙∙var name;
};

// good 
var plantTree = function() {
    var name;
};
```

No end of line (trailing) whitespace.

```javascript
// bad
var name;∙

// good
var name;
```

Pad concatenation points with one space when building strings.

```javascript
// bad
wood.description = "This is a "+color+" wood.";

// bad
wood.description = "This is a "+ color +" wood.";

// good
wood.description = "This is a " + color + " wood.";
```

Use one space before leading parens and leading brackets.

```javascript
// bad
if(expression){
    ...
}else{
    ...
}

// good
if (expression) {
    ...
} else {
    ...
}

// bad
for(var i = 0; i < length; i++){
    ...
}

// good
for (var i = 0; i < length; i++) {
    ...
}
```

**Exceptions**:

Function expressions and invocations.   

```javascript
// bad
var plantTree = function () {
    ...
};

// good
var plantTree = function() {
    ...
};

// good
plantTree();
```
    
Functions with callbacks.

```javascript
// ok
plantTree(function() {
    ...
});
```

Functions accepting arrays or objects.
    
```javascript
// ok
plantTrees(["Pine", "Walnut"]);    

// ok
plantTree({
    species: "Pine"
});
```

### <a name="commas-and-semicolons">Commas & Semicolons</a> 
Place commas end of line.

```javascript
// bad
var species
  , grain
  , hardness;

// good
var species,
    grain,
    hardness;

// bad
var wood = {
	species: "Walnut"
	, grain: "medium"
	, hardness: 1010
};

// good
var wood = {
	species: "Walnut",
	grain: "medium",
	hardness: 1010
};
```
    
Always use semicolons.

```javascript
// bad
(function() {
	var species = "Birch"
	return species
})()

// good
(function() {
	var species = "Birch";
	return species;
})();
```


### <a name="blocks">Blocks</a>  

`if/else/for/while/try` blocks always have braces and always span multiple lines.

```javascript
// bad
if (expression)
    return value;
    
// bad
if (expression) return value;

// good
if (expression) {
    return value;
}
```

Pad large blocks with blank lines.

```javascript
// bad
var plantTree = function() {
	// ...lots of stuff...
};

// good
var plantTree = function() {

    // ...lots of stuff...

};
```


## <a name="types">Types</a>  

### <a name="strings">Strings</a>
Use double quotes `""` for strings

```javascript
// bad
var species = 'Redwood';

// good
var species = "Redwood";
```

Long strings should be broken out onto multiple lines and concatenated properly.

```javascript
// bad
var description = "Walnut heartwood is a heavy, hard, open-grained hardwood. Freshly cut live wood may be Dijon-mustard colour, darkening to brown over a few days.";

// bad
var description = "Walnut heartwood is a heavy, hard, open-grained \
hardwood. Freshly cut live wood may be Dijon-mustard \
colour, darkening to brown over a few days.";

// good
var description = "Walnut heartwood is a heavy, hard, open-grained " +
    "hardwood. Freshly cut live wood may be Dijon-mustard " +
    "colour, darkening to brown over a few days.";
```

### <a name="booleans">Booleans</a>

Use _“can”_, _“has”_, _"should"_, or _“is”_ as a prefix when naming booleans.

```javascript
// bad
if (wood.hardEnough(value)) {
    ...
}

// good
if (wood.isHardEnough(value)) {
    ...
}

// bad
var wood.knots = true;

// good
var wood.hasKnots = true
```


### <a name="arrays">Arrays</a>
Use the literal syntax when creating arrays.

```javascript
// bad
var trees = new Array();

// good
var trees = [];
```
    
### <a name="objects">Objects</a>

Use the literal syntax when creating objects.

```javascript
// bad
var wood = new Object();

// good
var wood = {};
```

Don't use [reserved words](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Reserved_Words) as keys.

```javascript
// bad
var walnut = {
    class: "Magnoliophyta",
    default: { variety: "English" },
    private: true
};

// good
var walnut = {
    className: "Magnoliophyta",
    defaults: { variety: "English" },
    hidden: true
};
```

### <a name="functions">Functions</a>

Use function expressions rather than function declarations.

```javascript
// bad 
function funkDeclaration() {
    ...
};

// good
var funkExpression = function() {
    ...
};
```

Properly written function expressions: <sup>[[credit](https://github.com/airbnb/javascript#functions)]</sup>

```javascript
// anonymous function expression
var anonymous = function() {
    return true;
};

// named function expression for better traceability
var named = function named() {
    return true;
};

// immediately-invoked function expression (IIFE)
(function() {
    console.log("Welcome to the Internet. Please follow me.");
})();
```


## <a name="working-with-types">Working With Types</a>  
### <a name="variables">Variables</a>
Use one `var` declaration for multiple variables.

```javascript
// bad
var foo = "foo";
var bar = "bar";

// good
var foo = "foo",
    bar = "bar";
```
  
__Exception:__ Sometimes declaring variables individually - with comments - is helpful when documenting code. Do this only when you have an [uglification](https://github.com/mishoo/UglifyJS2) process in place since UglifyJS will remove comments and combine variable blocks.
    
```javascript
// ok

/**
 * Tree model
 * ...
 */
var treeModel = {
    ...
};

/**
 * Wood model
 * ...
 */
var woodModel = {
    ...
};
```

Declare unassigned variables last. 

```javascript
// bad
var quality,
    knots,
    wood = woods[0];

knots = wood.getKnots(); 

// good
var wood = woods[0],
    knots = wood.getKnots(),
    quality;
```


Create as few globals as possible.

```javascript
// bad
window.woodName = "Knotty Pine";
window.woodHardness = "soft";

// good
var wood = {
    name: "Knotty Pine",
    hardness: "soft"
};
```


Assign variables at the top of their scope to prevent [hoisting](http://www.kenneth-truyers.net/2013/04/20/javascript-hoisting-explained/).


### <a name="constructors">Constructors</a>

Avoid assigning an object to the prototype. Doing so may overwrite existing properties.

```javascript
var Tree = function() {
    ...
};

// bad
Tree.prototype = {
    grow: function() {
        ...
    },
    die: function() {
        ...
    }
};

// good
Tree.prototype.grow = function() {
    ...
};

Tree.prototype.die = function() {
    ...
};
```

### <a name="properties">Properties</a>
Use dot notation when accessing properties.

```javascript
var wood = {
    species: "Oak",
    hardness: 1300
};

// bad
var species = wood["species"];

// good
var species = wood.species;
```

Use subscript notation `[]` when accessing properties with a variable.

```javascript
var wood = {
    species: "Oak",
    hardness: 1300
};

var getProp = function(prop) {
  return wood[prop];
};

var specimenHardness = getProp("hardness");
```

### <a name="conditionals">Operators, Conditional Expressions & Equality</a>

Use `===` and `!==` when comparing values to ensure both _value_ and _type_ are compared.

```javascript
0 == false; // true
0 === false; // false

1 == "1"; // true
1 === "1" // false
```

Use comparison shortcuts.

```javascript
// bad
if (wood.species !== "") {
  ...
}

// good
if (wood.species) {
  ...
}

// bad
if (varieties.length > 0) {
  ...
}

// good
if (varieties.length) {
  ...
}
```

__Exception__: Avoid shortcuts if checking for `0`.

```javascript
var hardness = 0

// bad 
if (hardness) {
    ...
}

// good
if (hardness === 0) {
    ...
}
```

Avoid comparing to `true` and `false`.

```javascript
// bad
if (isSoft === true) {
    ...
}

// good
if (isSoft) {
    ...
}

// bad
if (isSoft === false) {
    ...
}

// good
if (!isSoft) {
    ...
}
```

Make your expressions more legible by keeping them brief.

```javascript
// bad
if ((walnut || hickory) && (spruce || pine)) {
	...
}

// good
var hardwood = walnut || spruce,
    softwood = spruce || pine;

if (hardwood && softwood) {
	...
}
```

When using ternary operators, wrap conditions in parens.

```javascript
// bad
var isSoft = wood.hardness < 800 ? true : false;

// good
var isSoft = (wood.hardness < 800) ? true : false;
```

### <a name="for-loops">For Loops</a>  

Cache loop length.

__Note__: It's OK to declare a variable inside the initialization expression.

```javascript
// good
var length = trees.length

for (var i = 0; i < length; i++) {
    ...
}
```


### <a name="readable-milliseconds">Readable Milliseconds</a>

Use a multiplier of `1000` to produce more readable timers.

```javascript
// bad
var timeout = 30000; 

// good
var timeout = 30 * 1000; 
```

## <a name="structure">Structure</a>  
### <a name="file-naming-conventions">File Naming Conventions</a>
Plugins/Modules should be prepended with the library/class they extend.

```javascript
// bad
myJqueryPlugin.js

// good
jquery.myJqueryPlugin.js
```
    

## <a name="appendix">Appendix</a>  

### References
- [Reserved Words](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Reserved_Words?redirectlocale=en-US&redirectslug=JavaScript%2FReference%2FReserved_Words)
- [AirBnb JavaScript Style Guide](https://github.com/airbnb/javascript)
- [Javascript hoisting explained](http://www.kenneth-truyers.net/2013/04/20/javascript-hoisting-explained/)


### Resources
- [Annotated ECMAScript 5.1](http://es5.github.com/)
- [jQuery Style Guide](http://contribute.jquery.org/style-guide/js/)
- [Idiomatic JS](https://github.com/rwldrn/idiomatic.js/)
- [JavaScript Patterns Collection](http://shichuan.github.com/javascript-patterns/)
- [Front End Development Guidelines](http://taitems.github.com/Front-End-Development-Guidelines/#javascriptSection)
- [Functions Explained](http://markdaggett.com/blog/2013/02/15/functions-explained/)
- [The Essentials of Writing High Quality JavaScript](http://net.tutsplus.com/tutorials/javascript-ajax/the-essentials-of-writing-high-quality-javascript/)

### Performance
- [On Layout & Web Performance](http://kellegous.com/j/2013/01/26/layout-performance/)
- [String vs Array Concat](http://jsperf.com/string-vs-array-concat/2)
- [Try/Catch Cost In a Loop](http://jsperf.com/try-catch-in-loop-cost)
- [Bang Function](http://jsperf.com/bang-function)
- [jQuery Find vs Context, Selector](http://jsperf.com/jquery-find-vs-context-sel/13)
- [innerHTML vs textContent for script text](http://jsperf.com/innerhtml-vs-textcontent-for-script-text)
- [Long String Concatenation](http://jsperf.com/ya-string-concat)
