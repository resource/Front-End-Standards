# Resource CSS Style Guide
Promoting the "Resource Way" for writing high-quality cascading style sheets.

## Table of Contents

### 1. [Comments](#comments)  
### 2. [Declaration Blocks](#declaration-blocks)  
### 3. [White Space](#white-space)  
### 4. [Selectors](#selectors)    
### 5. [Value Formatting](#value-formatting)  
### 6. [Typography](#typography)    
### 7. [Icons and Imagery](#icons-imagery)  
### 8. [Browser Compatibility](#browser-compatibility)  
### 9. [Accessibility](#accessibility)    
### 10. [Architecture](#architecture)  

***

## <a name="comments">Comments</a>  
- Use comments to divide sections and describe larger sets of rules.
   - Don't overcomment, as most CSS should be self-explanitory; too much commenting detracts from readbility.

    ```css
    /* bad */
    .media {
        height: 100px; /* set height to 100px */
        width: 100px; /* set width the same as height */
        color: #ff0000; /* red */
    }
    
    
    /* good */
    /* media block */
    .media {
    	height: 100px;
    	width: 100px;
    	color: #ff000;
    }
    ```
    
    - Comment formatting:
    
    ```css
    /* ==========================================================================
       Section Comment
       ========================================================================== */
    ```
    
    ```css
    /**
     * Multiple
     * lines
     */
    ```
    
    ```css
    /* Single line */
    ```

## <a name="declaration-blocks">Declaration Blocks</a>  
- Opening brackets should start on the same line; closing bracket on a new line.

   ```css
   .selector {
       ...
   }
   ```
   
- Separte multiple selectors with a new line.
    
    ```css
    .selector,
    .another-selector {
       ...
    }
    ```

- One declaration per line.

    ```css
    /* bad */
    .selector {
        width: 100px; height: 100px;
        margin: 13px; padding: 42px;
    }
    
    /* bad */
    .selector { height: 100px }
    
    /* good */
    .selector {
        width: 100px; 
        height: 100px;
        margin: 13px; 
        padding: 42px;
    }
    ```
    
- Try to keep similar properties grouped together

    ```css
    /* not great */
    .selector {
        height: 100px;
        z-index: 2;
        width: 100px;
        position: relative;
    }
    
    /* good */
    .selector {
        height: 100px;
        width: 100px;
        position: relative;
        z-index: 2;
    }
    ```


## <a name="white-space">White Space</a> 
- One space between selector and opening bracket.
    
    ```css
    /* bad */
    .selector{
		...
    }

	/* good */
	.selector∙{
		...
	}
    ```
 
- Use tabs set to 4 spaces/.
    
	```css
	/* bad */
	.selector {
	∙∙float: left;
	}

	/* good */
	.selector {
	∙∙∙∙float: left;
	}
	```
	
- No space after property; one space before property value declaration.

	```css
	/* bad */
	.selector {
		float:left;
	}
	
	/* bad */
	.selector {
		float∙:∙left;
	}

	/* good */
	.selector {
		float:∙left;
	}
	```
	
- Avoid nesting declaration blocks.

## <a name="selectors">Selectors</a>
### <a name="naming">Naming</a> 
### <a name="specificity">Specificity</a> 
### <a name="efficiency">Efficiency</a>  

## <a name="value-formatting">Value Formatting</a>

## <a name="typography">Typography</a> 

## <a name="icons-imagery">Icons and Imagery</a> 

## <a name="browser-compatibility">Browser Compatibility</a> 

## <a name="accessibility">Accessibility</a>  

## <a name="architecture">Architecture</a> 
