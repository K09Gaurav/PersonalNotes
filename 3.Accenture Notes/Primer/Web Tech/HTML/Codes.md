#webTech #accenture #quiz #html

# q1

## Question
Create a webpage for **KentPedia Online** to publish an article on **"Online Education"** using HTML5 semantic elements.

### Requirements

#### Header

- Create a `<header>` element with id `head`.
- Inside it, create:
  - `<h1 id="heading1">Online Education</h1>`

#### Main Content

- Create a `<div>` with id `content`.
- Everything except header and footer must be inside this div.

##### First Element in Div

- Create:
  ```html
  <h2 id="heading2">Future of Education</h2>
  ```

##### Second Element in Div

- Create an article:
  ```html
  <article id="art1">
  ```
- Inside it:
  - `<h3 id="intro">Introduction</h3>`
  - A paragraph containing Introduction content.
- After the paragraph:
  - Create an aside:
    ```html
    <aside id="side">
    ```
  - Place aside content inside a paragraph.

##### Third Element in Div

- Create:
  ```html
  <article id="art2">
  ```
- Inside it:
  - `<h3 id="overview">Why Online Education</h3>`
  - A paragraph containing the related content.

##### Fourth Element in Div

- Create:
  ```html
  <article id="art3">
  ```
- Inside it:
  - `<h3 id="reason">Reasons</h3>`
  - A paragraph containing the related content.

#### Footer

- Create a `<footer>` element with id `foot`.
- Inside it create:
  ```html
  <p id="status">Last update Apr 4,2019.</p>
  ```

---

## Solution

```html
<header id="head">
    <h1 id="heading1">Online Education</h1>
</header>

<div id="content">

    <h2 id="heading2">Future of Education</h2>

    <article id="art1">
        <h3 id="intro">Introduction</h3>
        <p>Introduction text.</p>

        <aside id="side">
            <p>Aside text.</p>
        </aside>
    </article>

    <article id="art2">
        <h3 id="overview">Why Online Education</h3>
        <p>Why Online Education text.</p>
    </article>

    <article id="art3">
        <h3 id="reason">Reasons</h3>
        <p>Reasons text.</p>
    </article>

</div>

<footer id="foot">
    <p id="status">Last update Apr 4,2019.</p>
</footer>
```


---
---


# q2

## Question Summary

Create a split-screen Table of Contents page.

### Left Side

Create an unordered list containing 6 links.

| Anchor ID | href |
|------------|---------|
| link1 | overview |
| link2 | syntax |
| link3 | attributes |
| link4 | events |
| link5 | forms |
| link6 | advd |

Requirements:

- UL id = `links`
- `list-style-type:none`
- Each link must be inside:
```html
<li>
    <a href="" id="">
        <p>Topic</p>
    </a>
</li>
```

---

### Right Side

Create a header:

```html
<header>
    <h2>TABLE OF CONTENTS</h2>
</header>
```

Create an ordered list containing:

1. HTML5 OVERVIEW
2. HTML5 SYNTAX
3. HTML5 ATTRIBUTES
4. HTML5 EVENTS
5. HTML5 WEB FORMS 2.0
6. HTML5 AUDIO & VIDEO

---

### IDs for Paragraphs

| Topic | Paragraph ID |
|---------|---------|
| HTML5 OVERVIEW | overview |
| HTML5 SYNTAX | syntax |
| HTML5 ATTRIBUTES | attributes |
| HTML5 EVENTS | events |
| HTML5 WEB FORMS 2.0 | forms |
| HTML5 AUDIO & VIDEO | advd |

Example:

```html
<li>
    <p id="overview">HTML5 OVERVIEW</p>

    <ul>
        <li><p>Subtopic 1</p></li>
        <li><p>Subtopic 2</p></li>
    </ul>

</li>
```

---
## Solution

```html
<!DOCTYPE html>
<html>
<head>
<title>Table of Contents</title>
<style>
*{
    font-weight:bold;
}
h2{
    text-align:center;
    color:#000000;
}
.split {
    height: 100%;
    width: 50%;
    position: fixed;
    overflow: scroll;
    z-index: 1;
    top: 0;
}
.left {
    left: 0;
    background-color: #000000;
}
.right {
    right: 0;
    background-color: #808080;
    color:#000000;
    width: 70%;
}
a{
    text-decoration:none;
    color:#808080;
}
</style>
</head>

<body>

<div class="split left">

    <ul id="links" style="list-style-type:none;">
        <li><a href="#overview" id="link1"><p>HTML5 OVERVIEW</p></a></li>
        <li><a href="#syntax" id="link2"><p>HTML5 SYNTAX</p></a></li>
        <li><a href="#attributes" id="link3"><p>HTML5 ATTRIBUTES</p></a></li>
        <li><a href="#events" id="link4"><p>HTML5 EVENTS</p></a></li>
        <li><a href="#forms" id="link5"><p>HTML5 WEB FORMS 2.0</p></a></li>
        <li><a href="#advd" id="link6"><p>HTML5 AUDIO & VIDEO</p></a></li>
    </ul>

</div>

<div class="split right">

    <header id="head">
        <h2 id="heading">TABLE OF CONTENTS</h2>
    </header>

    <ol>

        <li>
            <p id="overview">HTML5 OVERVIEW</p>
            <ul>
                <li><p>Introduction to HTML5</p></li>
                <li><p>Features of HTML5</p></li>
            </ul>
        </li>

        <li>
            <p id="syntax">HTML5 SYNTAX</p>
            <ul>
                <li><p>Document Structure</p></li>
                <li><p>Basic Tags</p></li>
            </ul>
        </li>

        <li>
            <p id="attributes">HTML5 ATTRIBUTES</p>
            <ul>
                <li><p>Global Attributes</p></li>
                <li><p>Custom Attributes</p></li>
            </ul>
        </li>

        <li>
            <p id="events">HTML5 EVENTS</p>
            <ul>
                <li><p>Mouse Events</p></li>
                <li><p>Keyboard Events</p></li>
            </ul>
        </li>

        <li>
            <p id="forms">HTML5 WEB FORMS 2.0</p>
            <ul>
                <li><p>Input Types</p></li>
                <li><p>Form Validation</p></li>
            </ul>
        </li>

        <li>
            <p id="advd">HTML5 AUDIO & VIDEO</p>
            <ul>
                <li><p>Audio Element</p></li>
                <li><p>Video Element</p></li>
            </ul>
        </li>

    </ol>

</div>

</body>
</html>
```

---
---
# q3
## Question Summary

Create a Chess Board using an HTML table.

### Table IDs

| Element | ID |
|----------|----------|
| Caption | table_caption |
| TBody | table_body |
| TFoot | table_footer |

Caption Text:

```html
CHESS-MASTER
```

---

## Chess Board Naming Convention

### Rank 8

| Square | ID |
|----------|----------|
| a8 | QR8 |
| b8 | QN8 |
| c8 | QB8 |
| d8 | Q8 |
| e8 | K8 |
| f8 | KB8 |
| g8 | KN8 |
| h8 | KR8 |

---

### Rank 7

| Square | ID |
|----------|----------|
| a7 | QR7 |
| b7 | QN7 |
| c7 | QB7 |
| d7 | Q7 |
| e7 | K7 |
| f7 | KB7 |
| g7 | KN7 |
| h7 | KR7 |

Pattern continues similarly down to Rank 1.

---

## Piece Titles

### Black Pieces (Rank 8)

| ID | Title |
|------|------|
| QR8 | Black Rook |
| QN8 | Black Knight |
| QB8 | Black Bishop |
| Q8 | Black Queen |
| K8 | Black King |
| KB8 | Black Bishop |
| KN8 | Black Knight |
| KR8 | Black Rook |

---

### Black Pawns (Rank 7)

All squares:

```html
title="Black Pawn"
```

---

### White Pawns (Rank 2)

All squares:

```html
title="White Pawn"
```

---

### White Pieces (Rank 1)

| ID | Title |
|------|------|
| QR1 | White Rook |
| QN1 | White Knight |
| QB1 | White Bishop |
| Q1 | White Queen |
| K1 | White King |
| KB1 | White Bishop |
| KN1 | White Knight |
| KR1 | White Rook |

---

## Square Color Pattern

### Odd Ranks (8,6,4,2)

```html
white black white black
white black white black
```

Example:

```html
<td class="white_square"></td>
<td class="black_square"></td>
```

---

### Even Ranks (7,5,3,1)

```html
black white black white
black white black white
```

Example:

```html
<td class="black_square"></td>
<td class="white_square"></td>
```

---

## Footer Buttons

| ID | Value |
|----------|----------|
| setup | SetUpBoard |
| online | PlayOnline |
| computer | PlayComputer |
| withdraw | Withdraw |

Example:

```html
<input type="button" id="setup" value="SetUpBoard">
```

---

## TFoot Structure

```html
<tfoot id="table_footer">
    <tr>
        <td>
            4 buttons here
        </td>
    </tr>
</tfoot>
```

---

## Frequently Tested Points

1. Caption ID must be `table_caption`
2. TBody ID must be `table_body`
3. TFoot ID must be `table_footer`
4. Rank 8 = Black major pieces
5. Rank 7 = Black pawns
6. Rank 2 = White pawns
7. Rank 1 = White major pieces
8. Alternate square colors every row
9. Buttons must be inside a single TD in TFoot
10. Use exact IDs given in the question

---
---

# q4

## Employee Basic Information Form

### Question Summary

Create an Employee Basic Information form using HTML5.

The form contains 3 fieldsets:

1. Personal Information
2. Current Position
3. Previous Employment

Each fieldset must contain a table for alignment.

---

### Fieldset IDs

| Fieldset | ID | Legend ID |
|-----------|-----------|-----------|
| Personal Information | personal | personallegend |
| Current Position | current | currentlegend |
| Previous Employment | previous | previouslegend |

---

### Input Fields

| Label | ID | Type | Required |
|---------|---------|---------|---------|
| Employee Name | employeename | text | Yes |
| Employee Id | employeeid | text | Yes |
| Aadhar Number | aadharnumber | text | Yes |
| Enter Email | email | text | Yes |
| Department | department | text | Yes |
| Designation | designation | text | Yes |
| Location | location | text | Yes |
| Employer | employer | text | Yes |
| Employer Designation | employerdesignation | text | Yes |

---

### Placeholders

#### Employee Name

```html
placeholder="Enter the employee name"
```

#### Employee Id

```html
placeholder="Enter the employee id"
```

#### Aadhar Number

```html
placeholder="Enter the aadhar number"
```

#### Email

```html
placeholder="Enter the email"
```

---

### Aadhar Pattern

Format:

```text
3214-5167-1092
```

Pattern:

```html
pattern="[0-9]{4}-[0-9]{4}-[0-9]{4}"
```

---

### Submit Button

| ID | Type | Value |
|---------|---------|---------|
| submit | submit | Save & continue |

```html
<input type="submit" id="submit" value="Save & continue">
```

---

## Complete Solution

```html
<form>

    <fieldset id="personal">
        <legend id="personallegend">Personal Information</legend>

        <table>
            <tr>
                <td><label for="employeename">Employee Name</label></td>
                <td>
                    <input type="text" id="employeename"
                           placeholder="Enter the employee name" required>
                </td>
            </tr>

            <tr>
                <td><label for="employeeid">Employee Id</label></td>
                <td>
                    <input type="text" id="employeeid"
                           placeholder="Enter the employee id" required>
                </td>
            </tr>

            <tr>
                <td><label for="aadharnumber">Aadhar Number</label></td>
                <td>
                    <input type="text" id="aadharnumber"
                           placeholder="Enter the aadhar number"
                           pattern="[0-9]{4}-[0-9]{4}-[0-9]{4}"
                           required>
                </td>
            </tr>

            <tr>
                <td><label for="email">Enter Email</label></td>
                <td>
                    <input type="text" id="email"
                           placeholder="Enter the email" required>
                </td>
            </tr>
        </table>

    </fieldset>

    <fieldset id="current">
        <legend id="currentlegend">Current Position</legend>

        <table>
            <tr>
                <td><label for="department">Department</label></td>
                <td><input type="text" id="department" required></td>
            </tr>

            <tr>
                <td><label for="designation">Designation</label></td>
                <td><input type="text" id="designation" required></td>
            </tr>

            <tr>
                <td><label for="location">Location</label></td>
                <td><input type="text" id="location" required></td>
            </tr>
        </table>

    </fieldset>

    <fieldset id="previous">
        <legend id="previouslegend">Previous Employment</legend>

        <table>
            <tr>
                <td><label for="employer">Employer</label></td>
                <td><input type="text" id="employer" required></td>
            </tr>

            <tr>
                <td><label for="employerdesignation">Employer Designation</label></td>
                <td><input type="text" id="employerdesignation" required></td>
            </tr>
        </table>

    </fieldset>

    <input type="submit" id="submit" value="Save & continue">

</form>
```

---

### Quick Revision

#### Required IDs

```text
personal
personallegend

current
currentlegend

previous
previouslegend

employeename
employeeid
aadharnumber
email
department
designation
location
employer
employerdesignation

submit
```

#### Special Requirement

```html
pattern="[0-9]{4}-[0-9]{4}-[0-9]{4}"
```

Used only for:

```text
Aadhar Number
```


---
---
# q5
## Forever Event Management - Vendor Registration Form

### Question Summary

Create a Vendor Registration Form for Forever Event Management.

The form contains:

1. Company Information
2. Vendor Type
3. Contact Details
4. TIN Details
5. Project Cost Slider
6. File Upload
7. Submit & Reset Buttons

---

## Important IDs

### Figure

| Element | ID |
|----------|----------|
| Figure | forever_image |
| Image | image1 |

Example:

```html
<figure id="forever_image">
    <img id="image1" src="forever.jpg">
</figure>
```

---

### Table

| Element | ID |
|----------|----------|
| Caption | table_caption |

Caption Text:

```text
Vendor Registeration Form
```

---

## Input Fields

| Label | ID | Type |
|---------|---------|---------|
| Company Name | cname | text |
| Phone Number | phno | tel |
| Email ID | email | email |
| Location | address | textarea |
| Website Address | link | url |
| TIN No | tin | number |
| TIN Expiry | expiry | date |
| Average Project Cost | cost | range |
| Upload Images | profile | file |

All are mandatory.

---

## Radio Buttons

Name must be:

```html
name="ctype"
```

IDs:

```text
corporation
partnership
individual
others
```

Example:

```html
<input type="radio" id="corporation" name="ctype">
```

---

## Phone Number Validation

Must:

- Start with 7, 8, or 9
- Have exactly 10 digits

Pattern:

```html
pattern="[789][0-9]{9}"
```

---

## Location Text Area

```html
<textarea
    id="address"
    rows="4"
    cols="50"
    required>
</textarea>
```

---

## Project Cost Slider

| Attribute | Value |
|------------|------------|
| min | 25000 |
| max | 500000 |
| step | 1000 |

Must include:

```html
onchange="show_value(this.value);"
```

Example:

```html
<input type="range"
       id="cost"
       min="25000"
       max="500000"
       step="1000"
       onchange="show_value(this.value);">
```

---

## File Upload

Requirements:

- Accept files
- Multiple files allowed
- Mandatory

```html
<input type="file"
       id="profile"
       multiple
       required>
```

---

## Footer Buttons

| ID | Type | Value |
|---------|---------|---------|
| submit | submit | REGISTER |
| reset | reset | CLEAR |

Example:

```html
<div id="foot">
    <input type="submit" id="submit" value="REGISTER">
    <input type="reset" id="reset" value="CLEAR">
</div>
```

---

## Complete Solution

```html
<figure id="forever_image">
    <img id="image1" src="forever.jpg" height="80" width="200" alt="bg_image">
</figure>

<table>

    <caption id="table_caption">Vendor Registeration Form</caption>

    <tr>
        <td>Company Name</td>
        <td><input type="text" id="cname" required></td>
    </tr>

    <tr>
        <td>Type</td>
        <td>
            <input type="radio" id="corporation" name="ctype">Corporation
            <input type="radio" id="partnership" name="ctype">Partnership
            <input type="radio" id="individual" name="ctype">Individual
            <input type="radio" id="others" name="ctype">Others
        </td>
    </tr>

    <tr>
        <td>Phone Number</td>
        <td>
            <input type="tel" id="phno"
                   pattern="[789][0-9]{9}"
                   required>
        </td>
    </tr>

    <tr>
        <td>Email ID</td>
        <td><input type="email" id="email" required></td>
    </tr>

    <tr>
        <td>Location</td>
        <td>
            <textarea id="address"
                      rows="4"
                      cols="50"
                      required></textarea>
        </td>
    </tr>

    <tr>
        <td>Website Address</td>
        <td><input type="url" id="link" required></td>
    </tr>

    <tr>
        <td>TIN No</td>
        <td><input type="number" id="tin" required></td>
    </tr>

    <tr>
        <td>TIN No Expiry Date</td>
        <td><input type="date" id="expiry" required></td>
    </tr>

    <tr>
        <td>Average Project Cost</td>
        <td>
            <input type="range"
                   id="cost"
                   min="25000"
                   max="500000"
                   step="1000"
                   onchange="show_value(this.value);"
                   required>
            <span id="demo"></span>
        </td>
    </tr>

    <tr>
        <td>Upload Images of Licence, PAN & Facade</td>
        <td>
            <input type="file"
                   id="profile"
                   multiple
                   required>
        </td>
    </tr>

</table>

<div id="foot">
    <input type="submit" id="submit" value="REGISTER">
    <input type="reset" id="reset" value="CLEAR">
</div>
```

---

## Quick Revision

#### Figure IDs

```text
forever_image
image1
```

#### Table Caption ID

```text
table_caption
```

#### Radio IDs

```text
corporation
partnership
individual
others
```

#### Special Validations

```html
pattern="[789][0-9]{9}"
```

```html
<textarea rows="4" cols="50">
```

```html
multiple
```

```html
onchange="show_value(this.value);"
```

#### Footer

```html
REGISTER
CLEAR
```

---
---
# q6