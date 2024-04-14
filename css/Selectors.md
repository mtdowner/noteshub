# CSS Selectors

## Type Selectors
- tag name selector or element selector

## Universal Selector
- indicated by an asterisk (*)
- selects everything in the document, or
-  inside parent element if it is being chained together with another element and a descendant combinator

## Class Selectors
- starts with a dot (.) character
- selects elements based on the class applied to it

## ID Selectors
- begins with a #
- used in the same way as a class selector
- . can only be used only once per page
- elements can only have a single id value applied to them
- can select an element that has the id set on it
- can precede the ID with a type selector to only target the element if both the element and ID match

## Attribute selectors

Attribute selectors match elements with an attribute value or substring value match.

Case-insensitive:
- HTML attribute names
- attribute value in selector of HTML attribute name

`accept`
`accept-charset`
`align`
`alink`
`axis`
`bgcolor`
`charset`
`checked`
`clear`
`codetype`
`color`
`compact`
`declare`
`defer`
`dir`
`direction`
`disabled`
`enctype`
`face`
`frame`
`hreflang`
`http-equiv`
`lang`
`language`
`link`
`media`
`method`
`multiple`
`nohref`
`noresize`
`noshade`
`nowrap`
`readonly`
`rel`
`rev`
`rules`
`scope`
`scrolling`
`selected`
`shape`
`target`
`text`
`type`
`valign`
`valuetype`
`vlink`

Case-sensitive:
- attribute value is case-sensitive when attribute selector value match is case-sensitive
- attributes outside of HTML specification i.e `role` and `aria-*`
- case-sensitive attribute selectors can be made case-insensitive with the inclusion of the case-insensitive modifier (i).

**CSS**

```css
/* <a> elements with a title attribute */

a[title] {
  color: purple;
}

/* <a> elements with an href matching "https://example.org" */

a[href="https://example.org"] {
  color: green;
}

/* <a> elements with an href containing "example" */
a[href*="example"] {
  font-size: 2em;
}

/* <a> elements with an href ending ".org", case-insensitive */
  a[href$=“.org” i] {
  font-style: italic;
}

/* <a> elements whose class attribute contains the word "logo" */
a[class~=“logo”] {
  padding: 2px;
}
```

## Syntax

```css
[attr]
Represents elements with an attribute name of attr.

[attr=value]
Represents elements with an attribute name of attr whose value is exactly value.

[attr~=value]
Represents elements with an attribute name of attr whose value is a whitespace-separated list of words, one of which is exactly value.

[attr|=value]
Represents elements with an attribute name of attr whose value can be exactly value or can begin with value immediately followed by a hyphen, - (U+002D). It is often used for language subcode matches.

[attr^=value]
Represents elements with an attribute name of attr whose value is prefixed (preceded) by value.

[attr$=value]
Represents elements with an attribute name of attr whose value is suffixed (followed) by value.

[attr*=value]
Represents elements with an attribute name of attr whose value contains at least one occurrence of value within the string.

[attr operator value i]
Adding an i (or I) before the closing bracket causes the value to be compared case-insensitively (for characters within the ASCII range).

[attr operator value s] Experimental
Adding an s (or S) before the closing bracket causes the value to be compared case-sensitively (for characters within the ASCII range).
```

### Examples

CSS

```css
a {
  color: blue;
}

/* Internal links, beginning with "#" */
a[href^="#"] {
  background-color: gold;
}

/* Links with "example" anywhere in the URL */
a[href*="example"] {
  background-color: silver;
}

/* Links with "insensitive" anywhere in the URL,
   regardless of capitalization */
a[href*="insensitive" i] {
  color: cyan;
}

/* Links with "cAsE" anywhere in the URL,
with matching capitalization */
a[href*="cAsE" s] {
  color: pink;
}

/* Links that end in ".org" */
a[href$=".org"] {
  color: red;
}

/* Links that start with "https://" and end in ".org" */
a[href^="https://"][href$=".org"]
{
  color: green;
}
```

HTML

```html
<ul>
  <li><a href="#internal">Internal link</a></li>
  <li><a href="http://example.com">Example link</a></li>
  <li><a href="#InSensitive">Insensitive internal link</a></li>
  <li><a href="http://example.org">Example org link</a></li>
  <li><a href="https://example.org">Example https org link</a></li>
</ul>
```

```css
/* All divs with a `lang` attribute are bold. */
div[lang] {
  font-weight: bold;
}

/* All divs without a `lang` attribute are italicized. */
div:not([lang]) {
  font-style: italic;
}

/* All divs in US English are blue. */
div[lang~=“en-us”] {
  color: blue;
}

/* All divs in Portuguese are green. */
div[lang=“pt”] {
  color: green;
}

/* All divs in Chinese are red, whether
   simplified (zh-Hans-CN) or traditional (zh-Hant-TW). */
div[lang|=“zh”] {
  color: red;
}

/* All divs with a Traditional Chinese
   `data-lang` are purple. */
/* Note: You could also use hyphenated attributes
   without double quotes */
div[data-lang=“zh-Hant-TW”] {
  color: purple;
}
```


HTML

```html
<div lang="en-us en-gb en-au en-nz">Hello World!</div>
<div lang="pt">Olá Mundo!</div>
<div lang="zh-Hans-CN">世界您好！</div>
<div lang="zh-Hant-TW">世界您好！</div>
<div data-lang="zh-Hant-TW">世界您好！</div>
```

## HTML ordered lists

The HTML specification requires the type attribute to be matched case-insensitively because it is primarily used in the `<input>` element. Note that if a modifier is not supported by the user agent, then the selector will not match.

```css
/* Case-sensitivity depends on document language */
ol[type="a"] {
  list-style-type: lower-alpha;
  background: red;
}

ol[type="b" s] {
  list-style-type: lower-alpha;
  background: lime;
}

ol[type="B" s] {
  list-style-type: upper-alpha;
  background: grey;
}

ol[type="c" i] {
  list-style-type: upper-alpha;
  background: green;
}
```

HTML

```html
<ol type="A">
  <li>
    Red background for case-insensitive matching (default for the type selector)
  </li>
</ol>
<ol type="b">
  <li>Lime background if `s` modifier is supported (case-sensitive match)</li>
</ol>
<ol type="B">
  <li>Grey background if `s` modifier is supported (case-sensitive match)</li>
</ol>
<ol type="C">
  <li>
    Green background if `i` modifier is supported (case-insensitive match)
  </li>
</ol>
```