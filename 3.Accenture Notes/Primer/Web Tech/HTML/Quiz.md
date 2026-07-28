#webTech #accenture #quiz #html

# Pre quiz


## Question 1

### Question
Which of the following is/are the new feature(s) of HTML5?

- A. Enhanced comment lines
- B. Supports offline Storage
- C. Browser automatically provide space before and after the tag `<p>`
- D. Performs Client-Side validation

---

### Answer
**Supports offline Storage**
**Performs Client-Side validation**

---

### Explanation

#### Why Correct Answers are Correct

##### Supports offline Storage
HTML5 introduced mechanisms that allow web applications to store data locally on the user's device.

Examples:
- Local Storage
- Session Storage
- IndexedDB

Benefits:
- Faster access to data
- Reduced server requests
- Offline web application support

Important exam points:
- Offline storage is a major HTML5 feature.
- Local Storage and Session Storage were introduced as part of modern web standards.

---

##### Performs Client-Side validation
HTML5 introduced built-in form validation features.

Examples:
- `required`
- `email`
- `number`
- `min`
- `max`
- `pattern`

Benefits:
- Reduces invalid submissions
- Improves user experience
- Reduces server-side validation load

Important exam points:
- HTML5 supports built-in client-side form validation.

---

#### Why Option A is Wrong
HTML5 did not introduce enhanced comment syntax.

HTML comments remain:

`<!-- Comment -->`

No major HTML5 feature relates to enhanced comment lines.

---

#### Why Option B is Correct
Offline storage support is one of HTML5's most important additions.

---

#### Why Option C is Wrong
Browsers traditionally provide default margins around `<p>` elements through browser stylesheets.

This behavior existed before HTML5 and is not a new HTML5 feature.

---

#### Why Option D is Correct
Built-in client-side validation is a significant HTML5 enhancement.

---

## Question 2

### Question
An application that lets you search and see material on the internet is

- A. Website
- B. Homepage
- C. Browser
- D. Webpage

---

### Answer
**Browser**

---

### Explanation

#### Why Correct Answer is Correct
A browser is software used to access, retrieve, and display information on the internet.

Examples:
- Google Chrome
- Mozilla Firefox
- Microsoft Edge
- Safari

Functions:
- Open websites
- Search the web
- Display web pages
- Run web applications

Important exam points:
- Browser = Application used to access the web.

---

#### Why Option A is Wrong
A website is a collection of related web pages.

Examples:
- Amazon
- Wikipedia
- YouTube

A website is accessed through a browser.

---

#### Why Option B is Wrong
A homepage is the main page of a website.

It is not the application used to access the internet.

---

#### Why Option C is Correct
A browser is the software application used to search and view internet content.

---

#### Why Option D is Wrong
A webpage is a single document displayed inside a browser.

It is not the application itself.

---

## Question 3

### Question
Which element is a container for all the head elements, and may include the document title, scripts, styles, meta information, and more?

- A. `<title></title>`
- B. `<head></head>`
- C. `<body></body>`
- D. `<br></br>`

---

### Answer
**`<head></head>`**

---

### Explanation

#### Why Correct Answer is Correct
The `<head>` element contains metadata and resources used by the browser.

Common contents include:
- Title
- Meta tags
- CSS stylesheets
- JavaScript references
- Character encoding information

Important exam points:
- `<head>` stores metadata.
- Content inside `<head>` is generally not displayed directly on the webpage.

---

#### Why Option A is Wrong
`<title>` defines the page title but is only one element contained within `<head>`.

---

#### Why Option B is Correct
`<head>` is the container for title, meta information, styles, scripts, and other metadata.

---

#### Why Option C is Wrong
`<body>` contains visible webpage content.

Examples:
- Text
- Images
- Forms
- Buttons

---

#### Why Option D is Wrong
`<br>` creates a line break and is unrelated to metadata.

---

## Question 4

### Question
HTML stands for __________

- A. Hot Markup Language
- B. Hybrid Text Markup Language
- C. Hyper Text Markup Language
- D. Hot Mail

---

### Answer
**Hyper Text Markup Language**

---

### Explanation

#### Why Correct Answer is Correct
HTML stands for **Hyper Text Markup Language**.

Meaning of each term:

- Hyper Text → Text containing links to other documents.
- Markup → Tags used to structure content.
- Language → Standardized syntax used to create web pages.

HTML is the foundation of web development.

Important exam points:
- HTML is not a programming language.
- HTML is a markup language used to structure web content.

---

#### Why Option A is Wrong
"Hot Markup Language" is not a valid term.

---

#### Why Option B is Wrong
"Hybrid Text Markup Language" is incorrect.

---

#### Why Option C is Correct
This is the official expansion of HTML.

---

#### Why Option D is Wrong
Hotmail is an email service and unrelated to HTML.

---

# Post Quiz


## Question 2

### Question
If the phone number should accept only 10 digit numbers, which of the following options will suit?

- A. `<input type="text" min="0" max="9" />`
- B. `<input type="number" pattern="[0-9]{10}"/>`
- C. `<input type="number" min="0" max="9" />`
- D. `<input type="text" pattern="[0-9]{10}"/>`

---

### Answer
**`<input type="text" pattern="[0-9]{10}"/>`**

---

### Explanation

#### Why Correct Answer is Correct
The pattern:

`[0-9]{10}`

means:
- Digits 0–9 only
- Exactly 10 occurrences

This enforces a 10-digit phone number format.

Important exam points:
- `pattern` works reliably with text inputs.
- Common HTML5 validation technique.

---

#### Why Option A is Wrong
`min` and `max` do not limit the number of digits.

---

#### Why Option B is Wrong
HTML5 pattern validation is generally intended for text-based inputs.

Many certification exams expect `type="text"` with `pattern`.

---

#### Why Option C is Wrong
Allows only values between 0 and 9.

Not 10-digit numbers.

---

#### Why Option D is Correct
This correctly enforces exactly ten digits.

---

## Question 3

### Question
Ram has designed a portal that fetches the citizens' feedback regarding the voting process in India. The portal allows the end user to choose either 'like' image or 'unlike' image, so that it gets redirected to a page : "thanks.html".

---

### Answer
**Option 1**

```html
<form action="thanks.html">

<input type="image" src="like.jpg" alt="submit"/>

<input type="image" src="unlike.jpg" alt="submit"/>

</form>
```

---

### Explanation

#### Why Correct Answer is Correct
The `image` input type behaves like a submit button but is displayed as an image.

When either image is clicked:
- The form is submitted.
- The user is redirected to `thanks.html`.

Important exam points:
- `type="image"` = Image + Submit Button.
- Frequently used for graphical form submission.

---

#### Why Option 1 is Correct
Both images act as submit controls.

---

#### Why Option 2 is Wrong
`submit` inputs do not support images through `src` in this way.

---

#### Why Option 3 is Wrong
`img` tags do not submit forms.

Also `href` is invalid for `<img>`.

---

#### Why Option 4 is Wrong
`img` elements inside submit tags do not create image submit buttons.

The structure is invalid.

---

## Question 4

### Question
Consider the below webpage:

Which of the following is used to do this?

---

### Answer
**Option 2**

```html
<input type="date" id="date" name="date" list="holidays">

<datalist id="holidays">

    <option label="Republic Day">2017-01-26</option>

    <option label="May Day">2017-05-01</option>

    <option label="Independence Day">2017-08-15</option>

</datalist>
```

---

### Explanation

#### Why Correct Answer is Correct
The `datalist` element provides predefined suggestions for an input field.

Benefits:
- User can choose from suggested values.
- User may still enter custom values.
- Improves user experience.

Important exam points:
- `list` attribute connects an input with a datalist.
- `datalist` provides suggestions.

---

#### Why Option 1 is Wrong
`select` does not support `type="date"`.

---

#### Why Option 2 is Correct
This is the correct HTML5 datalist implementation.

---

#### Why Option 3 is Wrong
Only limits the date range.

Does not provide predefined holiday suggestions.

---

#### Why Option 4 is Wrong
`list` works only with `datalist`, not `select`.

---

## Question 5

### Question
In the web page, we have a field called phoneno and inside this textbox field, the text : "Only numbers are allowed" must appear. This should get disappeared automatically once we type the phoneno into it. Which of the below options will suit the given scenario?

- A. `<input type="tel" value="Only numbers are allowed">`
- B. `<input type="text" value="Only numbers are allowed">`
- C. `<input type="text" placeholder="Only numbers are allowed">`
- D. `<input type="tel" default="Only numbers are allowed">`
- E. `<input type="tel" placeholder="Only numbers are allowed">`

---

### Answer
**`<input type="text" placeholder="Only numbers are allowed">`**
**`<input type="tel" placeholder="Only numbers are allowed">`**

---

### Explanation

#### Why Correct Answers are Correct

##### `<input type="text" placeholder="Only numbers are allowed">`
The placeholder attribute displays instructional text inside the field.

Behavior:
- Visible initially.
- Disappears automatically when typing begins.

---

##### `<input type="tel" placeholder="Only numbers are allowed">`
Same placeholder behavior.

Additionally:
- Semantically represents a telephone number.
- Mobile devices may show a numeric keypad.

Important exam points:
- Placeholder text disappears automatically when the user starts typing.
- Placeholder is the intended HTML5 solution.

---

#### Why Option A is Wrong
`value` inserts actual text into the field.

The user must manually delete it.

---

#### Why Option B is Wrong
`value` does not behave like placeholder text.

---

#### Why Option C is Correct
Uses placeholder correctly.

---

#### Why Option D is Wrong
`default` is not a valid HTML input attribute.

---

#### Why Option E is Correct
Uses placeholder correctly and is semantically appropriate for phone numbers.

---