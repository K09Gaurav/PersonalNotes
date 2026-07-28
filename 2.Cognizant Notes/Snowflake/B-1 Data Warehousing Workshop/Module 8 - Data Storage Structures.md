> [!info]
> **Module Objective**
> Learn how relational databases organize data using **tables**, **unique identifiers (Primary Keys)**, **Sequences**, **Auto Increment columns**, and **Bridge Tables** to model relationships between data.

#accenture #cognizant #snowflake 

---

# Quick Revision

| Concept | Remember |
|----------|----------|
| AUTOINCREMENT | Auto-generates IDs within one table |
| Sequence | Independent object that generates unique IDs |
| `NEXTVAL` | Returns the next sequence value |
| ORDER | Generates sequence values in order |
| BOOK | Stores book information |
| AUTHOR | Stores author information |
| BOOK_TO_AUTHOR | Bridge table connecting books and authors |
| Many-to-Many | One book ↔ many authors, one author ↔ many books |
| JOIN | Combines related tables using common keys |

---

# 1. Creating the Database

A new database is created to simulate a library catalog.

```sql
USE ROLE SYSADMIN;

CREATE DATABASE LIBRARY_CARD_CATALOG
COMMENT = 'DWW Lesson 10';

USE DATABASE LIBRARY_CARD_CATALOG;
```

The database structure will eventually look like:

```text
LIBRARY_CARD_CATALOG
│
├── BOOK
├── AUTHOR
├── BOOK_TO_AUTHOR
└── SEQ_AUTHOR_UID (Sequence)
```

---

# 2. The BOOK Table

The **BOOK** table stores information about books.

```sql
CREATE OR REPLACE TABLE BOOK
(
    BOOK_UID NUMBER AUTOINCREMENT,
    TITLE VARCHAR(50),
    YEAR_PUBLISHED NUMBER(4,0)
);
```

## AUTOINCREMENT

`AUTOINCREMENT` automatically generates a unique number whenever a new row is inserted.

Example:

```sql
INSERT INTO BOOK (TITLE, YEAR_PUBLISHED)
VALUES
('Food', 2001),
('Food', 2006),
('Food', 2008);
```

Result:

| BOOK_UID | TITLE | YEAR_PUBLISHED |
|----------:|-------|---------------:|
| 1 | Food | 2001 |
| 2 | Food | 2006 |
| 3 | Food | 2008 |

> [!important]
> Since `BOOK_UID` is auto-generated, it is **not included** in the `INSERT` statement.

---

# 3. The AUTHOR Table

The **AUTHOR** table stores author information.

```sql
CREATE OR REPLACE TABLE AUTHOR
(
    AUTHOR_UID NUMBER,
    FIRST_NAME VARCHAR(50),
    MIDDLE_NAME VARCHAR(50),
    LAST_NAME VARCHAR(50)
);
```

Initially, author IDs are entered manually.

```sql
INSERT INTO AUTHOR
(AUTHOR_UID, FIRST_NAME, MIDDLE_NAME, LAST_NAME)
VALUES
(1,'Fiona','','Macdonald'),
(2,'Gian','Paulo','Faleschini');
```

---

# 4. Sequences

## What is a Sequence?

A **Sequence** is a database object that generates **unique sequential numbers**.

Think of it as an automatic counter.

```
1
↓
2
↓
3
↓
4
↓
5
```

Unlike `AUTOINCREMENT`, a Sequence is **independent of any table** and can be reused across multiple tables.

---

## Why Use a Sequence?

`AUTOINCREMENT`

- Works for a single table only.

`SEQUENCE`

- Can generate IDs for multiple tables.
- Gives more control over numbering.
- Useful when related tables need coordinated IDs.

---

# 5. Creating a Sequence

![Pasted image 20260704183807](../Images/Pasted%20image%2020260704183807.png)
![Pasted image 20260704183855](../Images/Pasted%20image%2020260704183855.png)
![Pasted image 20260704183902](../Images/Pasted%20image%2020260704183902.png)
Example:

```sql
CREATE OR REPLACE SEQUENCE LIBRARY_CARD_CATALOG.PUBLIC.SEQ_AUTHOR_UID
START = 1
INCREMENT = 1
ORDER;
```

![Pasted image 20260704183919](../Images/Pasted%20image%2020260704183919.png)
### Properties

| Property | Meaning |
|----------|---------|
| START | First value generated |
| INCREMENT | Amount to increase each time |
| ORDER | Guarantees ordered values |

> [!note]
> Without the `ORDER` keyword, Snowflake may allocate values in larger jumps (e.g., by 100) to improve performance in distributed environments.

---

# 6. Using a Sequence

![Pasted image 20260704183941](../Images/Pasted%20image%2020260704183941.png)

Generate the next value:

```sql
SELECT SEQ_AUTHOR_UID.NEXTVAL;
```

Example executions:

```
1
2
3
4
```

Every call to `NEXTVAL` advances the sequence.

> [!important]
> Sequence values are **not reused**, even if rows are deleted. Gaps are normal.

---

## Using NEXTVAL Multiple Times

![Pasted image 20260704184016](../Images/Pasted%20image%2020260704184016.png)

Example:

```sql
SELECT
    SEQ_AUTHOR_UID.NEXTVAL,
    SEQ_AUTHOR_UID.NEXTVAL;
```

Possible output:

```
5    6
```

Each call generates a new unique value.

---

# 7. Resetting the Sequence

Since authors **1** and **2** already exist, recreate the sequence to start at **3**.

```sql
CREATE OR REPLACE SEQUENCE LIBRARY_CARD_CATALOG.PUBLIC.SEQ_AUTHOR_UID
START = 3
INCREMENT = 1
ORDER
COMMENT = 'Use this to fill in AUTHOR_UID values';
```

---

# 8. Using the Sequence in INSERT Statements

Instead of manually assigning IDs, use `NEXTVAL`.

```sql
INSERT INTO AUTHOR
(
    AUTHOR_UID,
    FIRST_NAME,
    MIDDLE_NAME,
    LAST_NAME
)
VALUES
(SEQ_AUTHOR_UID.NEXTVAL,'Laura','K','Egendorf'),
(SEQ_AUTHOR_UID.NEXTVAL,'Jan','','Grover'),
(SEQ_AUTHOR_UID.NEXTVAL,'Jennifer','','Clapp'),
(SEQ_AUTHOR_UID.NEXTVAL,'Kathleen','','Petelinsek');
```

Snowflake automatically generates:

| AUTHOR_UID | Author |
|------------:|--------|
| 3 | Laura K Egendorf |
| 4 | Jan Grover |
| 5 | Jennifer Clapp |
| 6 | Kathleen Petelinsek |

This approach avoids manually tracking the next available ID.

---

# 9. Relationships Between Tables

So far:

```
BOOK
```

contains books.

```
AUTHOR
```

contains authors.

How do we represent **which author wrote which book?**

A direct relationship won't work because:

- One book can have multiple authors.
- One author can write multiple books.

This is called a **Many-to-Many Relationship**.

---

# 10. Bridge Table (Junction Table)

To solve a Many-to-Many relationship, create a **Bridge Table**.

```sql
CREATE TABLE BOOK_TO_AUTHOR
(
    BOOK_UID NUMBER,
    AUTHOR_UID NUMBER
);
```

This table stores relationships instead of actual book or author details.

---

## Example Data

```sql
INSERT INTO BOOK_TO_AUTHOR
(BOOK_UID, AUTHOR_UID)
VALUES
(1,1),
(1,2),
(2,3),
(3,4),
(4,5),
(5,6);
```

---

## Relationship Diagram

```text
BOOK
│
│
├── BOOK_UID = 1
│
│
▼
BOOK_TO_AUTHOR
│
├── (1,1)
├── (1,2)
│
▼
AUTHOR
│
├── AUTHOR_UID = 1
└── AUTHOR_UID = 2
```

Book **1** is written by:

- Fiona Macdonald
- Gian Paulo Faleschini

---

# 11. Joining the Tables

To retrieve complete information, join all three tables.

```sql
SELECT *
FROM BOOK_TO_AUTHOR BA
JOIN AUTHOR A
    ON BA.AUTHOR_UID = A.AUTHOR_UID
JOIN BOOK B
    ON BA.BOOK_UID = B.BOOK_UID;
```

### Join Flow

```text
BOOK
   │
   │ BOOK_UID
   ▼
BOOK_TO_AUTHOR
   ▲
   │ AUTHOR_UID
AUTHOR
```

The bridge table connects the two main tables.

---

# Database Design Summary

```text
LIBRARY_CARD_CATALOG
│
├── BOOK
│      ├── BOOK_UID (PK)
│      ├── TITLE
│      └── YEAR_PUBLISHED
│
├── AUTHOR
│      ├── AUTHOR_UID (PK)
│      ├── FIRST_NAME
│      ├── MIDDLE_NAME
│      └── LAST_NAME
│
├── BOOK_TO_AUTHOR
│      ├── BOOK_UID (FK)
│      └── AUTHOR_UID (FK)
│
└── SEQ_AUTHOR_UID
```

---

# Key Takeaways

- `AUTOINCREMENT` automatically generates unique IDs for a single table.
- A **Sequence** is an independent object that generates unique sequential values.
- `NEXTVAL` retrieves the next available value from a Sequence.
- Sequence values are unique and are not reused, even if gaps appear.
- Use Sequences when multiple tables need coordinated unique identifiers.
- A **Bridge Table** (Junction Table) resolves **Many-to-Many** relationships.
- `BOOK_TO_AUTHOR` links books and authors without duplicating data.
- SQL `JOIN` combines related data across multiple tables using matching keys.

