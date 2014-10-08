# Resource HTML Style Guide

The "[Resource](https://github.com/resource) Way" of writing good Hypertext Markup.

## Table of Contents

1. [Document](#document)
1. [Tags](#tags)
1. [Semantics](#semantics)
1. [Accessibility](#accessibility)
1. [Separation Of Concerns](#separation-of-concerns)

***

## <a name='document'>Document</a>  

Use the HTML5 doctype.

```html
<!DOCTYPE html>
```

Define explicit character encoding to ensure proper rendering of content.

```html
<meta charset="utf-8">
```

Nest each tag.

```html
<!-- bad -->
<ul>
	<li><a href="...">Lorem ipsum</a></li>
</ul>

<!-- good -->
<ul>
	<li>
		<a href="...">Lorem ipsum</a>
	</li>
</ul>
```

Use tabs to indent.

```html
<!-- bad -->
<div>
••<div>Lorem ipsum</div>
</div>

<!-- good -->
<div>
	<div>Lorem ipsum</div>
</div>
```

Use proper settings for the `viewport`.

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

## <a name='tags'>Tags</a>  

Use lowercase for tags names and attributes.

```html
<!-- bad -->
<img SRC="images/walnut.jpg" ALT="Walnut tree">

<!-- good -->
<img src="images/walnut.jpg" alt="Walnut tree">
```

Use double quotes for attribute values.

```html
<!-- bad -->
<input type=text>

<!-- good -->
<input type="text">
```

Avoid trailing slashes on [void elements](http://www.w3.org/TR/html5/syntax.html#void-elements) (`<br>`, `<input>`, `<img>`).

Don’t omit [optional closing tags](http://www.w3.org/TR/html5/syntax.html#optional-tags).

Avoid type attributes on script and stylesheet includes - `text/css` and `text/javascript` are interpreted automatically.

Don't include values for [boolean attributes](https://html.spec.whatwg.org/multipage/infrastructure.html#boolean-attributes).

```html
<!-- bad -->
<input type="checkbox" value="1" checked="checked">

<!-- good -->
<input type="checkbox" value="1" checked>
```

## <a name='semantics'>Semantics</a>  

Use [semantic markup](http://www.adobe.com/devnet/html5/articles/semantic-markup.html).

```html
<!-- bad -->
<div>Heading</div>
<div>Paragraph copy</div>

<!-- good -->
<h1>Heading</h1>
<p>Paragraph copy</p>
```

Use `<span>` and `<div>` appropriately. Spans are for used for *in-line* styles - divs are used to build (block-level) structure.

## <a name='accessibility'>Accessibility</a>  

Declare a [language attribute](http://www.w3.org/html/wg/drafts/html/master/semantics.html#the-html-element) on the opening `<html>` tag.

```html
<html lang="en">
```

Use title and [alt](http://webaim.org/techniques/alttext/#basics) attributes on images.

```html
<img src="images/maple.jpg" alt="Maple tree" title="Maple tree">
```

Use [aria attributes](http://webaim.org/techniques/aria/).

```html
<header aria-role="banner">
	<nav aria-role="navigation"></nav>
</header>
```

## <a name='separation-of-concerns'>Separation of Concerns</a>  

Avoid obtrusive JavaScript. JavaScript should live in `.js` files. This helps keep a clear separation of concerns and aids in code scalability and maintainability.

```html
<!-- bad -->
<button onclick="submit()">Click Me!</button>
```

Don't rely on markup for visual formatting. (e.g. `<br>`, `<b>`, `<em>`).

```html
<!-- bad -->
<p>
	Walnut heartwood is a heavy, hard, open-grained hardwood.
	<br>
	Freshly cut live wood may be Dijon-mustard colour, darkening to brown over a few days.
</p>

<!-- good -->
<p>
	Walnut heartwood is a heavy, hard, open-grained hardwood.
</p>
<p>
	Freshly cut live wood may be Dijon-mustard colour, darkening to brown over a few days.
</p>
```

If you use inline formatting tags such as `<b>`, `<em>`, `<strong>`, etc, ensure that the appropriate styles are defined in your stylesheet.





