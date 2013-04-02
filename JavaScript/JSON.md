# Resource JSON Style Guide

Promoting the "Resource Way" of writing JavaScript Object Notation.

## Table of Contents

1. [Formatting](#formatting)

### <a name='formatting'>Formatting</a>  
- Use snake_case when naming properties.

    ```javascript
    // bad
    {
    "yearsInOperation": 30,
    "NotableClients": [
        "Sherwin Williams",
        "HP",
        "Victoria Secret",
        "P&G"
    ],
    "founder": "Nancy Kramer",
    "total-associates": 300
    }
    
    // good
    {
    "years_in_operation": 30,
    "notable_clients": [
        "Sherwin Williams",
        "HP",
        "Victoria Secret",
        "P&G"
    ],
    "founder": "Nancy Kramer",
    "total_associates": 300
    }   
    ```

