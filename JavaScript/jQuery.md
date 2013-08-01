# Resource jQuery Style Guide and Best Practices [WORKING DRAFT]

Promoting the "Resource Way" of writing performant and maintainable jQuery.

## Table of Contents
   
1. [Variable Naming](#variables)  
1. [Re-query](#re-query)  
1. [Sizzle](#sizzle)  


### <a name='variables'>Variable Naming</a>
- Prefix jQuery object variables with a `$`.

    ```javascript
    // bad
    var sidebar = $('.sidebar');

    // good
    var $sidebar = $('.sidebar');
    ```

### <a name='re-query'>Re-query</a>
- Cache jQuery lookups.

    ```javascript
    // bad
    function setSidebar() {
      $('.sidebar').hide();

      // ...stuff...

      $('.sidebar').css({
        'background-color': 'pink'
      });
    }

    // good
    function setSidebar() {
      var $sidebar = $('.sidebar');
      $sidebar.hide();

      // ...stuff...

      $sidebar.css({
        'background-color': 'pink'
      });
    }
    ```

### <a name='sizzle'>Sizzle</a>
- Use performant selectors. Sizzle reads right-to-left like native CSS, so much of the same rules apply.

- Use `find` with scoped jQuery object queries (rather than context).

    ```javascript
    // bad
    $('ul', '.sidebar').hide();

    // bad
    $('.sidebar').find('ul').hide();

    // good
    $('.sidebar ul').hide();

    // good
    $('.sidebar > ul').hide();

    // good (slower)
    $sidebar.find('ul');

    // good (faster)
    $($sidebar[0]).find('ul');
    ```
