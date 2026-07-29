> [!info]
> **Module Objective**
> Learn how to work with **nested JSON** in Snowflake using **JSON paths**, **arrays**, **FLATTEN**, and **Views** to make semi-structured data appear like relational tables.

#accenture #cognizant #snowflake 

---

## 1. Nested JSON

## What is Nested JSON?

In the previous module, each JSON row contained only one object.

Example:

```json
{
  "AUTHOR_UID": 1,
  "FIRST_NAME": "Fiona",
  "LAST_NAME": "Macdonald"
}
```

Real-world JSON is usually more complex.

Objects often contain other objects or arrays.

Example:

```json
{
  "BOOK_TITLE": "Food",
  "YEAR_PUBLISHED": 2001,
  "AUTHORS": [
    {
      "FIRST_NAME": "Fiona",
      "LAST_NAME": "Macdonald"
    },
    {
      "FIRST_NAME": "Gian",
      "LAST_NAME": "Faleschini"
    }
  ]
}
```

This structure is called **Nested JSON**.

---

## JSON Terminology

### Object

Surrounded by curly braces.

```json
{
    ...
}
```

---

### Array

Surrounded by square brackets.

```json
[
    ...
]
```

---

### Key

The attribute name.

Example:

```json
"FIRST_NAME"
```

---

### Value

The data associated with the key.

Example:

```json
"Fiona"
```

---

### Key-Value Pair

```json
"FIRST_NAME": "Fiona"
```

---

## JSON Structure

```text
Book
│
├── Book Title
├── Year Published
└── Authors
      │
      ├── Author 1
      └── Author 2
```

Think of nested JSON like **Russian nesting dolls**, where one object contains another object or array.

---

# 2. Loading Nested JSON

## Create the Table

```sql
CREATE OR REPLACE TABLE LIBRARY_CARD_CATALOG.PUBLIC.NESTED_INGEST_JSON
(
    RAW_NESTED_BOOK VARIANT
);
```

The existing JSON File Format from Module 9 can be reused.

---

## Load the File

```sql
COPY INTO LIBRARY_CARD_CATALOG.PUBLIC.NESTED_INGEST_JSON
FROM @UTIL_DB.PUBLIC.MY_INTERNAL_STAGE
FILES = ('json_book_author_nested.txt')
FILE_FORMAT = (
    FORMAT_NAME = LIBRARY_CARD_CATALOG.PUBLIC.JSON_FILE_FORMAT
);
```

---

# 3. Querying Nested JSON

Retrieve the entire JSON object:

```sql
SELECT RAW_NESTED_BOOK
FROM NESTED_INGEST_JSON;
```

---

Retrieve a top-level value:

```sql
SELECT RAW_NESTED_BOOK:YEAR_PUBLISHED
FROM NESTED_INGEST_JSON;
```

---

Retrieve the nested Authors array:

```sql
SELECT RAW_NESTED_BOOK:AUTHORS
FROM NESTED_INGEST_JSON;
```

---

# 4. JSON Paths

Snowflake accesses nested data using **JSON Paths**.

General syntax:

```text
COLUMN:KEY
```

Example:

```sql
RAW_NESTED_BOOK:YEAR_PUBLISHED
```

---

## Accessing Nested Arrays

Suppose the JSON contains:

```json
"AUTHORS":[
    {
        "FIRST_NAME":"Fiona"
    },
    {
        "FIRST_NAME":"Gian"
    }
]
```

The first author is accessed using index **0**.

```sql
RAW_NESTED_BOOK:AUTHORS[0].FIRST_NAME
```

Result:

```
Fiona
```

The second author:

```sql
RAW_NESTED_BOOK:AUTHORS[1].FIRST_NAME
```

Result:

```
Gian
```

> [!important]
> JSON arrays are **zero-indexed**.  
> The first element is at index **0**, not **1**.

---

# 5. FLATTEN

## Why FLATTEN?

Arrays store multiple values inside a single row.

Example:

```json
AUTHORS

[
   {...},
   {...}
]
```

To query each author individually, use **FLATTEN**.

---

## Using FLATTEN

```sql
SELECT VALUE:FIRST_NAME
FROM NESTED_INGEST_JSON,
LATERAL FLATTEN(
    INPUT => RAW_NESTED_BOOK:AUTHORS
);
```

Result:

| FIRST_NAME |
|------------|
| Fiona |
| Gian |
| Laura |
| ... |

Each array element becomes its own row.

---

## Equivalent Syntax

Snowflake also supports:

```sql
SELECT VALUE:FIRST_NAME
FROM NESTED_INGEST_JSON,
TABLE(FLATTEN(RAW_NESTED_BOOK:AUTHORS));
```

Both forms return the same results.

---

## Casting Values

Convert VARIANT values into SQL types.

```sql
SELECT
    VALUE:FIRST_NAME::VARCHAR,
    VALUE:LAST_NAME::VARCHAR
FROM NESTED_INGEST_JSON,
LATERAL FLATTEN(
    INPUT => RAW_NESTED_BOOK:AUTHORS
);
```

---

## Renaming Columns

```sql
SELECT
    VALUE:FIRST_NAME::VARCHAR AS FIRST_NM,
    VALUE:LAST_NAME::VARCHAR AS LAST_NM
FROM NESTED_INGEST_JSON,
LATERAL FLATTEN(
    INPUT => RAW_NESTED_BOOK:AUTHORS
);
```

---

# 6. Real-World Example - Twitter JSON

Real-world APIs generate deeply nested JSON.

Example hierarchy:

```text
Tweet
│
├── created_at
├── text
├── user
│     ├── id
│     └── name
│
└── entities
      ├── hashtags
      ├── urls
      └── user_mentions
```

Instead of creating dozens of relational tables immediately, Snowflake stores the complete JSON document in a VARIANT column.

Developers can later extract only the fields they need.

---

# 7. Exploring JSON

Before loading a JSON file, inspect its structure using a JSON viewer.

Example tool:

https://jsoneditoronline.org/

This helps identify:

- Objects
- Arrays
- Nested keys
- Paths required for queries

![877](../Images/Pasted%20image%2020260704191152.png)

![997](../Images/Pasted%20image%2020260704191335.png)


---

# 8. Challenge Lab - Load Tweet JSON

## Step 1 - Create Database

```sql
CREATE DATABASE SOCIAL_MEDIA_FLOODGATES;
```

---

## Step 2 - Create Table

```sql
USE DATABASE SOCIAL_MEDIA_FLOODGATES;

CREATE TABLE TWEET_INGEST
(
    RAW_STATUS VARIANT
);
```

---

## Step 3 - Create JSON File Format

```sql
CREATE OR REPLACE FILE FORMAT SOCIAL_MEDIA_FLOODGATES.PUBLIC.JSON_FILE_FORMAT
TYPE = 'JSON'
STRIP_OUTER_ARRAY = TRUE;
```

---

## Step 4 - Upload the File

Upload:

```
nutrition_tweets.json
```

to an internal stage (e.g., `@UTIL_DB.PUBLIC.MY_INTERNAL_STAGE`).

---

## Step 5 - Load the File

```sql
COPY INTO SOCIAL_MEDIA_FLOODGATES.PUBLIC.TWEET_INGEST
FROM @UTIL_DB.PUBLIC.MY_INTERNAL_STAGE
FILES = ('nutrition_tweets.json')
FILE_FORMAT = (
    FORMAT_NAME = SOCIAL_MEDIA_FLOODGATES.PUBLIC.JSON_FILE_FORMAT
);
```

---

## Step 6 - Verify the Load

```sql
SELECT *
FROM TWEET_INGEST;
```

Expected result:

- **9 rows**
- One tweet per row

---

# 9. Querying Tweet Data

Retrieve complete JSON:

```sql
SELECT RAW_STATUS
FROM TWEET_INGEST;
```

---

Retrieve entities:

```sql
SELECT RAW_STATUS:ENTITIES
FROM TWEET_INGEST;
```

---

Retrieve hashtags array:

```sql
SELECT RAW_STATUS:ENTITIES:HASHTAGS
FROM TWEET_INGEST;
```

---

Retrieve the first hashtag:

```sql
SELECT RAW_STATUS:ENTITIES:HASHTAGS[0].TEXT
FROM TWEET_INGEST;
```

---

Return only tweets that contain hashtags:

```sql
SELECT RAW_STATUS:ENTITIES:HASHTAGS[0].TEXT
FROM TWEET_INGEST
WHERE RAW_STATUS:ENTITIES:HASHTAGS[0].TEXT IS NOT NULL;
```

---

Retrieve tweet dates:

```sql
SELECT RAW_STATUS:CREATED_AT::DATE
FROM TWEET_INGEST
ORDER BY RAW_STATUS:CREATED_AT::DATE;
```

---

# 10. Flattening Nested Tweet Data

Flatten URL objects:

```sql
SELECT VALUE
FROM TWEET_INGEST,
LATERAL FLATTEN(
    INPUT => RAW_STATUS:ENTITIES:URLS
);
```

Equivalent syntax:

```sql
SELECT VALUE
FROM TWEET_INGEST,
TABLE(FLATTEN(RAW_STATUS:ENTITIES:URLS));
```

Both statements produce the same output.

---

## Flatten Hashtags

```sql
SELECT
    VALUE:TEXT::VARCHAR AS HASHTAG_USED
FROM TWEET_INGEST,
LATERAL FLATTEN(
    INPUT => RAW_STATUS:ENTITIES:HASHTAGS
);
```

---

## Preserve Tweet Context

```sql
SELECT
    RAW_STATUS:USER:NAME::TEXT AS USER_NAME,
    RAW_STATUS:ID AS TWEET_ID,
    VALUE:TEXT::VARCHAR AS HASHTAG_USED
FROM TWEET_INGEST,
LATERAL FLATTEN(
    INPUT => RAW_STATUS:ENTITIES:HASHTAGS
);
```

Each hashtag remains associated with its originating tweet.

---

# 11. Normalizing JSON with Views

## URLs View

```sql
CREATE OR REPLACE VIEW SOCIAL_MEDIA_FLOODGATES.PUBLIC.URLS_NORMALIZED AS
SELECT
    RAW_STATUS:USER:NAME::TEXT AS USER_NAME,
    RAW_STATUS:ID AS TWEET_ID,
    VALUE:DISPLAY_URL::TEXT AS URL_USED
FROM TWEET_INGEST,
LATERAL FLATTEN(
    INPUT => RAW_STATUS:ENTITIES:URLS
);
```

---

## Challenge - HASHTAGS_NORMALIZED View

```sql
CREATE OR REPLACE VIEW SOCIAL_MEDIA_FLOODGATES.PUBLIC.HASHTAGS_NORMALIZED AS
SELECT
    RAW_STATUS:USER:NAME::TEXT AS USER_NAME,
    RAW_STATUS:ID AS TWEET_ID,
    VALUE:TEXT::VARCHAR AS HASHTAG_USED
FROM TWEET_INGEST,
LATERAL FLATTEN(
    INPUT => RAW_STATUS:ENTITIES:HASHTAGS
);
```

Query the view:

```sql
SELECT *
FROM SOCIAL_MEDIA_FLOODGATES.PUBLIC.HASHTAGS_NORMALIZED;
```

The result resembles a normalized relational table while the original JSON remains unchanged.
![Pasted image 20260704191632](../Images/Pasted%20image%2020260704191632.png)

---

# Key Takeaways

- Nested JSON contains objects and arrays within other objects.
- JSON objects use `{}` and arrays use `[]`.
- Snowflake accesses nested data using JSON paths (`COLUMN:KEY`).
- Arrays are zero-indexed (`[0]`, `[1]`, ...).
- `FLATTEN` converts array elements into individual rows.
- `LATERAL FLATTEN` and `TABLE(FLATTEN())` are equivalent for most use cases.
- Cast JSON values using `::VARCHAR`, `::DATE`, etc., before treating them as SQL types.
- Store complete JSON in a VARIANT column and extract only the fields needed.
- Views can expose nested JSON as normalized relational data without duplicating or modifying the source JSON.

---

# Quick Revision

| Concept | Remember |
|----------|----------|
| Nested JSON | Objects and arrays inside other objects |
| JSON Object | `{}` |
| JSON Array | `[]` |
| JSON Path | `COLUMN:KEY` |
| Array Index | Starts at **0** |
| `FLATTEN` | Expands arrays into rows |
| `VALUE` | Current element produced by `FLATTEN` |
| `::VARCHAR` | Cast JSON value to SQL text |
| `LATERAL FLATTEN` | Preferred syntax for flattening arrays |
| View | Makes nested JSON appear like a relational table |