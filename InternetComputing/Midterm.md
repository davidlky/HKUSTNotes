## Midterm notes

- HTML -> HTML + CSS -> XML -> XHTML -> ... -> HTML 5
  - dropped the `X`
  - tags are objects with attributes

- watch out for closing tags, case sensitive tags, unescaped strings

- `dl -> dt -> dd`

- id for relative links

- `prompt`

Events
- string escaping for `"alert('escaped')"`
- `Math.Random()` -> [0,1)
- JS -> not graphics library and OO language \shrug

DOM -> tree

`setTimeOut("afsadasd()", 1000)` <- note the quotation mark around function

- document.images/applets/links are arrays of DOM

- `span` for inline shit

- tables sucks, inefficient need to load everything

`<map>` and `<area>` define the area within which a click will call a JavaScript function or jump a link
- `area` has `href`
- img needs `usemap="#website_overview"`

- `onkeydown` -> `key_event.keyCode`


- `.innerHTML` changes the text of something
- `.src` to change image for img

- embeded play media via plugin, better to use JS


CSS can be used for all XML based languages
- `:hover` etc are called Pseudo classes
- `FIRST-LETTER` and `FIRST-LINE` ??


priorities (cascading)
1. Inline styles: style attribute included within a tag
2. Embedded style: CSS rules inside the HTML itself
3. External style sheets: CSS files referenced from the HTML itself
4. User style: Local CSS file specified by the user on the browser
5. User agent style: browser’s default style sheet

JQuery: lib for DOM manipulation
- need to initialize

CSS
- `Immediate Sibling Selector: +`, same parent, immeidate next
- `Next Sibling Selector: ~` same parent

The World Wide Web Consortium (W3C)

## Svg
- coord start from top left corner
- polygon: `x,y x,y ...`
  - polyline: just line, not connected
- `image` -> `xlink:href="hong_kong.jpg"`

Path
- M = move to
- L = draw a straight line to
- H = draw a horizontal line to
- V = draw a vertical line to
- C = draw a curve to (uses a cubic Bezier)
- A = draw an arc to
- Z = finish/ go back to the beginning

Note: all path `d` value are based on absolute position

`Q` -> Quadratic Bezier curve
- `Q control,point end,point T,implicit`

can apply style just like html
- color -> fill

in `<defs><g id="id">...` you can reuse it later
- `<use id="" xlink:href="#id">`
- define `pattern` `clip-path`

Transform:
- translate, rotate, scale
  - rotate default is 0,0
- matrix (do all operations, individually or at same time)
- operations performed from right to left!

Animations
- animate
  - formatting any attribute
- animateColor
- animateMotion
  - animating object in motion path
- animateTransform
  - changing transformation;
- attributeType specifies XML or CSS


Matrices
- more efficient
- Initial Viewport -> outermost SVG or initial coordinate system
- transform coordinate system for all defined inside it

Current Transformation Matrix = all transformation you want to apply multiplied together


CSS review
- `.style.jsStyle = value`


```js
document.getElementsByTagName("circle")[0].parentNode.removeChild(document.getElementsBy
TagName("circle")[0]);
```