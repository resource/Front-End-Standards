# Resource CSS Style Guide
Promoting the "Resource Way" for writing high-quality cascading style sheets.

## Table of Contents

1. [Comments](#comments)  
1. [Declaration Blocks](#declaration-blocks)  
1. [White Space](#white-space)  
1. [Selectors](#selectors)    
1. [Value Formatting](#value-formatting)  
1. [Typography](#typography)    
1. [Icons and Imagery](#icons-imagery)  
1. [Browser Compatibility](#browser-compatibility)  
1. [Accessibility](#accessibility)    
1. [Architecture](#architecture)  
1. [References](#references)


***

### <a name="comments">Comments</a>  
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

### <a name="declaration-blocks">Declaration Blocks</a>  
- Opening brackets should start on the same line; closing bracket on a new line.

   ```css
   .selector {
       ...
   }
   ```
   
- Separate multiple selectors with a new line.
    
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


### <a name="white-space">White Space</a> 
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
 
- Use tabs set to 4 spaces.
    
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

### <a name="selectors">Selectors</a>
#### <a name="naming">Naming</a> 
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
    - Adhere to the "[Inception](http://thesassway.com/beginner/the-inception-rule)" rule.

    ```css
    /* bad */
   .one.too .many .levels .here {
        ...
    }

    /* good */
   .too .levels {
        ...
    }
    ```
    
- Avoid element selectors outside of normalization.


### <a name="value-formatting">Value Formatting</a>
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
    
- Avoid using units when declaring `0` as a value.

    ```css
    /* bad */
    .no-margin-left {
        margin-left: 0px;
    }

    /* good */
    .no-margin-left {
        margin-left: 0;
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

- Reference: ["Definitive Guide to Web Fonts"](https://insider.resource.com/groups/technology-dlt/blog/2013/02/14/definitive-guide-to-webfonts)

## <a name="icons-imagery">Icons and Imagery</a>
- Icon font vs. base64 vs. sprite.
![Small Images and Iconography Decision Tree](http://www.gliffy.com/go/publish/image/4754342/L.png)

- Use Resource's [guide for creating icon fonts](https://insider.resource.com/docs/DOC-2265).


### <a name="browser-compatibility">Browser Compatibility</a> 
- Use vendor prefixes for experimental (CSS3) features.

- Use [fallbacks](http://flippinawesome.org/2013/07/08/using-css-fallback-properties-for-better-cross-browser-compatibility/) when available.

    ```css
    /* good */
    .future-stuff {
        color: #ccc;
        color: rgba(0, 0, 0, 0.5);
    }
    ```

### <a name="accessibility">Accessibility</a>  
- Avoid low contrast color combinations.
    - Use [Contrast Ratio](http://leaverou.github.io/contrast-ratio/) to verify accessibility.

- Avoid `display: none` when [hiding content](https://github.com/h5bp/html5-boilerplate/blob/master/css/main.css#L152).

    ```css
    /* bad */
    .content {
       display: none;
    }

    /* good */
    .content {
        border: 0;
        clip: rect(0 0 0 0);
        height: 1px;
        margin: -1px;
        overflow: hidden;
        padding: 0;
        position: absolute;
        width: 1px;
    }
    ```
    
- Avoid `outline: none`.

### <a name="architecture">Architecture</a> 
- Use [normalize.css](https://github.com/necolas/normalize.css) to normalize styles.

- Leverage OOCSS principles.
    - Abstract commonly used styles into separate classes.
    - Follow the "Single Responsibility Principle".
    - Keep things DRY.

- Only use shorthand value declarations when the value will not be extended.

- Separate [structure from skin](http://churchm.ag/object-oriented-css-separating-skin-from-structure/). Define repeating visual features as separate "skins"
   
    ```css
    /* bad */
    #button {
        width: 200px;
        height: 50px;
        padding: 10px;
        border: solid 1px #ccc;
        background: linear-gradient(#ccc, #222);
        box-shadow: rgba(0, 0, 0, .5) 2px 2px 5px;
    }

    #box {
        width: 400px;
        overflow: hidden;
        border: solid 1px #ccc;
        background: linear-gradient(#ccc, #222);
        box-shadow: rgba(0, 0, 0, .5) 2px 2px 5px;
    }

    /* good */
    .button {
        width: 200px;
        height: 50px;
    }

    .box {
        width: 400px;
        overflow: hidden;
    }

    .skin {
        border: solid 1px #ccc;
        background: linear-gradient(#ccc, #222);
        box-shadow: rgba(0, 0, 0, .5) 2px 2px 5px;
    }
    ```

### <a name="references">References</a> 
#### CSS Inception Rule ####
- <a href="http://thesassway.com/beginner/the-inception-rule">http://thesassway.com/beginner/the-inception-rule</a>

#### CSS Specificity Related Articles ####
- Use of ID's in CSS Selectors (And why to avoid it)
    - <a href="http://oli.jp/2011/ids/">http://oli.jp/2011/ids/</a>

#### Specificity Calculation ####
- <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity#How_is_it_calculated.3F">https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity#How_is_it_calculated.3F</a>
- <a href="http://coding.smashingmagazine.com/2007/07/27/css-specificity-things-you-should-know/">http://coding.smashingmagazine.com/2007/07/27/css-specificity-things-you-should-know/</a>
- <a href="http://iamacamera.org/default.aspx?id=95">http://iamacamera.org/default.aspx?id=95</a>
- <a href="http://www.stuffandnonsense.co.uk/archives/css_specificity_wars.html">http://www.stuffandnonsense.co.uk/archives/css_specificity_wars.html</a>

#### Efficiency ####
- <a href="http://css-tricks.com/efficiently-rendering-css/">http://css-tricks.com/efficiently-rendering-css/</a>

#### CSS Architecture ####
- BEM
    - <a href="http://bem.info/method/">http://bem.info/method/</a>
- OOCSS
    - <a href="http://coding.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/">http://coding.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/</a>
    - <a href="http://churchm.ag/object-oriented-css-separating-skin-from-structure/">http://churchm.ag/object-oriented-css-separating-skin-from-structure/</a>
- DRY CSS
    - <a href="http://www.vanseodesign.com/css/dry-principles/">http://www.vanseodesign.com/css/dry-principles/</a>
- Normalize.css
    - <a href="https://github.com/necolas/normalize.css">https://github.com/necolas/normalize.css</a>
- Separate structure from skin
    - <a href="http://churchm.ag/object-oriented-css-separating-skin-from-structure/">http://churchm.ag/object-oriented-css-separating-skin-from-structure/</a>

#### Typography ####
- <a href="http://meyerweb.com/eric/thoughts/2006/02/08/unitless-line-heights/">http://meyerweb.com/eric/thoughts/2006/02/08/unitless-line-heights/</a>
- <a href="https://github.com/stubbornella/csslint/wiki/Bulletproof-font-face">https://github.com/stubbornella/csslint/wiki/Bulletproof-font-face</a>
- <a href="https://insider.resource.com/groups/technology-dlt/blog/2013/02/14/definitive-guide-to-webfonts">https://insider.resource.com/groups/technology-dlt/blog/2013/02/14/definitive-guide-to-webfonts</a>

#### Icons and Imagery ####
- <a href="https://insider.resource.com/docs/DOC-2265">Resource's guide for creating icon fonts</a>

#### Browser Compatibility ####
- <a href="http://flippinawesome.org/2013/07/08/using-css-fallback-properties-for-better-cross-browser-compatibility/">CSS Fallback Properties for Better Cross-browser Compatibility</a>

#### Accessibility ####
- <a href="http://leaverou.github.io/contrast-ratio/">Verifying accessibility with contrast ratio</a>
- <a href="https://github.com/h5bp/html5-boilerplate/blob/master/css/main.css#L152">Avoid display: none when hiding content</a>