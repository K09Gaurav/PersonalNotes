---
tags:
  - accenture
  - quiz
  - javascript
  - webTech
---
-


# Pre Quiz


## Question 1

### Question
Which of the below statements are used to comment a line in JavaScript file?

- A. `/* this is a comment */`
- B. `<!-- this is a comment -->`
- C. `// this is a comment`
- D. `// this is a comment //`

---

### Answer
**`// this is a comment`**

---

### Explanation

#### Why Correct Answer is Correct
JavaScript uses:

- `//` for single-line comments
- `/* ... */` for multi-line comments

Since the question specifically asks for commenting **a line**, the expected answer is:

`// this is a comment`

Important exam points:
- Single-line comment → `//`
- Multi-line comment → `/* ... */`

---

### Exam Tip

Although `/* this is a comment */` is a valid JavaScript comment, certification questions often distinguish between:

- Single-line comment → `//`
- Multi-line comment → `/* ... */`

Because the question says **"comment a line"**, the expected answer is `//`.

---

#### Why Option A is Wrong
This is a valid JavaScript comment but is generally used for block or multi-line comments.

---

#### Why Option B is Wrong
This is an HTML comment syntax, not standard JavaScript commenting.

---

#### Why Option C is Correct
This is the standard single-line JavaScript comment.

---

#### Why Option D is Wrong
The ending `//` is unnecessary and not the standard syntax expected by exams.

---

## Question 2

### Question
David, a beginner in web development trying to perform one particular operation using client side JavaScript. Choose the correct option(s) that he can't be done with client-side JavaScript?

- A. Store the form's contents to a database file on the server
- B. Display the alert box to the user
- C. Validate a form
- D. Send a form's contents by email

---

### Answer
**Store the form's contents to a database file on the server**

---

### Explanation

#### Why Correct Answer is Correct
Client-side JavaScript runs inside the user's browser.

For security reasons, it cannot directly:
- Access server databases
- Write records into server files
- Modify server-side resources

These tasks require server-side technologies such as:
- Java
- Node.js
- PHP
- Python
- .NET

Important exam points:
- Client-side JavaScript cannot directly interact with server databases.

---

#### Why Option A is Correct
Database storage requires server-side processing.

---

#### Why Option B is Wrong
JavaScript can display alert boxes using browser APIs.

---

#### Why Option C is Wrong
Form validation is one of the most common uses of client-side JavaScript.

---

#### Why Option D is Wrong
JavaScript can trigger email-related actions through forms or mail links, so exams generally do not consider this impossible.

---

## Question 3

### Question
Sita wishes to greet the user when the user clicks on "Greet Me" button. In which event does she need to write the JavaScript code for greeting the user?

- A. onclick
- B. onmouseover
- C. onchange
- D. onmouseclick

---

### Answer
**onclick**

---

### Explanation

#### Why Correct Answer is Correct
The `onclick` event is triggered whenever a user clicks an element.

Common uses:
- Buttons
- Links
- Images
- Interactive controls

Important exam points:
- Mouse click → onclick

---

#### Why Option A is Correct
This event is specifically designed for click actions.

---

#### Why Option B is Wrong
`onmouseover` occurs when the mouse pointer moves over an element.

---

#### Why Option C is Wrong
`onchange` occurs when an input value changes.

---

#### Why Option D is Wrong
`onmouseclick` is not a standard JavaScript event.

---

## Question 4

### Question
When you want to enclose some JavaScript statements in an HTML file, which is the correct tag you have to use?

- A. `<BODY>`
- B. `<SCRIPT>`
- C. `<STYLE>`
- D. `<HEAD>`

---

### Answer
**`<SCRIPT>`**

---

### Explanation

#### Why Correct Answer is Correct
JavaScript code is placed inside the `<script>` element.

This tag informs the browser that the enclosed content should be interpreted as JavaScript.

Important exam points:
- JavaScript → `<script>`
- CSS → `<style>`

---

#### Why Option A is Wrong
`<body>` contains webpage content.

---

#### Why Option B is Correct
This is the official tag for JavaScript code.

---

#### Why Option C is Wrong
`<style>` is used for CSS.

---

#### Why Option D is Wrong
`<head>` may contain script tags but is not itself the JavaScript container.

---

## Question 5

### Question
Which of the below JavaScript code helps to change the content of the paragraph tag dynamically?

Given:

```html
<p id="pid1">Aim Higher.. Sky is your limit
```

- A. `document.getElement("p").innerHTML = "Never give up!!";`
- B. `#demo.innerHTML = "Never give up!!";`
- C. `document.getElementByName("p").innerHTML = "Never give up!!";`
- D. `document.getElementById("pid1").innerHTML = "Never give up!!";`

---

### Answer
**`document.getElementById("pid1").innerHTML = "Never give up!!";`**

---

### Explanation

#### Why Correct Answer is Correct
The paragraph has:

`id="pid1"`

To access an element by its ID, JavaScript uses:

`document.getElementById()`

The `innerHTML` property changes the displayed content.

Important exam points:
- ID selection → `getElementById()`
- Content update → `innerHTML`

---

#### Why Option A is Wrong
`getElement()` is not a valid DOM method.

---

#### Why Option B is Wrong
This is CSS selector syntax, not valid standalone JavaScript.

---

#### Why Option C is Wrong
The element has an ID, not a name attribute.

---

#### Why Option D is Correct
This correctly targets the paragraph and changes its content.

---

## Question 6

### Question
When a user views a page containing a JavaScript program, which machine actually executes the script?

- A. The Web server
- B. A central machine deep within Netscape's corporate offices
- C. The User's machine running a Web browser
- D. Database Server

---

### Answer
**The User's machine running a Web browser**

---

### Explanation

#### Why Correct Answer is Correct
Client-side JavaScript executes within the browser on the user's device.

Examples:
- Chrome
- Firefox
- Edge
- Safari

Execution flow:
1. Browser downloads HTML and JavaScript.
2. Browser interprets JavaScript.
3. Code runs locally on the user's machine.

Important exam points:
- Client-side JavaScript executes in the browser.
- Not on the server.

---

#### Why Option A is Wrong
The web server delivers the file but does not execute client-side JavaScript.

---

#### Why Option B is Wrong
This is clearly not how JavaScript execution works.

---

#### Why Option C is Correct
The browser on the user's machine executes the script.

---

#### Why Option D is Wrong
Database servers store and retrieve data but do not execute client-side JavaScript.

---

---
# Post Quiz


## Question 1

### Question
Ram is the developer of Allen Software company. He is designing the website for the banking application. There is a button called "check interest rates". When that button is clicked, the user has to be redirected to a separate page to show the domestic interest rates. Help Ram in accomplishing this task using JavaScript.

- A. `url.newlocation`
- B. `page.location`
- C. `window.location`
- D. `window.reload`

---

### Answer
**`window.location`**

---

### Explanation

#### Why Correct Answer is Correct
`window.location` is used to get or change the current URL of the browser.

It is commonly used for:
- Redirecting users
- Navigating to another page
- Loading a different URL

Important exam points:
- Page redirection → `window.location`
- Very common DOM/BOM property

---

#### Why Option A is Wrong
`url.newlocation` is not a valid JavaScript property.

---

#### Why Option B is Wrong
`page.location` is not a standard JavaScript object.

---

#### Why Option C is Correct
This is the standard property used for browser redirection.

---

#### Why Option D is Wrong
`window.reload` is not used for redirection.

The actual method is `window.location.reload()` for refreshing a page.

---

## Question 2

### Question
Predict the output of the following JavaScript code:

```html
var txt= "pass 70% fail 30%";

var pattern = /\D/g;

var res= txt.match(pattern);

document.write(res);
```

- A. `7,0,%, ,3,0,%`
- B. `7,0,3,0`
- C. `7,0,%,3,0,%`
- D. `p,a,s,s, ,%, ,f,a,i,l, ,%`

---

### Answer
**`p,a,s,s, ,%, ,f,a,i,l, ,%`**

---

### Explanation

#### Why Correct Answer is Correct
The regex:

`\D`

means:

**Match every non-digit character**

The string is:

`pass 70% fail 30%`

Digits:
- 7
- 0
- 3
- 0

Everything else matches:

- p
- a
- s
- s
- space
- %
- space
- f
- a
- i
- l
- space
- %

The `match()` method returns all matching characters.

Important exam points:
- `\d` → Digit
- `\D` → Non-digit

---

#### Why Option A is Wrong
Contains digits rather than non-digits.

---

#### Why Option B is Wrong
Shows only digits.

---

#### Why Option C is Wrong
Still contains digits.

---

#### Why Option D is Correct
These are all non-digit characters found in the string.

---

## Question 3

### Question
Choose the correct JavaScript statement which helps you to write "World of JavaScript" in a web page?

- A. `println ("World of JavaScript")`
- B. `response.write("World of JavaScript")`
- C. `document.write("World of JavaScript")`
- D. `System.out.println("World of JavaScript")`

---

### Answer
**`document.write("World of JavaScript")`**

---

### Explanation

#### Why Correct Answer is Correct
`document.write()` writes content directly into the HTML document.

Important exam points:
- Basic webpage output → `document.write()`

---

#### Why Option A is Wrong
`println()` is not a standard JavaScript output function.

---

#### Why Option B is Wrong
`response.write()` is associated with server-side technologies.

---

#### Why Option C is Correct
This is the standard browser-side output statement.

---

#### Why Option D is Wrong
`System.out.println()` belongs to Java.

---

## Question 4

### Question
Which of the below is the correct syntax for executing some code if "amt" is equal to 5000?

- A. `if (amt = 5000)`
- B. `if (amt equals 5000)`
- C. `if (amt == 5000)`
- D. `if (amt === "5000")`

---

### Answer
**`if (amt == 5000)`**

---

### Explanation

#### Why Correct Answer is Correct
`==` is the equality comparison operator in JavaScript.

It checks whether two values are equal after type conversion if necessary.

Important exam points:
- `=` → Assignment
- `==` → Equality comparison
- `===` → Strict equality

---

### Exam Tip

In modern JavaScript, `===` is usually preferred. However, because the question specifically checks whether `amt` equals the numeric value `5000`, certification exams typically expect:

`if (amt == 5000)`

---

#### Why Option A is Wrong
Uses assignment, not comparison.

---

#### Why Option B is Wrong
`equals` is not JavaScript syntax.

---

#### Why Option C is Correct
This is the expected equality-check syntax.

---

#### Why Option D is Wrong
This checks whether the value is the string `"5000"` and the type is also string.

---

## Question 5

### Question
The `parseInt()` method converts the string to an integer. Before applying this function, Ram wants to know the type of the argument that is passed to the function. Which operator in JavaScript would support this?

- A. getType
- B. isofType
- C. instanceof
- D. typeof

---

### Answer
**typeof**

---

### Explanation

#### Why Correct Answer is Correct
`typeof` is used to determine the data type of a variable.

Examples:
- number
- string
- boolean
- object
- function

Important exam points:
- Data type checking → `typeof`

---

#### Why Option A is Wrong
No such JavaScript operator exists.

---

#### Why Option B is Wrong
Not a valid JavaScript operator.

---

#### Why Option C is Wrong
`instanceof` checks object inheritance, not primitive data types.

---

#### Why Option D is Correct
This is the standard operator for type checking.

---

## Question 6

### Question
Polson is allocated with the task of email validation in JavaScript. He needs to extract character by character and check for email validation like looking for @, ., etc. Which method is best suited to extract every character from the text?

- A. `getCharAt()`
- B. `charAt()`
- C. `characterAt()`

---

### Answer
**`charAt()`**

---

### Explanation

#### Why Correct Answer is Correct
`charAt()` returns the character at a specified position within a string.

Example usage:
- First character
- Second character
- Character-by-character processing

Important exam points:
- String character extraction → `charAt()`

---

#### Why Option A is Wrong
Not a JavaScript string method.

---

#### Why Option B is Correct
This is the official JavaScript method.

---

#### Why Option C is Wrong
No such JavaScript method exists.

---

## Question 7

### Question
What is the output of the below code snippet?

```html
<script type="text/javascript">

amt=55+"55";

document.write(amt);

</script>
```

- A. Error, No Output.
- B. 5
- C. 110
- D. 5555

---

### Answer
**5555**

---

### Explanation

#### Why Correct Answer is Correct
When JavaScript encounters:

```javascript
55 + "55"
```

one operand is a string.

JavaScript converts the number into a string and performs string concatenation.

Result:

```javascript
"55" + "55"
```

becomes:

```javascript
"5555"
```

Important exam points:
- Number + String → String concatenation
- JavaScript performs implicit type conversion

---

#### Why Option A is Wrong
The code is valid.

---

#### Why Option B is Wrong
This value cannot result from the expression.

---

#### Why Option C is Wrong
Numeric addition would require both operands to be numbers.

---

#### Why Option D is Correct
String concatenation produces `5555`.

---