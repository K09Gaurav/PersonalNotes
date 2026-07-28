#webTech #accenture #quiz #javascript #jquery

# Pre quiz


## Question 1

### Question
Which of the following is/are true about HTML?

- A. Browser does not throw any error even if we have mistaken in the HTML syntax
- B. HTML is case sensitive
- C. Some of the tags are self closing while some of the tags must be explicitly closed in HTML5

---

### Answer
**Browser does not throw any error even if we have mistaken in the HTML syntax**
**Some of the tags are self closing while some of the tags must be explicitly closed in HTML5**

---

### Explanation

#### Why Correct Answers are Correct

##### Browser does not throw any error even if we have mistaken in the HTML syntax
HTML is a forgiving language.

Most browsers attempt to:
- Interpret invalid HTML
- Correct common mistakes
- Render the page anyway

Examples:
- Missing closing tags
- Incorrect nesting
- Extra attributes

Important exam points:
- Browsers try to recover from HTML errors.
- Unlike programming languages, HTML rarely stops execution.

---

##### Some of the tags are self closing while some of the tags must be explicitly closed in HTML5
HTML contains:

Self-closing/void elements:
- `<br>`
- `<hr>`
- `<img>`
- `<input>`
- `<meta>`

Normal elements requiring closing tags:
- `<div></div>`
- `<p></p>`
- `<section></section>`
- `<article></article>`

Important exam points:
- HTML contains both void elements and container elements.

---

#### Why Option A is Correct
Browsers generally tolerate HTML syntax mistakes.

---

#### Why Option B is Wrong
HTML is generally **case-insensitive**.

Examples:

```html
<body>
<BODY>
<BoDy>
```

All are treated the same by browsers.

---

#### Why Option C is Correct
Some tags are void/self-closing while others require explicit closing tags.

---

## Question 2

### Question
Which of the following is most appropriate tag in HTML5 to divide the document into logical document groups?

- A. `<div></div>`
- B. `<span></span>`
- C. `<group></group>`
- D. `<section></section>`

---

### Answer
**`<section></section>`**

---

### Explanation

#### Why Correct Answer is Correct
HTML5 introduced semantic elements to describe document structure more clearly.

The `<section>` element represents:
- A thematic grouping of content
- A logical section of a document
- Related content grouped together

Examples:
- Introduction
- Features
- Contact information

Important exam points:
- `<section>` = Logical grouping of content.

---

#### Why Option A is Wrong
`<div>` is generic and non-semantic.

---

#### Why Option B is Wrong
`<span>` is an inline element.

---

#### Why Option C is Wrong
`<group>` is not a standard HTML5 element.

---

#### Why Option D is Correct
This is the semantic HTML5 element designed for logical sections.

---

## Question 3

### Question
When referencing an HTML element using jQuery preceded by a `#`, what JavaScript function is this equivalent to?

- A. getElement
- B. getElementByTagName
- C. getElementByClassName
- D. getElementById

---

### Answer
**getElementById**

---

### Explanation

#### Why Correct Answer is Correct
In jQuery:

```javascript
$("#myid")
```

selects an element by its ID.

The equivalent JavaScript DOM method is:

```javascript
document.getElementById("myid")
```

Important exam points:
- `#` → ID selector
- `.` → Class selector

---

#### Why Option A is Wrong
No standard DOM method named `getElement()` exists.

---

#### Why Option B is Wrong
Used for selecting HTML tags.

Example:

```javascript
document.getElementsByTagName("p")
```

---

#### Why Option C is Wrong
Used for selecting class names.

---

#### Why Option D is Correct
`#id` corresponds to `getElementById()`.

---

## Question 4

### Question
If you want to change the color of a link to red when moving mouse pointer on top of it, which CSS property you need to change?

- A. `a:moved { color:red; }`
- B. `link:visited { color:red; }`
- C. `a { color:red; }`
- D. `a:hover { color:red; }`

---

### Answer
**`a:hover { color:red; }`**

---

### Explanation

#### Why Correct Answer is Correct
The `:hover` pseudo-class activates when the mouse pointer is placed over an element.

Example:

```css
a:hover {
    color: red;
}
```

Behavior:
- Normal color before hover
- Red color while mouse is over the link

Important exam points:
- Hover effect → `:hover`

---

#### Why Option A is Wrong
`moved` is not a valid CSS pseudo-class.

---

#### Why Option B is Wrong
`:visited` applies after the link has been visited.

---

#### Why Option C is Wrong
Changes the color permanently, not only during hover.

---

#### Why Option D is Correct
This is the correct CSS hover syntax.

---

## Question 5

### Question
The following elements are newly added elements in HTML5:

- `<section>`
- `<article>`
- `<aside>`

These elements are called _____________

- A. Graphic elements
- B. Semantic elements
- C. Control elements
- D. Multimedia elements

---

### Answer
**Semantic elements**

---

### Explanation

#### Why Correct Answer is Correct
HTML5 introduced semantic elements that describe the meaning of content.

Examples:

- `<section>`
- `<article>`
- `<aside>`
- `<header>`
- `<footer>`
- `<nav>`

Benefits:
- Better readability
- Improved accessibility
- Better SEO
- Clearer document structure

Important exam points:
- Semantic elements describe content meaning.

---

#### Why Option A is Wrong
These elements are not used for graphics.

---

#### Why Option B is Correct
They are HTML5 semantic elements.

---

#### Why Option C is Wrong
Control elements refer to user-input controls.

---

#### Why Option D is Wrong
Multimedia elements include:
- `<audio>`
- `<video>`

These are unrelated.

---

---

# Post Quiz


## Question 1

### Question
Raju wants to remove an event handler that was attached with `on()` function. Help him to select the correct option.

- A. empty()
- B. change()
- C. off()
- D. delete()

---

### Answer
**off()**

---

### Explanation

#### Why Correct Answer is Correct
In jQuery:

- `on()` → Attach event handlers
- `off()` → Remove event handlers

Example concept:

- Event attached using `on()`
- Same event removed using `off()`

Important exam points:
- `on()` and `off()` are complementary methods.

---

#### Why Option A is Wrong
`empty()` removes child elements and content, not event handlers.

---

#### Why Option B is Wrong
`change()` is an event method, not an event-removal method.

---

#### Why Option C is Correct
`off()` is specifically designed to remove event handlers.

---

#### Why Option D is Wrong
`delete()` is not a jQuery event-handling method.

---

## Question 2

### Question
Bind an event handler to the "blur" JavaScript event on an element.

- A. `.blurElement()`
- B. `.blur()`
- C. `.blurOn()`
- D. `.focus()`

---

### Answer
**.blur()**

---

### Explanation

#### Why Correct Answer is Correct
The blur event occurs when an element loses focus.

Examples:
- User leaves a textbox
- Cursor moves away from an input field

jQuery provides:

`.blur()`

to bind or trigger blur events.

Important exam points:
- Focus gained → `focus()`
- Focus lost → `blur()`

---

#### Why Option A is Wrong
No such jQuery method exists.

---

#### Why Option B is Correct
This is the official jQuery blur method.

---

#### Why Option C is Wrong
No such jQuery method exists.

---

#### Why Option D is Wrong
`focus()` is the opposite event.

---

## Question 3

### Question
Kiran wants to remove all the child nodes from the given div element. Help him to select the correct option to remove all the child nodes from the div element.

- A. remove(expr)
- B. empty()
- C. None of the above
- D. delete()

---

### Answer
**empty()**

---

### Explanation

#### Why Correct Answer is Correct
The jQuery `empty()` method:

- Removes all child elements
- Removes all text nodes
- Leaves the parent element intact

For the given div:

Before:

```html
<div>
  Text
  <h2>...</h2>
  <p>...</p>
</div>
```

After `empty()`:

```html
<div></div>
```

Important exam points:
- Remove contents only → `empty()`
- Remove entire element → `remove()`

---

#### Why Option A is Wrong
`remove()` removes the selected element itself.

---

#### Why Option B is Correct
Removes all child nodes while preserving the parent.

---

#### Why Option C is Wrong
A correct option exists.

---

#### Why Option D is Wrong
No such jQuery method exists.

---

## Question 4

### Question
Rhita wants to replace a jQuery code `$(document).ready(fun)` using another equivalent method. Help her to find the correct method from the given options.

- A. `#(fun)`
- B. `jQury(fun)`
- C. There is no equivalent function for the given code
- D. `$(fun)`

---

### Answer
**$(fun)**

---

### Explanation

#### Why Correct Answer is Correct
The following two forms are equivalent:

```javascript
$(document).ready(fun)
```

and

```javascript
$(fun)
```

Both execute the function when the DOM is fully loaded.

Important exam points:
- Short-hand ready function → `$(fun)`

---

#### Why Option A is Wrong
Invalid syntax.

---

#### Why Option B is Wrong
Invalid jQuery syntax.

---

#### Why Option C is Wrong
An equivalent shorthand exists.

---

#### Why Option D is Correct
This is the official shorthand form.

---

## Question 5

### Question
jQuery is a JavaScript Object Notation library.

- A. True
- B. False

---

### Answer
**False**

---

### Explanation

#### Why False is Correct
jQuery is:

- A JavaScript library
- Used for DOM manipulation
- Event handling
- Animations
- AJAX

JSON stands for:

**JavaScript Object Notation**

JSON is a data-interchange format, not jQuery.

Important exam points:
- jQuery ≠ JSON
- Very common exam trap.

---

#### Why True is Wrong
jQuery and JSON are completely different technologies.

---

#### Why False is Correct
The statement incorrectly describes jQuery.

---

## Question 6

### Question
`$("#name").remove();`
This will remove the text field when you click on the button. State true or false.

- A. True
- B. False

---

### Answer
**True**

---

### Explanation

#### Why True is Correct
The statement:

```javascript
$("#name").remove();
```

removes the selected element from the DOM.

If `#name` refers to a textbox:

```html
<input id="name">
```

then the textbox itself is removed.

Important exam points:
- `remove()` deletes the entire selected element.

---

### Exam Tip

Although the statement itself does not explicitly contain a button click handler, certification questions usually assume it is executed when the button is clicked. Therefore the expected answer is **True**.

---

#### Why True is Correct
The textbox would be removed when this statement executes.

---

#### Why False is Wrong
`remove()` definitely removes the selected element.

---

## Question 7

### Question
John wants to animate (moving effect) an element in the webpage he designed. For this, he set its CSS position property to its default value and applied the animations. If there is no syntax error in the code, what would be output he gets?

- A. Animation failed because the CSS position property set to default value
- B. Animation failed because the CSS position property set to Fixed
- C. Run the webpage successfully with animated elements
- D. Animation failed because the CSS position property set to static

---

### Answer
**Animation failed because the CSS position property set to static**

---

### Explanation

#### Why Correct Answer is Correct
The default CSS position value is:

```css
position: static;
```

For many jQuery movement animations involving:

- left
- right
- top
- bottom

the element must use:

- relative
- absolute
- fixed

A static element cannot be repositioned using these properties.

Important exam points:
- Default position = static
- Moving animations typically require non-static positioning.

---

#### Why Option A is Wrong
The more precise reason is that the default value is static.

---

#### Why Option B is Wrong
The question says default value, not fixed.

---

#### Why Option C is Wrong
Movement animations generally fail when position remains static.

---

#### Why Option D is Correct
Static positioning prevents movement-based animations.

---

## Question 8

### Question
Some people don’t want animation to interfere with their web page experience. What do I do if I want to let a user turn off the animation?

- A. Not possible to turn off the animation by the user
- B. Use the jQuery method: stop()
- C. Use the jQuery method: stop.animation()

---

### Answer
**Use the jQuery method: stop()**

---

### Explanation

#### Why Correct Answer is Correct
The jQuery `stop()` method:

- Stops the currently running animation
- Prevents queued animations from continuing
- Gives users control over animation behavior

Important exam points:
- Stop animation → `stop()`

---

#### Why Option A is Wrong
Animations can be stopped programmatically.

---

#### Why Option B is Correct
This is the official jQuery method.

---

#### Why Option C is Wrong
`stop.animation()` is not a valid jQuery method.

---