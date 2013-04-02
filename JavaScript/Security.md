# Resource Client-side Security Best Practices

Promoting the "Resource Way" of secure client-side websites and applications.

## Table of Contents

1. [DOM XSS](#dom-xss)

### <a name='dom-xss'>DOM XSS</a>  
- Cleanse user-inputted data before evaluating.

    ```javascript
    // bad
    var hash = window.location.hash;
    
    if ( hash ) {
        // ...XSS bro...
    };
    
    
    // good
    var hash = encodeURIComponent( window.location.hash );
    
    if ( hash ) {
        // ...some stuff...
    };
    ```

