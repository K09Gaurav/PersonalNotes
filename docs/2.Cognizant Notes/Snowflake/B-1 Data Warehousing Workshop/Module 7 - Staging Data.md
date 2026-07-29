---
tags:
  - accenture
  - snowflake
  - cognizant
---

> [!info]
> **Module Objective**
> Learn how Snowflake stages files before loading them into tables, create and use **Stage** objects, define reusable **File Formats**, and load data efficiently using the **COPY INTO** command.
 
---

# Quick Revision

| Concept                      | Remember                          |
| ---------------------------- | --------------------------------- |
| Stage                        | Temporary storage for files       |
| Internal Stage               | Snowflake-managed cloud storage   |
| COPY INTO                    | Loads staged data into tables     |
| File Format                  | Defines how files are parsed      |
| FIELD_DELIMITER              | Character separating columns      |
| SKIP_HEADER                  | Number of header rows to ignore   |
| FIELD_OPTIONALLY_ENCLOSED_BY | Handles quoted values             |
| TSV                          | Tab-Separated Values (`\t`)       |
| Query Stage                  | Read staged files before loading  |
| Common COPY Error            | Wrong File Format or delimiter    |
| Best Practice                | Inspect → Query → Load → Validate |

---

# 1. What is a Stage?

## Definition

A **Stage** is a storage location where files are kept temporarily before being loaded into Snowflake tables.

Instead of loading files directly into tables, the recommended workflow is:

```
Local File
      │
      ▼
Stage
      │
      ▼
Table
```

A Stage acts as an intermediate storage area.

---

## Internal Stage

In this module, an **Internal Stage** is created.

The stage stores files inside Snowflake-managed cloud storage.

![Pasted image 20260704181630](../Images/Pasted%20image%2020260704181630.png)
![Pasted image 20260704181640](../Images/Pasted%20image%2020260704181640.png)
![Pasted image 20260704181645](../Images/Pasted%20image%2020260704181645.png)

---

## Cloud Storage Behind the Scenes

Depending on the cloud provider, Snowflake stores staged files in different storage services.

| Cloud Provider | Storage Service |
|----------------|-----------------|
| AWS | Amazon S3 Bucket |
| Azure | Azure Blob Storage |
| Google Cloud | Google Cloud Storage Bucket |

Although users interact with a Stage, Snowflake manages the underlying cloud storage automatically.

---

# 2. Uploading Files to a Stage

A data file is uploaded into the internal stage.

Example file:

```
VEG_NAME_TO_SOIL_TYPE_PIPE.txt
```

![Pasted image 20260704181727](../Images/Pasted%20image%2020260704181727.png)
![Pasted image 20260704181732](../Images/Pasted%20image%2020260704181732.png)

---

## Data Loading Workflow

```
Local Computer

↓

Upload File

↓

Snowflake Stage

↓

COPY INTO

↓

Snowflake Table
```

---

# 3. Components Required for COPY INTO

A successful `COPY INTO` operation typically requires four components:

1. A destination table
2. A stage object
3. A source file
4. A file format (Optional but necessary)

---

## COPY INTO Syntax

```sql
COPY INTO table_name
FROM @stage_name
FILES = ('file_name')
FILE_FORMAT = (
    FORMAT_NAME = file_format_name
);
```
![Pasted image 20260704181759](../Images/Pasted%20image%2020260704181759.png)

---

## Component Summary

| Component | Purpose |
|-----------|----------|
| Table | Destination for loaded data |
| Stage | Holds uploaded files |
| File | Source data |
| File Format | Explains how the file is structured |

---

# 4. Creating the Destination Table

Example:

```sql
CREATE OR REPLACE TABLE VEGETABLE_DETAILS_SOIL_TYPE
(
    PLANT_NAME VARCHAR(25),
    SOIL_TYPE NUMBER(1,0)
);
```

---

## Table Structure

| Column | Data Type |
|----------|-----------|
| PLANT_NAME | VARCHAR(25) |
| SOIL_TYPE | NUMBER(1,0) |

---

# 5. File Formats

## What is a File Format?

A File Format tells Snowflake **how to interpret a file**.

It defines properties such as:

- Delimiter
- Header rows
- Quoting
- Escaping
- Encoding

Instead of repeating these settings every time, create reusable File Format objects.

---

# 6. Pipe-Delimited File Format

Example:

```sql
CREATE FILE FORMAT PIPECOLSEP_ONEHEADROW
TYPE = 'CSV'
FIELD_DELIMITER = '|'
SKIP_HEADER = 1;
```

---

## Explanation

### TYPE

```sql
TYPE = 'CSV'
```

Even though the file uses pipes, Snowflake treats most flat files as CSV-type files.

This setting is used for:

- CSV
- TSV
- Pipe-delimited files
- Other text-based flat files

---

### FIELD_DELIMITER

```sql
FIELD_DELIMITER='|'
```

Specifies that columns are separated using:

```
|
```

---

### SKIP_HEADER

```sql
SKIP_HEADER=1
```

Ignore the first row because it contains column names rather than data.

---

# 7. Loading Data with COPY INTO

Example:

```sql
COPY INTO VEGETABLE_DETAILS_SOIL_TYPE
FROM @UTIL_DB.PUBLIC.MY_INTERNAL_STAGE
FILES=('VEG_NAME_TO_SOIL_TYPE_PIPE.txt')
FILE_FORMAT=(
FORMAT_NAME=GARDEN_PLANTS.VEGGIES.PIPECOLSEP_ONEHEADROW
);
```

---

## COPY INTO Process

```
Stage

↓

Read File

↓

Interpret File
(using File Format)

↓

Load Rows

↓

Destination Table
```

---

# 8. Querying Files Before Loading

A major advantage of Stages is that files can be queried before loading.

Example:

```sql
SELECT $1
FROM @stage/file;
```

This reads the staged file directly.

No table is required.

---

## Why Query Before Loading?

Useful for:

- Verifying delimiter
- Checking header rows
- Confirming column order
- Detecting formatting issues

This helps prevent loading bad data.

---

# 9. File Format Comparison

The same file can produce different results depending on the File Format.

Example:

```
Apple,"Loamy Soil",1
```

---

Correct File Format

↓

```
Column 1

Apple

Column 2

Loamy Soil

Column 3

1
```

---

Incorrect File Format

↓

```
Apple,"Loamy Soil",1
```

appears as one entire column.

This demonstrates why choosing the correct File Format is critical.

---

# 10. Optional Quoting

Some files surround values with quotation marks.

Example:

```text
"Apple","Loamy Soil","1"
```

To support this:

```sql
FIELD_OPTIONALLY_ENCLOSED_BY='"'
```

This tells Snowflake to remove quotation marks during parsing.

---

## Example File Format

```sql
create file format garden_plants.veggies.COMMASEP_DBLQUOT_ONEHEADROW 
    TYPE = 'CSV'--csv for comma separated files
    FIELD_DELIMITER = ',' --commas as column separators
    SKIP_HEADER = 1 --one header row  
    FIELD_OPTIONALLY_ENCLOSED_BY = '"' --this means that some values will be wrapped in double-quotes bc they have commas in them
    ;
```

---

# 11. TSV Files

TSV stands for:

> **Tab-Separated Values**

Columns are separated using:

```
\t
```

(tab character)

Example:

```text
1    Clay    Heavy soil
2    Sandy   Loose soil
```

The tab characters are invisible in most editors.

---

## Tab Delimiter

A File Format for TSV files uses:

```sql
FIELD_DELIMITER='\t'
```

---

# 12. Challenge Lab - Create a Custom File Format

The file **`LU_SOIL_TYPE.tsv`** is a **TSV (Tab-Separated Values)** file with:

- Tab (`\t`) as the column delimiter
- One header row
- Some text fields enclosed in double quotes

Therefore, create the following File Format:

```sql
CREATE OR REPLACE FILE FORMAT GARDEN_PLANTS.VEGGIES.L9_CHALLENGE_FF
TYPE = 'CSV'
FIELD_DELIMITER = '\t'
SKIP_HEADER = 1
FIELD_OPTIONALLY_ENCLOSED_BY = '"';
```

### Verify the File Format

Before loading, query the staged file:

```sql
SELECT
    $1,
    $2,
    $3
FROM @UTIL_DB.PUBLIC.MY_INTERNAL_STAGE/LU_SOIL_TYPE.tsv
(
    FILE_FORMAT => GARDEN_PLANTS.VEGGIES.L9_CHALLENGE_FF
);
```

If the output shows three properly separated columns, the File Format is correct.

---

# 13. Challenge Lab - Create and Load the Soil Lookup Table

## Create the Table

```sql
CREATE OR REPLACE TABLE GARDEN_PLANTS.VEGGIES.LU_SOIL_TYPE
(
    SOIL_TYPE_ID NUMBER,
    SOIL_TYPE VARCHAR(15),
    SOIL_DESCRIPTION VARCHAR(75)
);
```

---

## Load the File

```sql
COPY INTO GARDEN_PLANTS.VEGGIES.LU_SOIL_TYPE
FROM @UTIL_DB.PUBLIC.MY_INTERNAL_STAGE
FILES = ('LU_SOIL_TYPE.tsv')
FILE_FORMAT = (
    FORMAT_NAME = GARDEN_PLANTS.VEGGIES.L9_CHALLENGE_FF
);
```

---

## Verify the Load

```sql
SELECT *
FROM GARDEN_PLANTS.VEGGIES.LU_SOIL_TYPE;
```

If the data is parsed correctly:

- Columns are separated properly.
- Header row is skipped.
- Text values are clean (without extra quotes).

If the data is incorrect:

```sql
TRUNCATE TABLE GARDEN_PLANTS.VEGGIES.LU_SOIL_TYPE;
```

Fix the File Format and run the `COPY INTO` command again.

---

# 14. Challenge Lab - Create and Load the Plant Height Table

## Step 1 - Inspect the File

Open **`veg_plant_height.csv`** in a text editor.

Observations:

- Comma-separated values
- One header row
- Standard CSV format

---

## Step 2 - Create the Table

Use the header row from the file as the column names.

```sql
CREATE OR REPLACE TABLE GARDEN_PLANTS.VEGGIES.VEGETABLE_DETAILS_PLANT_HEIGHT
(
    PLANT_NAME VARCHAR(25),
    UOM VARCHAR(2),
    LOW_END_OF_RANGE NUMBER(3),
    HIGH_END_OF_RANGE NUMBER(3)
);
```

> [!note]
> The column names and data types are chosen based on the CSV header and sample values.

---

## Step 3 - Upload the File

Upload **`veg_plant_height.csv`** to:

```
@UTIL_DB.PUBLIC.MY_INTERNAL_STAGE
```

using the Stage upload interface.

---

## Step 4 - Choose the Correct File Format

Since the file is:

- Comma-separated
- Has one header row

Reuse the previously created File Format:

```
COMMASEP_DBLQUOT_ONEHEADROW
```

No new File Format is required.

---

## Step 5 - Load the File

```sql
COPY INTO GARDEN_PLANTS.VEGGIES.VEGETABLE_DETAILS_PLANT_HEIGHT
FROM @UTIL_DB.PUBLIC.MY_INTERNAL_STAGE
FILES = ('veg_plant_height.csv')
FILE_FORMAT = (
    FORMAT_NAME = GARDEN_PLANTS.VEGGIES.COMMASEP_DBLQUOT_ONEHEADROW
);
```

---

## Step 6 - Verify the Data

```sql
SELECT *
FROM GARDEN_PLANTS.VEGGIES.VEGETABLE_DETAILS_PLANT_HEIGHT;
```

Confirm that:

- All rows are loaded.
- Each value appears in the correct column.
- No header row exists in the table.

---

# 15. Common COPY INTO Errors & Troubleshooting

## Error

```text
Number of columns in file (1)
does not match that of the corresponding table (4)
```

### Cause

Snowflake is reading the entire line as a single column because the wrong File Format (or delimiter) is being used.

For example:

```
Carrot,cm,15,30
```

If the File Format expects a pipe (`|`) delimiter instead of a comma (`,`), Snowflake treats the entire line as one value.

---

## Troubleshooting Checklist

1. Verify the correct file is uploaded to the Stage.
2. Check the file delimiter in a text editor.
3. Ensure the correct File Format is used.
4. Confirm the table has the same number of columns as the file.
5. Query the staged file before loading to verify parsing:

```sql
SELECT
    $1,
    $2,
    $3,
    $4
FROM @UTIL_DB.PUBLIC.MY_INTERNAL_STAGE/veg_plant_height.csv
(
    FILE_FORMAT => GARDEN_PLANTS.VEGGIES.COMMASEP_DBLQUOT_ONEHEADROW
);
```

6. If the table was loaded incorrectly:

```sql
TRUNCATE TABLE GARDEN_PLANTS.VEGGIES.VEGETABLE_DETAILS_PLANT_HEIGHT;
```

Then rerun the `COPY INTO` command with the correct File Format.

> [!tip]
> Always validate a staged file with a `SELECT` before using `COPY INTO`. It is much easier to fix a File Format than to clean up incorrectly loaded data.
---

---

# COPY INTO Workflow

```
Local File

↓

Upload

↓

Internal Stage

↓

Query File

↓

Create File Format

↓

Create Table

↓

COPY INTO

↓

Validate Data
```

---

# Key Takeaways

- A Stage is a temporary storage location used before loading data into Snowflake tables.
- Internal Stages use cloud storage managed by Snowflake (Amazon S3, Azure Blob Storage, or Google Cloud Storage).
- `COPY INTO` is Snowflake's primary command for loading staged data into tables.
- A typical `COPY INTO` workflow requires:
  - Table
  - Stage
  - File
  - File Format
- File Formats describe how Snowflake should interpret flat files.
- `TYPE='CSV'` is used for most flat files, including CSV, TSV, and pipe-delimited files.
- Always inspect raw files before creating File Formats.
- Query staged files before loading them to validate parsing.
- Incorrect delimiters are the most common cause of loading errors.
- If data loads incorrectly, fix the File Format, truncate the table, and reload.

