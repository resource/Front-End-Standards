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
    .selector?{
        ...
    }
    ```
 
- Use tabs set to 4 spaces/.
    
    ```css
    /* bad */
    .selector {
    ??float: left;
    }

    /* good */
    .selector {
    ????float: left;
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
        float?:?left;
    }

    /* good */
    .selector {
        float:?left;
    }
    ```
	
- Avoid nesting declaration blocks.

## <a name="selectors">Selectors</a>
### <a name="naming">Naming</a> 
- Selectors are always lowercase

    ```css
    /* bad */
    .Selector {
        ...
    }
    
    .SELECTOR {
        ...
    }

    .sElector {
        ...
    }

    /* good */
    .selector {
        ...
    }
    ```
    
- Selectors are dash-delimited.

    ```css
    /* bad */
    .main_selector {
        ...
    }
    
    /* good */
    .main-selector {
        ...
    }
    ```
    
    - Exception: underscores are OK when using BEM or any other modifier schema.
        
        ```css
        /* BEM delimits block, element, and modifiers with two underscores  */
        .menu__item menu__item_state_current {
            background-color: #fff;
        }
        ```

- Adhere to the design language of the brand when naming elements/selectors.

- Don't over-semantize class names; it reduces repurposability.
    
    ```css
    /* bad */
    .largeText {
        ...
    }

    .clearix {
        ...
    }

    .header-text-red {
        color: #f00;
    }
    
    /* good */
    .callout-text {
        ...
    }
    
    .group {
        ...
    }

    .header-text-alt {
        color: #f00;
    }
    ```

### <a name="specificity">Specificity</a> 
- Specificity is the means by which a browser decides which property values are the most relevant to an element and gets to be applied. Specificity is only based on the matching rules which are composed of selectors of different sorts.

#### Calculation ####
- Specificity is calculated based on the count of each selector type. The influence of each type, from weakest to strongest:
    1. Universal selectors
    2. Type selectors
    3. Class selectors
    4. Attributes selectors
    5. Pseudo-classes
    6. ID selectors
    7. Inline style

- In case of specificity equality, the latest declaration found in the CSS is applied to the element.

    ```css
    /* green */
    body h1 {
        color: #0f0;
    }

    /* purple */
    html h1 {
        color: #f0f;
    }

    /* h1 will render as purple */
    ```

#### The :not exception ####
- The negation pseudo-class :not _is not considered as a pseudo-class_ in the specificity calculation. However, selectors placed _inside of_ the negation pseudo-class count as normal selectors.

    ```css
    /* these two selectors have equal specificity so the last declaration takes precedence */
    
    div.outer p {
        color:orange;
    }

    div:not(.outer) p {
        color: lime;
    }
    ```
    
- Avoid use of `!important`.

- Avoid use of #IDs.

    ```css
    TODO
    ```
- Use preferred-child instead of decendent selectors.
    
    ```css
    /* bad */
    .selector p {
        ...
    }
    
    /* good */
    .selector > p {
        ...
    }
    ```

### <a name="efficiency">Efficiency</a>  
- Understand how CSS selectors are parsed.
    
    ```css
    TODO
    ```

- Avoid unessesary selectors; keep them as short as possible.
    - Adhere to the "Inception" rule.

    ```css
    TODO
    ```
    
- Avoid element selectors outside of normalization.

    ```css
    TODO
    ```

## <a name="value-formatting">Value Formatting</a>
- Use hex or rgba.
    - Use hex shortcut when possible. 
  
    ```css
    
    /* bad */
    .my-bad-header {
        color: blue; 
    }

    /* better */
    .my-better-header {
        color: #0000ff; 
    }

    /* good */
    .my-good-header {
        color: #00f; 
    }

    .my-good-header-alt {
        color: rgba(0, 0, 255, 1); 
    }

    ```

- Avoid named shortcuts.

    ```css
    TODO
    ```

- No quotes on `url()` values.

    ```css
    TODO
    ```
    

## <a name="typography">Typography</a> 
- Use pixels for `font-size`.

    ```css
    TODO
    ```
    
- Use unit-less values for `line-height`.

    ```css
    TODO
    ```
    
- Use the "bullet proof" method for `font-face` declarations.

    ```css
    TODO
    ```

## <a name="icons-imagery">Icons and Imagery</a>
- Icon font vs. base64 vs. sprite.
    - TODO chart

- How to create icon font.


## <a name="browser-compatibility">Browser Compatibility</a> 
- Use vendor prefixes for experimental (CSS3) features.

- Use fallbacks when available.

    ```css
    TODO
    ```

## <a name="accessibility">Accessibility</a>  
- Avoid low contrast color combinations.
    - Use [Contrast Ratio](http://leaverou.github.io/contrast-ratio/) to verify accessibilty.

- Avoid `display: none` when hiding content.

    ```css
    TODO
    ```
    
- Avoid `outline: none`.

## <a name="architecture">Architecture</a> 
- Use [normalize.css](https://github.com/necolas/normalize.css) to normalize styles.

- Leverage OOCSS principles.
    - Abstract commonly used styles into separate classes.
    - Follow the "Single Responsibility Principle".
    - Keep things DRY.

- Only use shorthand value declarations when the value will not be extended.

    ```css
    TODO
    ```
