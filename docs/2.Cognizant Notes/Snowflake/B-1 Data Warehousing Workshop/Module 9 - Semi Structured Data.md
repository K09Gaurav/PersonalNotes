> [!info]
> **Module Objective**
> Learn how Snowflake stores and queries **Semi-Structured Data** using the **VARIANT** data type, create a **JSON File Format**, load JSON files using `COPY INTO`, and extract values using JSON path notation.

#accenture #cognizant #snowflake 


---
# Quick Revision

| Concept | Remember |
|----------|----------|
| Semi-Structured Data | Flexible hierarchical data (JSON, XML, etc.) |
| VARIANT | Snowflake data type for semi-structured data |
| JSON File Format | Defines how JSON files are parsed |
| `STRIP_OUTER_ARRAY = TRUE` | Loads each JSON object as a separate row |
| `COPY INTO` | Loads staged JSON data into a table |
| `RAW_AUTHOR:FIELD` | Accesses a JSON attribute |
| `::STRING` | Casts a JSON value to SQL STRING |
| Supported Formats | JSON, XML, Parquet, Avro, ORC |

---

# 1. What is Semi-Structured Data?

Traditionally, databases stored **structured data**, where information is organized into rows and columns.

Example:

| ID | First Name | Last Name |
|----|------------|-----------|
| 1 | Fiona | Macdonald |
| 2 | Gian | Faleschini |

Modern applications (social media, e-commerce, APIs, and mobile apps) often exchange data in **semi-structured formats** instead.

Common semi-structured formats include:

- JSON
- XML
- Parquet
- Avro
- ORC

Unlike tables, semi-structured data is hierarchical and flexible.

JSON example:
![Pasted image 20260704184952](../Images/Pasted%20image%2020260704184952.png)

---

## Structured vs Semi-Structured Data

| Structured Data | Semi-Structured Data |
|-----------------|----------------------|
| Fixed rows and columns | Flexible hierarchical structure |
| Schema defined beforehand | Schema can vary between records |
| Stored in relational tables | Stored as documents or nested objects |

---

# 2. Snowflake VARIANT Data Type

Snowflake stores semi-structured data using the **VARIANT** data type.

The `VARIANT` type can hold:

- JSON
- XML
- Avro
- ORC
- Parquet

without first converting the data into relational tables.

---

## Creating a Table for JSON

```sql
USE DATABASE LIBRARY_CARD_CATALOG;
USE ROLE SYSADMIN;

CREATE TABLE LIBRARY_CARD_CATALOG.PUBLIC.AUTHOR_INGEST_JSON
(
    RAW_AUTHOR VARIANT
);
```

Table structure:

| Column | Data Type |
|---------|-----------|
| RAW_AUTHOR | VARIANT |

Each row stores one complete JSON object.

---

# 3. JSON File Format

To load JSON data correctly, create a JSON File Format.

```sql
CREATE FILE FORMAT LIBRARY_CARD_CATALOG.PUBLIC.JSON_FILE_FORMAT
TYPE = 'JSON'
COMPRESSION = 'AUTO'
ENABLE_OCTAL = FALSE
ALLOW_DUPLICATE = FALSE
STRIP_OUTER_ARRAY = TRUE
STRIP_NULL_VALUES = FALSE
IGNORE_UTF8_ERRORS = FALSE;
```

---

## Explanation of Properties

| Property | Value | Purpose |
|----------|-------|---------|
| `TYPE` | `JSON` | Specifies JSON file format |
| `COMPRESSION` | `AUTO` | Detects compression automatically |
| `ENABLE_OCTAL` | `FALSE` | Disables octal number parsing |
| `ALLOW_DUPLICATE` | `FALSE` | Rejects duplicate keys |
| `STRIP_OUTER_ARRAY` | `TRUE` | Loads each object inside the outer array as a separate row |
| `STRIP_NULL_VALUES` | `FALSE` | Retains null values |
| `IGNORE_UTF8_ERRORS` | `FALSE` | Does not ignore UTF-8 encoding errors |

> [!important]
> **`STRIP_OUTER_ARRAY = TRUE`** is the key setting in this lab.  
> The JSON file contains an outer square-bracket array (`[...]`). Enabling this option loads each JSON object as an individual row instead of storing the entire array in a single row.

![Pasted image 20260704185335](../Images/Pasted%20image%2020260704185335.png)

---

# 4. Loading the JSON File

Assuming the file `author_with_header.json` has already been uploaded to the internal stage:

```sql
COPY INTO LIBRARY_CARD_CATALOG.PUBLIC.AUTHOR_INGEST_JSON
FROM @UTIL_DB.PUBLIC.MY_INTERNAL_STAGE
FILES = ('author_with_header.json')
FILE_FORMAT = (
    FORMAT_NAME = LIBRARY_CARD_CATALOG.PUBLIC.JSON_FILE_FORMAT
);
```

---

## Data Loading Workflow

```text
JSON File

↓

Internal Stage

↓

JSON File Format

↓

COPY INTO

↓

VARIANT Column
```

Each JSON object becomes one row in the `AUTHOR_INGEST_JSON` table.

---

# 5. Viewing the Loaded JSON

Query the table:

```sql
SELECT *
FROM AUTHOR_INGEST_JSON;
```

The `RAW_AUTHOR` column contains complete JSON objects.

Example:

```json
{
  "AUTHOR_UID": 1,
  "FIRST_NAME": "Fiona",
  "MIDDLE_NAME": "",
  "LAST_NAME": "Macdonald"
}
```

---

# 6. Querying JSON Data

Snowflake uses **colon (`:`) notation** to access JSON attributes.

Example:

```sql
SELECT RAW_AUTHOR:AUTHOR_UID
FROM AUTHOR_INGEST_JSON;
```

Result:

| AUTHOR_UID |
|------------|
| 1 |
| 2 |
| 3 |
| ... |

---

## Extracting Multiple Fields

```sql
SELECT
    RAW_AUTHOR:AUTHOR_UID,
    RAW_AUTHOR:FIRST_NAME::STRING AS FIRST_NAME,
    RAW_AUTHOR:MIDDLE_NAME::STRING AS MIDDLE_NAME,
    RAW_AUTHOR:LAST_NAME::STRING AS LAST_NAME
FROM AUTHOR_INGEST_JSON;
```

Result:

| AUTHOR_UID | FIRST_NAME | MIDDLE_NAME | LAST_NAME |
|------------|------------|-------------|-----------|
| 1 | Fiona | | Macdonald |
| 2 | Gian | Paulo | Faleschini |
| ... | ... | ... | ... |

---

## Understanding the Syntax

### JSON Path Operator

```sql
RAW_AUTHOR:FIRST_NAME
```

- `RAW_AUTHOR` → VARIANT column
- `FIRST_NAME` → JSON attribute

---

### Type Casting

```sql
::STRING
```

Converts the JSON value into a SQL `STRING`.

Without casting, Snowflake treats the value as a VARIANT.

---

# 7. Query Flow

```text
VARIANT Column

↓

JSON Path (:)

↓

Extract Value

↓

Type Cast (::STRING)

↓

SQL Output
```

---

# Key Takeaways

- Semi-structured data is commonly exchanged using formats such as **JSON**, **XML**, **Parquet**, **Avro**, and **ORC**.
- Snowflake stores semi-structured data using the **VARIANT** data type.
- A JSON File Format defines how JSON files should be parsed during loading.
- `STRIP_OUTER_ARRAY = TRUE` loads each object inside a JSON array as a separate row.
- Use `COPY INTO` to load JSON files from a Stage into a VARIANT column.
- Access JSON attributes using **colon (`:`) notation**.
- Use `::STRING` (or another appropriate data type) to cast JSON values into SQL types for querying.
