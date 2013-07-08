# Resource JavaScript Style Guide

Promoting the "Resource Way" of writing semantic, reusable, and maintainable JavaScript.

## Table of Contents

### 1. [Formatting](#formatting)  
  1. [Comments](#comments)
  1. [Naming Conventions](#naming-conventions)  
  1. [Whitespace](#whitespace)   
  1. [Commas & Semicolons](#commas-and-semicolons)  
  1. [Blocks](#blocks)  

### 2. [Types](#types)
  1. [Primitive vs. Complex](#primitive-vs-complex)   
  1. [Strings](#strings)    
  1. [Booleans](#booleans)    
  1. [Arrays](#arrays)  
  1. [Objects](#objects)    
  1. [Functions](#functions)    

### 3. [Working With Types](#working-with-types)  
  1. [Variables](#variables)  
  1. [Constructors](#constructors)  
  1. [Properties](#properties)  
  1. [Casting & Coercion](#casting-and-coercion)  
  1. [Conditional Expressions & Equality](#conditionals)  
  1. [For Loops](#for-loops)  
  1. [Readable Milliseconds](#readable-milliseconds)  


### 5. [Structure](#structure)  
  1. [File Naming Conventions](#file-naming-conventions) 
  1. [Modules](#modules)  

### 6. [Appendix](#appendix)  
  1. [References](#references)
  1. [Performance](#performance) 
  1. [About Resource](#about-resource) 
  1. [License](#license) 

***

## <a name="formatting">Formatting</a>  
### <a name="comments">Comments</a>  

- Code should be thoroughly documented. The developer should strive to write logical and informative comments that contriburte to code maintainabiltiy and developer collaboration.

- Single-line comments should be written with two leading `//` followed by one space.
  - Use case goes here.

    ```javascript
    // single-line comment
    ```

- Comment blocks spanning multiple lines should be written using an opening `/**` and closing `*/`, with each line beginning with a single `*` surrounded by one leading and trailing space. 
  - Use case goes here.

    ```javascript
    /**
     * Multi-line comment 
     */
    ```
   

### <a name="naming-conventions">Naming Conventions</a>
  
- Avoid ambigious names. Be descriptive with your naming.

    ```javascript
    // bad
    function leanf() {
        // ...stuff...
    }
    
    // worse
    function lf() {
        // ...stuff...
    }

    // good
    function leanForward() {
        // ..stuff..
    }
    ```

- Use camelCase when naming objects, functions, and instances

    ```javascript
    // bad
    var OBJEcttsssss = {};
    var this_is_my_object = {};
    var this-is-my-object = {};
    function c() {};
    var u = new user({
        name: "Nancy Kramer"
    });

    // good
    var thisIsMyObject = {};
    function thisIsMyFunction() {};
    var user = new User({
        name: "Nancy Kramer"
    });
    ```

- Use PascalCase when naming constructors or classes

    ```javascript
    // bad
    function user(options) {
        this.name = options.name;
    }

    var bad = new user({
        name: "nope"
    });

    // good
    function User(options) {
        this.name = options.name;
    }

    var good = new User({
        name: "yup"
    });
    ```

- Use a leading underscore `_` when naming private properties.

    ```javascript
    // bad
    this.__firstName__ = "Nancy";
    this.firstName_ = "Nancy";

    // good
    this._firstName = "Nancy";
    ```

### <a name="whitespace">Whitespace</a>  

- Use liberal whitespace to enhance legibility.

- Use tabs set to 4 spaces.

    ```javascript
    // bad
    function() {
    ∙∙var name;
    }
    
    // good
    function() {
    ∙∙∙∙var name;
    }
    ```

- No end of line (trailing) whitespace.

    ```javascript
    // bad
    function() {
        var name;∙
    }
    
    // good
    function() {
        var name;
    }
    ```

- Use one space before leading parens and leading brackets.

    ```javascript
    // bad
    if(expression){
        // ...stuff...
    }
    
    // good
    if (expression) {
        // ...stuff...
    }
    
    // bad
    function(){
        // ...stuff...
    }
    
    // good
    function() {
        // ...stuff...
    }
    ```


- **Exceptions**:  
  - Function declarations and invocations.    

    ```javascript
    // ok
    var myFunction = function() {
        // ...stuff...
    }
    
    // ok
    myfunction();
    ```
    
  - Functions with callbacks.
    
    ```javascript
    // ok
    myfunction(function() {
        // ..stuff...
    });
    ```

  - Functions accepting arrays or objects.
    
    ```javascript
    // ok
    myfunction(["foo", "bar"]);    

    // ok
    myfunction({
        foo: "bar"
    });
    ```


### <a name="commas-and-semicolons">Commas & Semicolons</a> 
- Place commas end of line.

    ```javascript
    // bad
    var noodle
      , lounge
      , pod;

    // good
    var noodle,
        lounge,
        pod;

    // bad
    var associate = {
        firstName: "Nancy"
      , lastName: "Kramer"
      , role: "Founder"
      , superPower: "strength"
    };

    // good
    var associate = {
      firstName: "Nancy",
      lastName: "Kramer",
      role: "Founder",
      superPower: "strength"
    };
    ```
    
- Always use semicolons.

    ```javascript
    // bad
    (function() {
      var name = "Kramer"
      return name
    })()

    // good
    (function() {
      var name = "Kramer";
      return name;
    })();
    ```


### <a name="blocks">Blocks</a>  

- `if/else/for/while/try` always have braces and are always on multiple lines.

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

- Pad large blocks with blank lines.

    ```javascript
    // bad
    var createOpenBrand = function() {
        // ... lots of stuff...
    }
    
    // good
    var createOpenBrand = function() {

        // ... lots of stuff...
    
    }
    ```


## <a name="types">Types</a>  
### <a name="primitive-vs-complex">Primitive vs. Complex</a>

- **Primitives**: When you access a primitive type you work directly on its value.

    + `string`
    + `number`
    + `boolean`
    + `null`
    + `undefined`

    ```javascript
    var foo = 1,
        bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
    ```

- **Complex**: When you access a complex type you work on a reference to its value.

    + `object`
    + `array`
    + `function`

    ```javascript
    var foo = [1, 2],
        bar = foo;

    bar[0] = 9;

    console.log(foo[0], bar[0]); // => 9, 9
    ```


### <a name="strings">Strings</a>
- Use double quotes `""` for strings

    ```javascript
    // bad
    var name = 'Nancy Kramer';

    // good
    var name = "Nancy Kramer";

    // bad
    var fullName = 'Nancy ' + this.lastName;

    // good
    var fullName = "Nancy " + this.lastName;
    ```

- Strings longer than 80 characters should be written across multiple lines using string concatenation.
- Note: If overused, long strings with concatenation could impact performance. [jsPerf](http://jsperf.com/ya-string-concat) & [Discussion](https://github.com/airbnb/javascript/issues/40)

    ```javascript
    // bad
    var aboutResource = "There's nothing typical or ordinary about Resource. Even if you've previously worked at an agency, we think you'll find there's something singularly special about us, our offices and the way we do business.";

    // bad
    var aboutResource = "There's nothing typical \
    or ordinary about Resource. Even if you've \
    previously worked at an agency, we think you'll \
    find there's something singularly special about \
    us, our offices and the way we do business.";

    var aboutResource = "There's nothing typical" +
        "or ordinary about Resource. Even if you've" +
        "previously worked at an agency, we think you'll" +
        "find there's something singularly special about" +
        "us, our offices and the way we do business.";
    ```

- When programatically building up a string, use Array.join() instead of string concatenation. Mostly for IE: [jsPerf](http://jsperf.com/string-vs-array-concat/2).

    ```javascript
    var items,
        messages,
        length, i;

    messages = [{
        state: "success",
        message: "This one worked."
    }, {
        state: "success",
        message: "This one worked as well."
    }, {
        state: "error",
        message: "This one did not work."
    }];

    length = messages.length;


    // bad
    var inbox = function(messages) {
      
      items = "<ul>";

      for (i = 0; i < length; i++) {
        items += "<li>" + messages[i].message + "</li>";
      }

      return items + "</ul>";
      
    }

    // good
    var inbox = function(messages) {
      
      items = [];

      for (i = 0; i < length; i++) {
        items[i] = messages[i].message;
      }

      return "<ul><li>" + items.join("</li><li>") + "</li></ul>";
      
    }
    ```


### <a name="booleans">Booleans</a>

- Use “can”, “has” or “is” as a prefix when naming booleans.

    ```javascript
    // bad
    if (kramer.superPumped()) {
        return false;
    }
    
    // good
    if (kramer.isSuperPumped()) {
        return false;
    }
    
    // bad
    var shoe.tied = false;

    // good
    var shoe.isTied = false
    ```


### <a name="arrays">Arrays</a>
- Use the literal syntax for array creation

    ```javascript
    // bad
    var items = new Array();

    // good
    var items = [];
    ```

- If you don"t know array length use Array#push.

    ```javascript
    var someStack = [];


    // bad
    someStack[someStack.length] = "abracadabra";

    // good
    someStack.push("abracadabra");
    ```
    
### <a name="objects">Objects</a>

- Use the literal syntax for object creation.

    ```javascript
    // bad
    var item = new Object();

    // good
    var item = {};
    ```

- Don"t use [reserved words](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Reserved_Words) as keys.

    ```javascript
    // bad
    var resourceU = {
        class: "Raving Clients",
        default: { teacher: "Kramer" },
        private: true
    };

    // good
    var resourceU = {
        className: "Raving Clients",
        defaults: { teacher: "Kramer" },
        hidden: true
    };
    ```



### <a name="functions">Functions</a>

- Use function expressions rather than function declarations.

    ```javascript
    // bad 
    function funkDeclaration() {
        // ...stuff...
    };
    
    // good
    var funkExpression = function() {
        // ...stuff...
    };
    ```

- Properly written function expressions:

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

- Never declare a function in a non-function block (if, while, etc). Assign the function to a variable instead. Browsers will allow you to do it, but they all interpret it differently, which is bad news bears.
  - **Note:** ECMA-262 defines a `block` as a list of statements. A function declaration is not a statement. [Read ECMA-262"s note on this issue](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf#page=97).

    ```javascript
    // bad
    if (currentUser) {
        function test() {
            console.log("Nope.");
        }
    }

    // good
    if (currentUser) {
        var test = function() {
            console.log("Yup.");
        };
    }
    ```

- Never name a parameter `arguments`, this will take precedence over the `arguments` object that is given to every function scope.

    ```javascript
    // bad
    function nope(name, options, arguments) {
        // ...stuff...
    }

    // good
    function yup(name, options, args) {
        // ...stuff...
    }
    ```


## <a name="working-with-types">Working With Types</a>  
### <a name="variables">Variables</a>
- Use one `var` declaration for multiple variables.

    ```javascript
    // bad
    var foo = "foo";
    var bar = "bar";
    
    // good
    var foo = "foo",
        bar = "bar";
    ```
  
- **Exception**: It"s ok to use dedicated `var` declarations in order to enhance legibility, but ONLY when the code is going to be uglified eventually.
    
    ```javascript
    // ok

    /**
     * Data models
     */
    var storeModel = {
        foo: "bar"
    };

    var userModel = {
        foo: "bar"
    };
    ```

- Declare unassigned variables last. This is helpful when later on you might need to assign a variable depending on one of the previous assigned variables.

    ```javascript
    // bad
    var gpat,
        beerCart = true,
        noodle,
        locations = ["Columbus", "Cincinatti", "San Francisco", "Chicago"];
    
    // good
    var beerCart = true,
        locations = ["Columbus", "Cincinatti", "San Francisco", "Chicago"],
        gpat, noodle;
    ```

- Assign variables at the top of their scope. This helps avoid issues with variable declaration and assignment hoisting related issues. [More information about hoisting in JavaScript](http://www.kenneth-truyers.net/2013/04/20/javascript-hoisting-explained/)

- Create as few globals as possible.

    ```javascript
    // bad
    window.brownBagContent = "Knowledge Bombs";
    window.brownBagPresenter = "Super Cool Associte";
    
    // good
    var brownBag = {
        content: "Knowledge Bombs",
        presenter: "Super Cool Associate"
    };
    
    // bad (implied global "goodTime")
    var brownBag = function(content, presenter) {
        goodTime = content + presenter;
        return goodTime;
    };
    
    // good
    var brownBag = function(content, presenter) {
        var goodTime = content + presenter;
        return goodTime;
    };
    ```


### <a name="constructors">Constructors</a>

- Assign methods to the prototype object, instead of overwriting the prototype with a new object. Overwriting the prototype makes inheritance impossible: by resetting the prototype you"ll overwrite the base!

    ```javascript
    function Orbie() {
        console.log("new Orbie");
    }

    // bad
    Orbie.prototype = {
        feedTheCulture: function() {
            console.log("feeding the culture");
        },  
        leanForward: function() {
            console.log("leaning forward");
        }
    };

    // good
    Orbie.prototype.feedTheCulture = function() {
        console.log("feeding the culture");
    };

    Orbie.prototype.leanForward = function() {
        console.log("leaning forward");
    };
    ```

- Methods can return `this` to help with method chaining.

    ```javascript
    // bad
    Orbie.prototype.thinkBig = function() {
      this.thinkingBig = true;
      return true;
    };

    Jedi.prototype.takeRisks = function(risk) {
      this.risk = risk;
    };

    var pat = new Orbie();
    pat.thinkBig(); // => true
    pat.takeRisks("over-deliver") // => undefined

    // good
    Orbie.prototype.thinkBig = function() {
      this.thinkingBig = true;
      return this;
    };

    Orbie.prototype.takeRisks = function(risk) {
      this.risk = risk;
      return this;
    };

    var pat = new Orbie();

    pat.thinkBig()
      .takeRisks("over-deliver");
    ```



### <a name="properties">Properties</a>
- Use dot notation when accessing properties.

    ```javascript
    var pat = {
      orbie: true,
      age: 12
    };

    // bad
    var isOrbieWinner = pat["orbie"];

    // good
    var isOrbieWinner = pat.orbie;
    ```

- Use subscript notation `[]` when accessing properties with a variable.

    ```javascript
    var pat = {
        orbie: true,
        age: 12
    };

    function getProp(prop) {
      return pat[prop];
    }

    var isOrbieWinner = getProp("orbie");
    ```



### <a name="casting-and-coercion">Casting & Coercion</a>

- Perform type coercion at the beginning of the statement.

    ```javascript
    //  => this.reviewScore = 9;

    // bad
    var totalScore = this.reviewScore + "";

    // good
    var totalScore = "" + this.reviewScore;

    // bad
    var totalScore = "" + this.reviewScore + " total score";

    // good
    var totalScore = this.reviewScore + " total score";
    ```

- Use `parseInt` for Numbers and always with a radix for type casting.

    ```javascript
    // bad
    var newNumber = parseFloat("30");
    
    // bad
    var newNumber = parseInt("30");

    // good
    var newNumber = parseInt("30", 10);
    ```

  - **Exception**: Use `parseFloat` when converting to a floating point number.

    ```javascropt
    // ok
    var newNumer = parseFloat("30.4");
    ```

### <a name="conditionals">Operators, Conditional Expressions & Equality</a>
- **Objects** evaluate to **true**
- **Undefined** evaluates to **false**
- **Null** evaluates to **false**
- **Booleans** evaluate to **the value of the boolean**
- **Numbers** evalute to **false** if **+0, -0, or NaN**, otherwise **true**
- **Strings** evaluate to **false** if an empty string `""`, otherwise **true**  

  
- Use `===` and `!==` over `==` and `!=`.
  - **Exception**: `==` comparison is allowed when comparing to `null`, because it will detect both `null` or `undefined` properties.

    ```javascript
    var foo = null;

    // foo is null, but bar is undefined as it has not been declared
    if (foo == null && bar == null) {
        // ...stuff...
    }
    ```

- Use shortcuts.

    ```javascript
    // bad
    if (name !== "") {
      // ...stuff...
    }

    // good
    if (name) {
      // ...stuff...
    }

    // bad
    if (collection.length > 0) {
      // ...stuff...
    }

    // good
    if (collection.length) {
      // ...stuff...
    }
    ```
  - **Exception**: Avoid shortcut if checking for `0`.

    ```javascript
    // => value = 0;
    
    // bad 
    if (value) {
        // I"m in!
    }

    // good
    if (value !== 0) {
        // I"m NOT in!
    }
    ```

- Avoid comparing to `true` and `false`.

    ```javascript
    // bad
    if (isSuperPumped === true) {
        // ...party...
    }
    
    // good
    if (isSuperPumped) {
        // ...party...
    }
    
    // bad
    if (isSuperPumped === false) {
        // ...go home...
    }
    
    // good
    if (!isSuperPumped) {
        // ...go home...
    }
    ```

- Make your expressions more legible by keeping them brief.

    ```javascript
    // bad
    if ((buca || zPizza) && (udf || jenis)) {
      // ...party?
    }
    
    // good
    var pizza = buca || zPizza,
        iceCream = udf || jenis;
    
    if (pizza && iceCream) {
      // ...party!
    }
    ```

### <a name="for-loops">For Loops</a>  

- Cache loop length.
  - **Note**: It"s OK to declare a variable inside the initialization expression.

    ```javascript
    // yup
    var length = toLoop.length
    for (var i = 0; i < length; i++) {
        // GOOD - the length is only looked up once and then cached
    }
    ```


### <a name="readable-milliseconds">Readable Milliseconds</a>

- Use a multiplier of `1000` to produce more readble timers.

    ```javascript
    // bad
    var timeout = 30000; 
    
    // good
    var timeout = 30 * 1000; 
    ```

## <a name="structure">Structure</a>  
### <a name="file-naming-conventions">File Naming Conventions</a>
- Plugins/Modules should be prepended with the library/class they extend.

    ```javascript
    // bad
    myJqueryPlugin.js
    
    // good
    jquery.myJqueryPlugin.js
    ```
    
### <a name="modules">Modules</a>


## <a name="appendix">Appendix</a>  

### <a name="references">Resources</a>

- [Annotated ECMAScript 5.1](http://es5.github.com/)
- [AirBnb JavaScript Style Guide](https://github.com/airbnb/javascript)
- [jQuery Style Guide](http://contribute.jquery.org/style-guide/js/)
- [Idiomatic JS](https://github.com/rwldrn/idiomatic.js/)
- [JavaScript Patterns Collection](http://shichuan.github.com/javascript-patterns/)
- [Front End Development Guidelines](http://taitems.github.com/Front-End-Development-Guidelines/#javascriptSection)
- [Functions Explained](http://markdaggett.com/blog/2013/02/15/functions-explained/)
- [The Essentials of Writing High Quality JavaScript](http://net.tutsplus.com/tutorials/javascript-ajax/the-essentials-of-writing-high-quality-javascript/)

### <a name="performance">Performance</a> 
- [On Layout & Web Performance](http://kellegous.com/j/2013/01/26/layout-performance/)
- [String vs Array Concat](http://jsperf.com/string-vs-array-concat/2)
- [Try/Catch Cost In a Loop](http://jsperf.com/try-catch-in-loop-cost)
- [Bang Function](http://jsperf.com/bang-function)
- [jQuery Find vs Context, Selector](http://jsperf.com/jquery-find-vs-context-sel/13)
- [innerHTML vs textContent for script text](http://jsperf.com/innerhtml-vs-textcontent-for-script-text)
- [Long String Concatenation](http://jsperf.com/ya-string-concat)

### <a name="about-resource">About Resource</a>  
### <a name="license">License</a>  
