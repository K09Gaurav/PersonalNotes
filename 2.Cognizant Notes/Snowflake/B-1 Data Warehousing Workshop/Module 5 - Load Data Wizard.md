
> [!info]
> **Module Objective**
> Learn how to efficiently load data from external files into Snowflake tables using the **Load Data Wizard**, understand CSV file formats, customize file parsing options, and perform basic data validation and cleanup.

#accenture #cognizant #snowflake 

---

# Quick Revision

| Concept | Remember |
|----------|----------|
| Load Data Wizard | GUI tool for bulk data loading |
| CSV | Comma-Separated Values |
| Plain Text Editor | Best way to inspect file formatting |
| Destination Table | Must exist before loading data |
| File Delimiter | Can be `,`, \| , tab, `;`, etc. |
| File Preview | Verify parsing before loading |
| TRUNCATE | Removes all rows, keeps table |
| DELETE | Removes selected rows |
| Data Validation | Check row count and duplicates after loading |
| Expected Final Row Count | 41 rows (after removing the incorrect duplicate) |

---

# 1. Why Use the Load Data Wizard?

## Problem with INSERT Statements

Using `INSERT` statements is practical for adding a few rows.

Example:

```sql
INSERT INTO ROOT_DEPTH
VALUES (...);
```

However, manually writing hundreds or thousands of INSERT statements quickly becomes impractical.

Instead, Snowflake provides the **Load Data Wizard** for bulk data loading.

---

## Advantages of the Load Data Wizard

- Loads many rows at once
- Faster than manual INSERT statements
- Supports multiple file formats
- Provides file parsing options
- Simple graphical interface

---

# 2. CSV Files

## What is a CSV File?

CSV stands for:

> **Comma-Separated Values**

Each row represents one record.

Each value is separated by a delimiter.

Example:

```text
Carrot,S
Spinach,S
Potato,D
```

Internally, commas separate the columns.

![Pasted image 20260704161403](../Images/Pasted%20image%2020260704161403.png)


---

## Viewing CSV Files

Do **not** rely on Excel or Google Sheets when inspecting file formatting.

Spreadsheet software automatically hides delimiters.

Instead, open the file using a plain text editor such as:

- Notepad (Windows)
- TextEdit (Mac)
- VS Code
- Notepad++

This allows you to verify:

- Column delimiter
- Row delimiter
- Quotation marks
- File formatting

> [!tip]
> Always inspect raw data files with a text editor before loading them into Snowflake. Different files may use different delimiters.

---

# 3. Creating the Target Table

Before loading data, create a destination table.

```sql
CREATE TABLE GARDEN_PLANTS.VEGGIES.VEGETABLE_DETAILS
(
    PLANT_NAME VARCHAR(25),
    ROOT_DEPTH_CODE VARCHAR(1)
);
```
![Pasted image 20260704161427](../Images/Pasted%20image%2020260704161427.png)

---

## Table Structure

| Column | Data Type | Purpose |
|----------|-----------|----------|
| PLANT_NAME | VARCHAR(25) | Vegetable name |
| ROOT_DEPTH_CODE | VARCHAR(1) | Root depth category |

---

# 4. Loading Data (File 1)

The first data file contains vegetables from **A to K**.

Example format:

```text
Arugula,S
Beet,D
Carrot,D
...
```

Delimiter used:

```
,
```

(comma)

---

## Load Process

Using the Load Data Wizard:

1. Select the destination table.
2. Upload the CSV file.
3. Confirm delimiter settings.
4. Preview the parsed data.
5. Load the file into the table.

![Pasted image 20260704161514](../Images/Pasted%20image%2020260704161514.png)
![Pasted image 20260704161521](../Images/Pasted%20image%2020260704161521.png)
![Pasted image 20260704161530](../Images/Pasted%20image%2020260704161530.png)
![Pasted image 20260704161536](../Images/Pasted%20image%2020260704161536.png)
![Pasted image 20260704161541](../Images/Pasted%20image%2020260704161541.png)
![Pasted image 20260704161546](../Images/Pasted%20image%2020260704161546.png)
![Pasted image 20260704161550](../Images/Pasted%20image%2020260704161550.png)

---

## Result

The table now contains the rows from the first file.

---

# 5. Loading Data (File 2)

The second file contains vegetables from **K to Z**.

Unlike the first file, this file uses a different delimiter.

Example:

```text
Kale|M
Lettuce|S
Onion|M
```

Delimiter:

```
|
```

(pipe)

![Pasted image 20260704161629](../Images/Pasted%20image%2020260704161629.png)

---

## Important Difference

The data itself is similar.

Only the delimiter has changed.

Before loading the second file, update the file format settings in the wizard.
![Pasted image 20260704161656](../Images/Pasted%20image%2020260704161656.png)

---

## Delimiter Comparison

### File 1

```text
Carrot,S
```

Delimiter:

```
,
```

---

### File 2

```text
Carrot|S
```

Delimiter:

```
|
```

---

## Lesson

Never assume all data files use commas.

Different systems may export files using:

- Commas `,`
- Pipes `|`
- Tabs
- Semicolons `;`
- Other delimiters

Always verify the file format before loading.

---

## Final Result

After loading both files:

```
VEGETABLE_DETAILS

42 Rows
```
![Pasted image 20260704161725](../Images/Pasted%20image%2020260704161725.png)
Running:

```sql
SELECT *
FROM VEGETABLE_DETAILS;
```

should display vegetables from **A through Z**.

Sorting in descending order should place:

```
Zucchini
```

near the top, confirming that the second file loaded successfully.

---

# 6. Reloading Data

If the same file is accidentally loaded multiple times, duplicate rows may appear.

Instead of deleting every row manually, use:

```sql
TRUNCATE TABLE GARDEN_PLANTS.VEGGIES.VEGETABLE_DETAILS;
```

---

## TRUNCATE

Purpose:

- Deletes all rows
- Preserves the table structure
- Allows data to be loaded again

---

# 7. Viewing Loaded Data

After loading data:

```sql
SELECT *
FROM VEGETABLE_DETAILS;
```

Verify:

- Data loaded correctly
- Correct number of rows
- No unexpected values

---

# 8. Detecting Duplicate Records

During inspection, one vegetable appears twice.
![Pasted image 20260704161826](../Images/Pasted%20image%2020260704161826.png)

Example:
```
Spinach   S
Spinach   D
```

Only one of these rows is correct.

---

## Investigating the Duplicate

Instead of deleting blindly, first isolate the incorrect record.

Example concept:

```sql
SELECT *
FROM VEGETABLE_DETAILS
WHERE PLANT_NAME = 'Spinach';
```

This displays only the duplicate entries.

![Pasted image 20260704161841](../Images/Pasted%20image%2020260704161841.png)


---

# 9. Removing Incorrect Data

After identifying the incorrect row, delete only that specific record.

Example concept:

```sql
DELETE
FROM VEGETABLE_DETAILS
WHERE PLANT_NAME = 'Spinach'
AND ROOT_DEPTH_CODE = 'D';
```

This removes only the incorrect duplicate while preserving the valid row.
![Pasted image 20260704161942](../Images/Pasted%20image%2020260704161942.png)
![Pasted image 20260704161954](../Images/Pasted%20image%2020260704161954.png)

---

# 10. Validating the Data

After deleting the incorrect row:

Run another query to verify the results.

Expected outcome:

- No duplicate vegetable names
- Only one Spinach row remains
- Total row count becomes:

```
41 Rows
```

![Pasted image 20260704162016](../Images/Pasted%20image%2020260704162016.png)

---

# Data Loading Workflow

```text
CSV File
      │
      ▼
Inspect File Format
(Text Editor)
      │
      ▼
Create Destination Table
      │
      ▼
Open Load Data Wizard
      │
      ▼
Configure File Format
      │
      ▼
Preview Data
      │
      ▼
Load into Table
      │
      ▼
Validate Data
      │
      ▼
Clean Incorrect Records
```

---

# Commands Learned

## Create Table

```sql
CREATE TABLE ...
```

Creates a destination table.

---

## Select

```sql
SELECT *
FROM VEGETABLE_DETAILS;
```

Displays table contents.

---

## Delete

```sql
DELETE
FROM VEGETABLE_DETAILS
WHERE ...
```

Removes selected rows.

---

## Truncate

```sql
TRUNCATE TABLE VEGETABLE_DETAILS;
```

Removes all rows while preserving the table structure.

---

# Key Takeaways

- The Load Data Wizard is preferred over manual INSERT statements for bulk data loading.
- CSV stands for **Comma-Separated Values**, but files may use other delimiters.
- Always inspect data files using a plain text editor to verify the delimiter and file format.
- Create the destination table before loading data.
- Configure the correct delimiter when using the Load Data Wizard.
- Different files can use different delimiters (e.g., `,` or `|`).
- Use `TRUNCATE` to quickly remove all rows before reloading data.
- Validate loaded data by checking row counts and identifying duplicates.
- Use `DELETE` with a `WHERE` clause to remove only incorrect records.

