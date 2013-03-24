JavaScript

## Blocks
- Blank line at the beginning and end of a block.
  - Exceptions: single line blocks, objects.
- Single space before the leading bracket.
  - Exceptions: functions that accept objects as an argument.


## <a name='functions'>Functions</a>
- Use function expressions rather than function declarations.  


    ```javascript
    // bad 
    function getData() {  
    } 

    // good
    var getData = function() {  
    };
    
    // better
    var getData = function getData() {  
    };
    ```

**References**  
["JavasScript Patterns" by shichuan](http://shichuan.github.com/javascript-patterns/)
    

    
    
