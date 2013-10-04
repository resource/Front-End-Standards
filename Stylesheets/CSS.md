# CSS Style Guide
The "[Resource](https://github.com/resource) Way" of writing legible, scalable, and useful CSS.

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
Don't over comment, as most CSS should be self-explanatory. Too much commenting detracts from readability.

```css
/* bad */
.selector {
    height: 100px; /* set height to 100px */
    width: 100px; /* set width the same as height */
    color: #ff0000; /* red */
}


/* good */
/* selector block */
.selector {
    height: 100px;
    width: 100px;
    color: #ff000;
}
```

### Comment Formatting

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
    margin: 13px;
    padding: 42px;
    width: 100px;
    height: 100px;
}
```

Keep [similar properties](http://www.w3.org/wiki/CSS/Properties) grouped together. Use [CSScomb](http://csscomb.com/) with the default settings.

```css
/* bad */
.selector {
    height: 100px;
    top: 0;
    z-index: 2;
    width: 100px;
    position: absolute;
    right: 0;
}

/* good */
.selector {
    position: absolute;
    top: 0;
    right: 0;
    z-index: 2;
    width: 100px;
    height: 100px;
}
```

Separate declaration blocks with a blank line.

```css
/* bad */
.selector {
    ...
}
.another-selector {
    ...
}

/* good */
.selector {
    ...
}
↩
.another-selector {
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

Use tabs to indent.

```css
/* bad */
.selector {
••float: left;
}

/* good */
.selector {
    float: left;
}
```

Avoid pseudo-nesting declaration blocks.

```css
/* bad */
.selector {
    ...
}
    .another-selector {
       ...
    }

/* good */
.selector {
    ...
}

.another-selector {
   ...
}
```


## <a name="selectors">Selectors</a>

### Naming
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

Selectors should be dash-delimited.

```css
/* bad */
.super_cool_selector {
    ...
}

/* good */
.super-cool-selector {
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

Avoid [overly-semantic](http://www.webdesignerdepot.com/2009/05/10-best-css-practices-to-improve-your-code/) selector names.

```css
/* bad */
.cart-item-blue {
    ...
}

.post-text-large {
    ...
}

/* good */
.cart-item-selected {
    ...
}

.post-title {
    ...
}

/* ok - helper class */
.margin-left--small {
    ...
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
.selector {
    color: blue;
}

/* ok */
.selector {
    color: #0000ff;
}

/* good */
.selector {
    color: #00f;
}

.selector-alt {
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
.text-bold {
  font-weight: bold;
}

/* good */
.text-bold {
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
.selector {
  background-image: url("../img/frown.png");
}

/* bad */
.selector {
  background-image: url(/img/frown.png);
}

/* good */
.selector {
  background-image: url(../img/rainbow.png);
}
```


## <a name="typography">Typography</a>
Use `em` for `font-size`. [PXtoEM](http://pxtoem.com/) can help with the conversion. 

Use [unit-less values](http://meyerweb.com/eric/thoughts/2006/02/08/unitless-line-heights/) for `line-height`.

```css
/* bad */
.selector {
    font-size: 1em;
    line-height: 1.3em;
}

/* good */
.selector {
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
Use the appropriate image delivery method.

![Small Images and Iconography Decision Tree](http://i.imgur.com/lVFZi25.png)


## <a name="browser-compatibility">Browser Compatibility</a>
Use vendor prefixes for experimental or non-spec properties.

```css
.selector {
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

[Avoid](http://www.outlinenone.com/) `outline: none`.

[Avoid](http://snook.ca/archives/html_and_css/hiding-content-for-accessibility) `display: none` when hiding content.

```css
/* bad */
.hidden-visually {
   display: none;
}

/* good */
.hidden-visually {
    position: absolute;
    overflow: hidden;
    clip: rect(0 0 0 0);
    margin: -1px;
    padding: 0;
    width: 1px;
    height: 1px;
    border: 0;
}
```

## <a name="references">References</a>

### Declarations and Values
- [CSScomb](http://csscomb.com/)
- [Common Website & Web Design Terms](http://logicpool.com/archives/235)

### Specificity
- [Inception Rule](http://thesassway.com/beginner/the-inception-rule)
- [Don’t use IDs in CSS selectors?](http://oli.jp/2011/ids/)
- [10 Best CSS Practices to Improve Your Code](http://www.webdesignerdepot.com/2009/05/10-best-css-practices-to-improve-your-code/)
- [Specificity - How is it calculated?](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity#How_is_it_calculated.3F)
- [CSS Specificity: Things You Should Know](http://coding.smashingmagazine.com/2007/07/27/css-specificity-things-you-should-know/)
- [Specificity Wars](http://www.stuffandnonsense.co.uk/archives/css_specificity_wars.html)

#### Efficiency ####
- [Efficiently Rendering CSS](http://css-tricks.com/efficiently-rendering-css/)

#### CSS Architecture ####
- BEM
    - [BEM Methodology](http://bem.info/method/)
- OOCSS
    - [An Introduction to Object Oriented CSS](http://coding.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/)
    - [Object Oriented CSS: Separating Skin From Structure](http://churchm.ag/object-oriented-css-separating-skin-from-structure/)
- DRY CSS
    - [DRY CSS: Don’t Repeat Your CSS](http://www.vanseodesign.com/css/dry-principles/)
- Normalize.css
    - [A modern, HTML5-ready alternative to CSS resets](https://github.com/necolas/normalize.css)

#### Typography ####
- [PXtoEM.com: PX to EM conversion made simple.](http://pxtoem.com/)
- [Unitless line-heights](http://meyerweb.com/eric/thoughts/2006/02/08/unitless-line-heights/)
- [Bulletproof font face](https://github.com/stubbornella/csslint/wiki/Bulletproof-font-face)
- [Definitive Guide to Webfonts](https://insider.resource.com/groups/technology-dlt/blog/2013/02/14/definitive-guide-to-webfonts)

#### Icons and Imagery ####
- [Resource's guide for creating icon fonts](https://insider.resource.com/docs/DOC-2265)

#### Browser Compatibility ####
- [CSS Fallback Properties for Better Cross-browser Compatibility](http://flippinawesome.org/2013/07/08/using-css-fallback-properties-for-better-cross-browser-compatibility/)

#### Accessibility ####
- [Contrast Ratio: Easily calculate color contrast ratios. Passing WCAG was never this easy!](http://leaverou.github.io/contrast-ratio/)
- [CSS outline property - outline: none and outline: 0](http://www.outlinenone.com/)
- [Hiding Content for Accessibility](http://snook.ca/archives/html_and_css/hiding-content-for-accessibility)

