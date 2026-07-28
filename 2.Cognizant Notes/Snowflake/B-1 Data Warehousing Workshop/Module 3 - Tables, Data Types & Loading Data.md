> [!info]
> **Module Objective**
> Learn how to create tables using SQL, choose appropriate data types, insert data, preview tables, and retrieve data using basic SQL queries.

#accenture #snowflake #cognizant 

---

# Quick Revision

| Concept                    | Remember                                       |
| -------------------------- | ---------------------------------------------- |
| SQL                        | Structured Query Language                      |
| Common Pronunciations      | SQL, SeQueL                                    |
| Data Modeling              | Designing the database structure               |
| Normalization              | Organizing data to reduce redundancy           |
| NUMBER                     | Numeric values                                 |
| TEXT / VARCHAR             | Character data                                 |
| CREATE OR REPLACE          | Creates or replaces a table                    |
| INSERT                     | Adds rows                                      |
| SELECT *                   | Returns all columns                            |
| LIMIT                      | Restricts returned rows                        |
| UPDATE                     | Modifies rows                                  |
| DELETE                     | Removes selected rows                          |
| TRUNCATE                   | Deletes all rows, keeps the table              |
| First Troubleshooting Step | Verify Role, Database, Schema, and Object Name |

---

# 1. Introduction to SQL

## Scenario

Uncle Yer now has:

```
GARDEN_PLANTS
├── VEGGIES
├── FRUITS
└── FLOWERS
```

The next step is to create **tables** inside these schemas and load spreadsheet data into them.

To accomplish this, Tsai introduces **SQL**.

---

## What is SQL?

**SQL** stands for:

> **Structured Query Language**

It is the standard language used to communicate with relational databases.

Common pronunciations:

- SQL (S.Q.L.)
- SeQueL (Sequel)

Both pronunciations are widely accepted.

---

## What SQL Can Do

SQL is used to:

- Create databases
- Create schemas
- Create tables
- Insert data
- Query data
- Update data
- Delete data
- Manage database objects

---

# 2. Preparing Data for a Database

Before importing spreadsheet data into a database, Tsai restructures the data.

This process follows two important concepts.

## Data Modeling

Data Modeling is the process of designing how data should be organized.

It involves deciding:

- Tables
- Columns
- Relationships
- Keys
- Data types

---

## Normalization

Normalization is the process of organizing data to reduce redundancy and improve consistency.

Typical improvements include:

- Removing duplicate information
- Splitting data into logical columns
- Creating unique identifiers
- Improving storage efficiency

---

## Example Transformation

Original Spreadsheet

| Root Depth | Measurement |
|------------|-------------|
| Shallow | 12-18 inches |

Improved Database Design

| ID | Code | Name | Unit | Min | Max |
|----|------|------|------|-----|-----|
| 1 | S | Shallow | cm | 30 | 45 |

Changes made:

- Added a unique ID
- Added a short code
- Split measurements into Min and Max
- Converted inches to centimeters

---

# 3. Choosing Data Types

Every table column requires an appropriate data type.

The ROOT_DEPTH table uses two primary data types.

---

## NUMBER

Stores numeric values.

Examples:

```text
1
30
45
100
```

Used for:

- IDs
- Measurements
- Counts
- Numeric calculations

Example:

```sql
NUMBER(2)
```

Meaning:

- Up to 2 digits

---

## TEXT (VARCHAR)

Stores characters and strings.

Examples:

```text
S
Shallow
cm
```

Snowflake internally converts `TEXT` into `VARCHAR`.

Example:

```sql
TEXT(7)
```

becomes

```sql
VARCHAR(7)
```

---

# 4. Creating the ROOT_DEPTH Table

## Table Structure


SQL:

```sql
CREATE OR REPLACE TABLE ROOT_DEPTH (
    ROOT_DEPTH_ID NUMBER(1),
    ROOT_DEPTH_CODE TEXT(1),
    ROOT_DEPTH_NAME TEXT(7),
    UNIT_OF_MEASURE TEXT(2),
    RANGE_MIN NUMBER(2),
    RANGE_MAX NUMBER(2)
);
```

![Pasted image 20260704154036](../Images/Pasted%20image%2020260704154036.png)

---

## Understanding the Columns

| Column | Purpose | Data Type |
|---------|----------|-----------|
| ROOT_DEPTH_ID | Unique identifier | NUMBER(1) |
| ROOT_DEPTH_CODE | Short code | TEXT(1) |
| ROOT_DEPTH_NAME | Category name | TEXT(7) |
| UNIT_OF_MEASURE | Measurement unit | TEXT(2) |
| RANGE_MIN | Minimum depth | NUMBER(2) |
| RANGE_MAX | Maximum depth | NUMBER(2) |
![Pasted image 20260704154010](../Images/Pasted%20image%2020260704154010.png)

---

## CREATE OR REPLACE

```sql
CREATE OR REPLACE TABLE
```

Meaning:

- Create the table if it doesn't exist.
- Replace the existing table if it already exists.

Useful during development when repeatedly modifying table structures.

> [!warning]
> Replacing a table deletes its existing data.

---

# 5. Finding the Table

After creating the table:

- Refresh Database Explorer.
- Search for the table.
- Use Object Picker.
- Use `SHOW TABLES`.
![Pasted image 20260704154131](../Images/Pasted%20image%2020260704154131.png)
![Pasted image 20260704154242](../Images/Pasted%20image%2020260704154242.png)

If the table isn't visible:

- Refresh the explorer.
- Verify Role.
- Verify Database.
- Verify Schema.
- Run metadata commands.
![Pasted image 20260704154151](../Images/Pasted%20image%2020260704154151.png)

---

## If Something Went Wrong

Possible fixes:

- Rename the table.
- Transfer ownership.
- Move it to the correct schema.
- Verify worksheet context.
![Pasted image 20260704154210](../Images/Pasted%20image%2020260704154210.png)
Most issues are caused by incorrect context rather than SQL syntax.

---

# 6. Snowflake SQL Adjustments

After creating the table, Snowflake may automatically modify the stored SQL definition.

Common changes include:

### TEXT → VARCHAR

Example:

```sql
TEXT(7)
```

becomes

```sql
VARCHAR(7)
```

---

### NUMBER Precision

Example:

```sql
NUMBER(2)
```

may appear internally as:

```sql
NUMBER(2,0)
```

The extra `0` represents the number of decimal places.

---

## Why?

Snowflake stores SQL using its internal standardized representation.

The table remains functionally identical.

---

# 7. Inserting Data

Once the table exists, rows can be inserted.

Example:

```sql
INSERT INTO ROOT_DEPTH
VALUES
(
    1,
    'S',
    'Shallow',
    'cm',
    30,
    45
);
```

This inserts one complete row.
![Pasted image 20260704154356](../Images/Pasted%20image%2020260704154356.png)

---

## Ways to Load Data

Throughout the course, data will be loaded using:

1. `INSERT`
2. Load Data Wizard
3. `COPY INTO`

INSERT is the simplest method and is best for small amounts of data.

---

# 8. Previewing Table Data

Before inserting data:

```
ROOT_DEPTH
Rows = 0
```

After insertion:

```
ROOT_DEPTH
Rows = 1
```

Table Preview lets you quickly inspect the contents without writing SQL.

![Pasted image 20260704154331](../Images/Pasted%20image%2020260704154331.png)

---

# 9. "Does Not Exist" Errors

One of the most common Snowflake errors is:
![Pasted image 20260704154422](../Images/Pasted%20image%2020260704154422.png)

```
Object does not exist
```

or

```
Object does not exist or not authorized
```

This usually means one of the following:

- Wrong Role
- Wrong Database
- Wrong Schema
- Wrong Object Name
- Missing permissions

---

## Troubleshooting Checklist

Ask yourself:

- Am I using the correct Role?
- Am I connected to the correct Database?
- Am I using the correct Schema?
- Does this object exist?
- Does my Role have permission?

If necessary:

- Change Role.
- Change worksheet context.
- Fully qualify the object name.
- Transfer ownership.

---

# 10. Querying Data

## SELECT *

```sql
SELECT *
FROM ROOT_DEPTH;
```

The `*` (asterisk) means:

> Return **all columns**.

Example:

```
ID
CODE
NAME
UNIT
MIN
MAX
```

Without `*`, every column would have to be listed individually.

---

## LIMIT

Sometimes tables contain millions of rows.

Instead of retrieving everything, use:

```sql
SELECT *
FROM ROOT_DEPTH
LIMIT 1;
```

This returns only the first row.

---

## Why Use LIMIT?

Benefits:

- Faster execution
- Lower compute usage
- Easier debugging
- Safer exploration of large tables

---

## SELECT * vs LIMIT

| Statement | Result |
|------------|---------|
| `SELECT *` | All columns, all rows |
| `SELECT * LIMIT 5` | All columns, first 5 rows |

---

# 11. Adding Multiple Rows

Additional rows can be inserted individually or together.

Example:

```sql
INSERT INTO ROOT_DEPTH
VALUES
(2,'M','Medium','cm',46,60),
(3,'D','Deep','cm',61,90);
```

After insertion:

```
ROOT_DEPTH

1  Shallow
2  Medium
3  Deep
```
![Pasted image 20260704154521](../Images/Pasted%20image%2020260704154521.png)
---

# 12. Other Useful SQL Commands

## DELETE

Removes selected rows.

```sql
DELETE FROM ROOT_DEPTH
WHERE ROOT_DEPTH_ID = 9;
```

Only matching rows are removed.

---

## UPDATE

Changes existing values.

```sql
UPDATE ROOT_DEPTH
SET ROOT_DEPTH_ID = 7
WHERE ROOT_DEPTH_ID = 9;
```

---

## TRUNCATE

Deletes **all rows** while keeping the table structure.

```sql
TRUNCATE TABLE ROOT_DEPTH;
```

Useful for restarting data loads.

---

# SQL Commands Learned

| Command | Purpose |
|----------|----------|
| `CREATE TABLE` | Create a table |
| `INSERT` | Add rows |
| `SELECT` | Retrieve data |
| `LIMIT` | Restrict returned rows |
| `UPDATE` | Modify existing rows |
| `DELETE` | Remove selected rows |
| `TRUNCATE` | Remove all rows while keeping the table |

---

# Key Takeaways

- SQL stands for **Structured Query Language**.
- Common pronunciations are **SQL** and **SeQueL**.
- Before loading data, apply **Data Modeling** and **Normalization**.
- Every table column requires a suitable data type.
- Snowflake internally converts `TEXT` to `VARCHAR`.
- `NUMBER(2)` may appear as `NUMBER(2,0)` after table creation.
- `INSERT` adds data to tables.
- Table Preview allows quick inspection of data.
- Most "Does Not Exist" errors are caused by incorrect context or permissions.
- `SELECT *` retrieves all columns.
- `LIMIT` restricts the number of returned rows.
- `DELETE` removes selected rows, while `TRUNCATE` removes all rows but keeps the table.

