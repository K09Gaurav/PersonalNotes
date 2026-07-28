> [!info]
> **Module Objective**
> Learn how to use **Snowflake Notebooks** to organize SQL workflows and **Streamlit in Snowflake (SiS)** to build simple data-entry applications that insert data into Snowflake tables.

#accenture #snowflake #cognizant 

---

# Quick Revision

| Concept | Remember |
|----------|----------|
| Notebook | Interactive document for SQL and documentation |
| Markdown Cell | Documentation only |
| SQL Cell | Executes SQL |
| `SET` | Creates SQL variables |
| `$variable` | References SQL variables |
| Streamlit | Builds interactive Snowflake applications |
| `st.text_input()` | Text input field |
| `st.selectbox()` | Dropdown selection |
| Python Variables | Store user input |
| `if st.button()` | Executes code after button click |
| Indentation | Required in Python |
| Escape Character | `\` |
| `session.sql()` | Executes SQL from Python |
| Verification | Query the table after inserting data |

# Notebook vs Streamlit

| Notebook | Streamlit |
|-----------|-----------|
| SQL-focused workflow | Interactive application |
| Manual execution | User-friendly interface |
| Good for developers | Good for end users |
| Documentation + SQL | Forms + Python + SQL |

---

---

# 1. Alternative Ways to Work with Data

So far, data has been added using:

- `INSERT` statements
- Load Data Wizard

Snowflake also provides interactive tools for working with data:

- **Snowflake Notebooks**
- **Streamlit in Snowflake (SiS)**

These tools help automate repetitive tasks and create reusable workflows.

---

# 2. Snowflake Notebooks

## What is a Notebook?

A Notebook is an interactive workspace that combines:

- Documentation
- SQL
- Python (optional)
- Query results

Think of it as a document where code and explanations are stored together.
![Pasted image 20260704174948](../Images/Pasted%20image%2020260704174948.png)

---

## Typical Notebook Structure

```
Notebook

├── Markdown Cell
├── SQL Cell
├── SQL Cell
├── SQL Cell
└── Results
```

---

## Advantages

- Document workflows
- Execute SQL step by step
- Share processes with teammates
- Organize related SQL together

---

## Notebook Cells

### Markdown Cell

Used for documentation.

Examples:

- Notes
- Instructions
- Explanations
- Process documentation

No code is executed.

---

### SQL Cell

Used to execute SQL statements.

Examples:

```sql
SELECT *
FROM FLOWER_DETAILS;
```

or

```sql
INSERT INTO ...
```

Each SQL cell runs independently.

---

# 3. Creating a Table for Notebook Practice

The course creates a new table based on the existing `VEGETABLE_DETAILS` structure.

Destination table:

```
FLOWER_DETAILS
```

![Pasted image 20260704174839](../Images/Pasted%20image%2020260704174839.png)
![Pasted image 20260704174844](../Images/Pasted%20image%2020260704174844.png)
![Pasted image 20260704174852](../Images/Pasted%20image%2020260704174852.png)

---

# 4. Using SQL Cells

Example insert statement:

```sql
INSERT INTO GARDEN_PLANTS.FLOWERS.FLOWER_DETAILS
SELECT 'Petunia', 'M';
```

This inserts one row into the table.
![Pasted image 20260704175037](../Images/Pasted%20image%2020260704175037.png)

---

Next, create another SQL cell to verify the insertion.

```sql
SELECT *
FROM FLOWER_DETAILS;
```

---

## Typical Notebook Workflow

```
Markdown

↓

Insert Data

↓

Check Results
```

This makes the entire process easy to follow and repeat.

---

# 5. Notebook Variables

Variables allow values to be reused throughout the notebook.

Instead of hardcoding values multiple times, define them once and reference them later.

---

## Creating Variables

```sql
SET rdc = 'S';

SET fn = 'Lilac';
```
![Pasted image 20260704175122](../Images/Pasted%20image%2020260704175122.png)

---

## Reading Variables

Variables are referenced using the `$` symbol.

```sql
SELECT
    $fn,
    $rdc;
```

Result:

```
Lilac

S
```

---

## Why Use Variables?

Instead of:

```sql
INSERT INTO FLOWER_DETAILS
SELECT 'Lilac','S';
```

use:

```sql
INSERT INTO FLOWER_DETAILS
SELECT
    $fn,
    $rdc;
```
![Pasted image 20260704175215](../Images/Pasted%20image%2020260704175215.png)
Benefits:

- Easier maintenance
- Less repetitive code
- Reusable SQL

---

# 6. Notebook Organization

Notebook cells can be:

- Renamed
- Moved
- Reordered

A well-organized notebook improves readability.

Example order:

```
Markdown

↓

Set Variables

↓

Check Variables

↓

Insert Data

↓

Verify Results
```

---

# 7. Notebook Documentation

Markdown cells explain:

- What the notebook does
- Required steps
- Expected results
- Process documentation

![Pasted image 20260704175249](../Images/Pasted%20image%2020260704175249.png)

This makes notebooks useful for collaboration and knowledge sharing.

---

# 8. Practical Exercise

Additional flower records were inserted.

Examples:

| Flower | Root Depth |
|----------|------------|
| Sunflower | D |
| Lavender | S |
| Tulip | M |
![Pasted image 20260704175306](../Images/Pasted%20image%2020260704175306.png)
These rows are added using the same notebook workflow.

![Pasted image 20260704175321](../Images/Pasted%20image%2020260704175321.png)

---

# 9. Streamlit in Snowflake (SiS)

## What is Streamlit?

Streamlit in Snowflake allows developers to build interactive web applications directly inside Snowflake.

Instead of writing SQL manually, users interact with:

- Text boxes
- Buttons
- Drop-down menus
- Forms

---

## Typical Flow

```
User

↓

Form

↓

Python

↓

SQL

↓

Snowflake Database
```

---

# 10. Creating a Data Entry Form

A new table is created:

```
FRUIT_DETAILS
```

The Streamlit application acts as a data entry form for this table.

![Pasted image 20260704175400](../Images/Pasted%20image%2020260704175400.png)


![Pasted image 20260704175416](../Images/Pasted%20image%2020260704175416.png)
![Pasted image 20260704175508](../Images/Pasted%20image%2020260704175508.png)

After creation Delete Most of the Sample Code

On the code side of the screen, delete all code from line 18 to the end. Then click 'Run" in the upper left corner.

![Pasted image 20260704175531](../Images/Pasted%20image%2020260704175531.png)

---

# 11. Streamlit Input Widgets

## Text Input

```python
st.text_input("Fruit Name:")
```

Displays a textbox for entering a fruit name.

---

## Select Box

```python
st.selectbox(
    "Root Depth:",
    ("S","M","D")
)
```

Displays a dropdown list.

Possible choices:

- S
- M
- D
![Pasted image 20260704175735](../Images/Pasted%20image%2020260704175735.png)
---

# 12. Capturing User Input

The values entered by the user are stored in Python variables.

```python
fn = st.text_input("Fruit Name:")

rdc = st.selectbox(
    "Root Depth:",
    ("S","M","D")
)
```

Variables:

```
fn

↓

Fruit Name
```

```
rdc

↓

Root Depth Code
```

![Pasted image 20260704175824](../Images/Pasted%20image%2020260704175824.png)

---

# 13. Submit Button

A button triggers the processing of the form.

```python
if st.button("Submit"):
```

Everything inside the `if` block executes only after the button is clicked.

Example:

```python
if st.button('Submit'):
    st.write('Fruit Name entered is ' + fn)
    st.write('Root Depth Code chosen is ' + rdc)
```

![1083](../Images/Pasted%20image%2020260704175937.png)

---

# 14. Building SQL Dynamically

The form values are used to construct an SQL statement.

Example:

```python
sql_insert = (
    "insert into "
    "garden_plants.fruits.fruit_details "
    "select "
    + fn
    + ","
    + rdc
)

st.write(sql_insert)
```

![Pasted image 20260704180117](../Images/Pasted%20image%2020260704180117.png)

The SQL statement is assembled using:

- Strings
- Variables
- Concatenation (`+`)

---

# 16. Escape Characters

Sometimes quotation marks need to appear inside strings.

Example:

Incorrect:

```python
'Hello ma'am'
```

Python interprets the second apostrophe as the end of the string.

Correct:

```python
'Hello ma\'am'
```

The backslash (`\`) tells Python to treat the following quote as a literal character.

![Pasted image 20260704180200](../Images/Pasted%20image%2020260704180200.png)

## 🥋 Fix the Insert Statement
![Pasted image 20260704180245](../Images/Pasted%20image%2020260704180245.png)

---

## Escape Character

Python uses:

```
\
```

to escape special characters.

---

# 17. Executing SQL from Python

![Pasted image 20260704180403](../Images/Pasted%20image%2020260704180403.png)

After building the SQL statement:

```python
result = session.sql(sql_insert)
```

This sends the SQL statement to Snowflake.

The result can be displayed:

```python
st.write(result)
```

![Pasted image 20260704180345](../Images/Pasted%20image%2020260704180345.png)

---

## Overall Flow

```
User enters data

↓

Python variables

↓

SQL statement

↓

session.sql()

↓

Snowflake

↓

Row inserted
```

---

# 18. Verifying the Insert

After submitting the form:

```sql
SELECT *
FROM FRUIT_DETAILS;
```

Verify that the row has been added.

The exercise then repeats the process until three fruit records exist.

---

# Key Takeaways

- Snowflake Notebooks combine documentation and executable SQL.
- Notebooks support Markdown and SQL cells.
- SQL variables can be created using `SET`.
- Variables are referenced using the `$` symbol.
- Streamlit in Snowflake enables interactive applications inside Snowflake.
- User input is collected through widgets like `text_input()` and `selectbox()`.
- Form values are stored in Python variables.
- Python uses indentation to define code blocks.
- SQL statements can be dynamically constructed using Python strings and variables.
- Escape characters (`\`) allow quotation marks to appear inside strings.
- `session.sql()` executes SQL generated by the Streamlit application.
- Always verify inserted data by querying the destination table.

---

