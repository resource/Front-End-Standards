# Resource JSON Style Guide

Promoting the "Resource Way" of writing JavaScript Object Notation.

## Table of Contents

1. [Definitions](#definitions)    
1. [Formatting](#formatting)  
1. [Naming Conventions](#naming-conventions)  
1. [Structure](#structure)  
1. [Tools](#tools) 
1. [Well-formed JSON API Examples](#api-examples)  
1. [References](#references)  

***

All JSON should adhere to the standards defined on [JSON.org](http://json.org/). The purpose of this document is to provide guidelines for writing JSON at Resource. It assumes that all JSON conforms to the JSON.org standard, and that this document is used as a continuation of those standards.

### <a name='definitions'>Definitions</a>  
JSON, or JavaScript Object Notation, is a text-based open standard designed for human-readable data interchange. It is derived from the JavaScript scripting language for representing simple data structures and associative arrays, called objects. Despite its relationship to JavaScript, it is language-independent, with parsers available for many languages. [[source]](http://en.wikipedia.org/wiki/JSON)


* __property__: A name:value pair inside of a JSON object.
* __property name__: The name (key) portion of the property.
* __property value__: The value portion of the property.
* __collection__: A property value that is an array of objects with the same schema.

    ```javascript      
    // example
    {
    	"property_name": "property_value",
    	"collection": [
    		{
    			"name": "Kramer",
    			"company": "Resource"
    		},
    		{
    			"name": "Mooney",
    			"company": "Resource"
    		}
    	]
    }
    ```


### <a name='formatting'>Formatting</a>  
- Write underscore `_` delimited property names.

    ```javascript
    // bad
    {
    	"yearsInOperation": 30,
    	"NotableClients": [
        	"Sherwin Williams",
        	"HP",
        	"Victoria\u2019s Secret",
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
        	"Victoria\u2019s Secret",
        	"P&G"
    	],
    	"founder": "Nancy Kramer",
    	"total_associates": 300
    }   
    ```

### <a name='naming-conventions'>Naming Conventions</a>  
- Use meaningful, semantic names.

    ```javascript      
    // bad
    {
    	"years": 30,
    	"loc": ["Columbus", "Cincinatti", "San Francisco", "Chicago"]
    }
    
    // good
    {
    	"years_in_operation": 30,
    	"locations": ["Columbus", "Cincinatti", "San Francisco", "Chicago"]
    }
    ```
    
- Property values that are arrays should have plural names. Others should have singular names.
	- __Exemption__: Enumerable values can be either plural or singular

    ```javascript      
    // bad
    {
    	"room_total": 16,
    	"room_list": ["101", "102", "406"],
    	"building_numbers": "343"
    }
    
    // ok
    {
    	"total_rooms": 16
    }
    
    // good
    {	
    	"room_count": 16,
    	"rooms": ["101", "102", "406"],
    	"building_number": "343"
    }
    ```

- Avoid using [reserved JavaScript words](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Reserved_Words) as property names.

### <a name='structure'>Structure</a>  
- Use nested objects to provide structure.

	```javascript      
	// bad
	{
    	"company": "Resource",
    	"address": "343 Front St.",
    	"address2": "Floor 3",
    	"city": "Columbus"
    }
    
    // good
    {
    	"company": "Resource",
    	"address": {
    		"line1": "343 Front St.",
    		"line2": "Floor 3",
    		"city": "Columbus"
    	}
    }
    ```
    
- Resevere the "top-level" of your JSON object for meta data.
- Use a `data` object to store the primary content of your JSON object.
- Use semantic names for collections of like-data (e.g. `"employees"`).

	```javascript
	// example
	{
		"method": "GET",
		"id": "08819019273097",
		"data": {
			"item_count": 2,
			"items_per_page": 2
			"page": 1,
			"employees": [
				{
					"name": "Kramer",
					"company": "Resource"
				},
				{
					"name": "Mooney",
					"company": "Resource"
				}
			]
		}
	}	
	```
	
### <a name='tools'>Tools</a> 
- [JSONLint](http://jsonlint.com/)
- [JSONmate](http://jsonmate.com/) 

### <a name='api-examples'>Well-formed JSON API Examples</a> 
- [Soundcloud](http://developers.soundcloud.com/docs/api/reference)
- [Youtube](https://developers.google.com/youtube/2.0/reference)
- [Twitter](https://dev.twitter.com/docs/api/1.1)

### <a name='references'>References</a>
- [JSON.org](http://json.org/)
- [Google JSON Style Guide](http://google-styleguide.googlecode.com/svn/trunk/jsoncstyleguide.xml) 
