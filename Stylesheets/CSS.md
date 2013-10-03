# CSS Style Guide
The "Resource Way" for writing legible, scalable, and useful CSS.

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

## <a name="comments">Comments</a>
Comments should be _useful_ and should provide _clarity_. Use comments to divide sets of rules into groups, or to explain potentially confusing rule declarations.


### Avoid Over Commenting
Don't over comment, as most CSS should be self-explanatory; too much commenting detracts from readability.

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

### Types of Comments

#### Multiple Line
```css
/**
 * Multiple
 * lines
 */
```

#### Single Line
```css
/* Single line */
```

## <a name="declaration-blocks">Declaration Blocks</a>

Opening brackets should start on the same line; closing bracket on a new line.

```css
/* bad */
.selector { ... }

/* bad */
.selector {
... }

/* good */
.selector {
   ...
}
```

Separate multiple selectors with a new line.

```css
/* bad */
.selector, .another-selector {
   ...
}

/* good */
.selector,
.another-selector {
   ...
}
```

Each rule declaration on it's own line.

```css
/* bad */
.selector {
    width: 100px; height: 100px;
    margin: 13px; padding: 42px;
}

/* bad */
.selector { height: 100px; }

/* good */
.selector {
    width: 100px;
    height: 100px;
    margin: 13px;
    padding: 42px;
}
```

Keep similar properties grouped together. Use **[CSSComb](http://csscomb.com/)** with the default settings.

```css
/* bad */
.selector {
    height: 100px;
    z-index: 2;
    width: 100px;
    position: relative;
}

/* bad */
.selector {
    height: 100px;
    position: relative;
    width: 100px;
    z-index: 2;
}

/* good */
.selector {
    height: 100px;
    width: 100px;
    position: relative;
    z-index: 2;
}
```

Separate declaration blocks with a blank line.

```css
/* bad */
.selector {
    ...
}
.selector {
    ...
}

/* good */
.selector {
    ...
}
↩
.selector {
    ...
}
```


## <a name="white-space">White Space</a>
Use one space between the selector and the opening bracket.

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

Use tabs set to 4 spaces.

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

Use one space between the property key and value declaration.

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

Avoid nesting declaration blocks.

```css
/* bad */
.selector {
    ...
}
    .selector-2 {
       ...
    }

/* good */
.selector {
    ...
}

.selector-2 {
   ...
}
```


## <a name="selectors">Selectors</a>

### <a name="naming">Naming</a>
Adhere to the [design language](http://logicpool.com/archives/235) of the brand when naming selectors.

Selectors never contain uppercase letters.

```css
/* bad */
.Selector {
    ...
}

/* bad */
.SELECTOR {
    ...
}

/* bad */
.selectorName {
    ...
}

/* good */
.selector {
    ...
}
```

Selectors are dash-delimited.

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

Exception: underscores are OK when using [BEM](http://bem.info/method/) or any other modifier schema.

```css
/* BEM - OK */
.block__element--modifier {
    background-color: #fff;
}
```

Avoid overly-semantic selector names.

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
Avoid using overly-specific selectors. Understand [specificity](http://coding.smashingmagazine.com/2007/07/27/css-specificity-things-you-should-know/) and [how it works](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity#How_is_it_calculated.3F). 

```css
/* bad */
div.media {
    ...
}

.media #video-1 {
    ...
}

/* good */
.media {
    ...
}

.video:first-child {
    ...
}

```


Use ID selectors sparingly.

```css
/* bad */
#walnut-promo {
    ...
}

#maple-promo {
    ...
}

#hickory-promo {
    ...
}

/* good */
.promo {
    ...
}

.promo-walnut {
    ...
}

.promo-maple {
    ...
}

.promo-hickory {
    ...
}
```

Use preferred-child instead of descendant selectors.

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
Avoid inefficient selectors by [understanding](http://css-tricks.com/efficiently-rendering-css/) how selectors are parsed.

```css
/* bad */
ul li a.menu-link {
    ...
}

/* good */
.menu-link {
    ...
}
```

Avoid unnecessary selectors; keep them as short as possible. Adhere to the "[Inception](http://thesassway.com/beginner/the-inception-rule)" rule.

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

Avoid element selectors (outside of [normalization](https://github.com/necolas/normalize.css)).

```css
/* bad */
div {
    background-color: #000;
}

/* good */
.selector {
    background-color: #000;
}
```

## <a name="value-formatting">Value Formatting</a>
Use hex or rgba. Use hex shortcuts when possible.

```css
/* bad */
.my-bad-header {
    color: blue;
}

/* ok */
.my-ok-header {
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

Use lowercase for hex values

```css
/* bad */
.selector {
    color: #CCC;
}

/* good */
.selector {
    color: #ccc;
}
```

Avoid named shortcuts.

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

Avoid using units when declaring `0` as a value.

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

Avoid quotes and absolute paths in `url()` values.

```css
/* bad */
.my-container {
  background-image: url("../img/frown.png");
}

/* bad */
.my-container {
  background-image: url(/img/frown.png);
}

/* good */
.my-container {
  background-image: url(../img/rainbow.png);
}
```


## <a name="typography">Typography</a>
Use `em` for `font-size`. [PXtoEM](http://pxtoem.com/) can help with the conversion. 

Use [unit-less values](http://meyerweb.com/eric/thoughts/2006/02/08/unitless-line-heights/) for `line-height`.

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

Use the ["bullet proof"](https://github.com/stubbornella/csslint/wiki/Bulletproof-font-face) method for `font-face` declarations.

```css
/* example */
@font-face {
    font-family: "My-Font-Family";
    src: url(../fonts/custom-webfont.eot);
    src: url(../fonts/custom-webfont.eot?#iefix) format("embedded-opentype"),
         url(../fonts/custom-webfont.woff) format("woff"),
         url(../fonts/custom-webfont.ttf) format("truetype"),
         url(../fonts/custom-webfont.svg#My-Font-Family) format("svg");
    font-weight: 400;
    font-style: normal;
}
```

## <a name="icons-imagery">Icons and Imagery</a>
Icon font vs. base64 vs. sprite. Use Resource's [guide for creating icon fonts](https://insider.resource.com/docs/DOC-2265).
![Small Images and Iconography Decision Tree](http://i.imgur.com/lVFZi25.png)


## <a name="browser-compatibility">Browser Compatibility</a>
Use vendor prefixes for experimental or non-spec properties.

```css
.container {
    display: -webkit-box;
    display: -webkit-flex;
    display: -moz-box;
    display: -ms-flexbox;
    display: flex
}
```

Use [fallbacks](http://flippinawesome.org/2013/07/08/using-css-fallback-properties-for-better-cross-browser-compatibility/) when necessary.

```css
/* good */
.future-stuff {
    color: #ccc;
    color: rgba(0, 0, 0, 0.5);
}
```

## <a name="accessibility">Accessibility</a>
Avoid low contrast color combinations. Use [Contrast Ratio](http://leaverou.github.io/contrast-ratio/) to verify accessibility. 

Avoid `outline: none`.

Avoid `display: none` when [hiding content](https://github.com/h5bp/html5-boilerplate/blob/master/css/main.css#L152).

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

## <a name="references">References</a>
#### CSS Inception Rule ####
- <a href="http://thesassway.com/beginner/the-inception-rule">http://thesassway.com/beginner/the-inception-rule</a>

#### CSS Specificity Related Articles ####
- Use of ID's in CSS Selectors (And why to avoid it)
    - <a href="http://oli.jp/2011/ids/">http://oli.jp/2011/ids/</a>
- Sorting and grouping of CSS properties
    - Use [CSSComb](http://csscomb.com/)

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
- <a href="http://pxtoem.com/">http://pxtoem.com/</a>
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

