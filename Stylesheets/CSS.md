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
    .selector•{
        ...
    }
    ```
 
- Use tabs set to 4 spaces/.
    
    ```css
    /* bad */
    .selector {
    ••float: left;
    }

    /* good */
    .selector {
    ••••float: left;
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
        float•:•left;
    }
    
    /* good */
    .selector {
        float:•left;
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

    .selectorName {
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

    .clearfix {
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
- Avoid using overly-specific selectors by understanding [specificity](http://coding.smashingmagazine.com/2007/07/27/css-specificity-things-you-should-know/) and [how it works](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity#How_is_it_calculated.3F).
    
- Avoid use of `!important`.

- Avoid use of #IDs.

    ```css
    /* bad */
    #my-selector {
        ...
    }    

    /* good */
    .my-selector {
        ...
    } 
    ```
- Use preferred-child instead of descendent selectors.
    
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
- Avoid inefficient selectors by [understanding](http://css-tricks.com/efficiently-rendering-css/) how selectors are parsed.
    
    ```css
    /* bad */
    html body ul li a {
        ...
    }

    /* good */
    .my-anchor {
        ...
    }
    ```

- Avoid unnecessary selectors; keep them as short as possible.
    - Adhere to the "Inception" rule.

    ```css
    /* bad */
   .one.too .many .levels {
        ...
    }

    /* good */
   .too .levels {
        ...
    }
    ```
    
- Avoid element selectors outside of normalization.


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
   /* bad */ 
   .my-font {
      font-weight: bold;
   }

    /* good */ 
   .my-font {
      font-weight: 700;
   }
    ```

- No quotes on `url()` values.

    ```css
    /* bad */
    .my-container {
      background-image: url('../img/frown.png');
   }

    /* good */
    .my-container {
      background-image: url(../img/rainbow.png);
   }
    ```
    

## <a name="typography">Typography</a> 
- Use `em` for `font-size`.

- Use [unit-less values](http://meyerweb.com/eric/thoughts/2006/02/08/unitless-line-heights/) for `line-height`.

    ```css
    /* bad */
    .my-paragraph {
        font-size: 1em;
        line-height: 1.3em;
    }
 
    /* good */
    .my-paragraph {
        font-size: 1em;
        line-height: 1.3;
    }
    ```
    
- Use the ["bullet proof"](https://github.com/stubbornella/csslint/wiki/Bulletproof-font-face) method for `font-face` declarations.

    ```css
    /* example */
    @font-face {
        font-family: "MyFontFamily";
        src: url(myfont-webfont.eot?#iefix) format("embedded-opentype"), 
            url(myfont-webfont.woff) format("woff"), 
            url(myfont-webfont.ttf)  format("truetype"),
            url(myfont-webfont.svg#svgFontName) format("svg");
    }
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
