# SQL Fundamentals

This section contains the basic SQL concepts and commands introduced at the beginning of the course.

---

## SQL Versions / Implementations Mentioned

The course works with SQL implementations such as:

```text
SQL Server
MySQL
```

Some syntax may vary depending on the database system being used.

---

## SQL Case Sensitivity

According to the course notes:

```text
SQL is not case-sensitive.
```

For example, SQL keywords may appear as:

```sql
SELECT
```

or:

```sql
select
```

Throughout these notes, SQL keywords will normally be written in uppercase to make queries easier to read.

---

# Important SQL Commands

The course introduces several important SQL commands:

| Command | Purpose |
|---|---|
| `SELECT` | Extract data from a database |
| `UPDATE` | Update data in a database |
| `DELETE` | Delete data from a database |
| `INSERT INTO` | Insert new data |
| `CREATE DATABASE` | Create a new database |
| `ALTER DATABASE` | Modify a database |
| `CREATE TABLE` | Create a table |
| `ALTER TABLE` | Modify a table |
| `DROP TABLE` | Delete a table |
| `CREATE INDEX` | Create an index |
| `DROP INDEX` | Delete an index |

These commands will be covered in more detail throughout the repository.

---

# SELECT

The `SELECT` command is used to retrieve information from a table.

Basic syntax:

```sql
SELECT column1, column2, ...
FROM table_name;
```

Example:

```sql
SELECT CustomerName, CustomerID
FROM Customers;
```

This retrieves the selected columns from the specified table.

---

## Selecting All Columns

To retrieve all columns from a table, use:

```sql
SELECT *
FROM table_name;
```

The `*` represents all columns.

Example:

```sql
SELECT *
FROM Customers;
```

---

# SELECT DISTINCT

`SELECT DISTINCT` is used when a column contains repeated values and only unique values should be returned.

Basic syntax:

```sql
SELECT DISTINCT column1, column2, ...
FROM table_name;
```

Example:

```sql
SELECT DISTINCT Country
FROM Customers;
```

Instead of displaying the same country multiple times, the result contains only the distinct values.

---

# COUNT with DISTINCT

If the goal is to determine how many unique values exist, `COUNT` can be combined with `DISTINCT`.

Syntax:

```sql
SELECT COUNT(DISTINCT column1)
FROM table_name;
```

Example:

```sql
SELECT COUNT(DISTINCT Country)
FROM Customers;
```

This returns the number of distinct values found in the selected column.

> `COUNT(DISTINCT ...)` returns the number of unique values rather than displaying the values themselves.

---

# Basic SELECT Structure

A basic SQL query follows this structure:

```sql
SELECT column1, column2
FROM table_name;
```

Conceptually:

```text
SELECT → What data do I want?
FROM   → Where does the data come from?
```

Example:

```sql
SELECT CustomerName, Country
FROM Customers;
```

---

# Quick Reference

| Syntax | Purpose |
|---|---|
| `SELECT column FROM table;` | Retrieve a column |
| `SELECT column1, column2 FROM table;` | Retrieve multiple columns |
| `SELECT * FROM table;` | Retrieve all columns |
| `SELECT DISTINCT column FROM table;` | Retrieve unique values |
| `COUNT(DISTINCT column)` | Count unique values |

---

## Examples

### Select one column

```sql
SELECT CustomerName
FROM Customers;
```

### Select multiple columns

```sql
SELECT CustomerName, Country
FROM Customers;
```

### Select all columns

```sql
SELECT *
FROM Customers;
```

### Select unique values

```sql
SELECT DISTINCT Country
FROM Customers;
```

### Count unique values

```sql
SELECT COUNT(DISTINCT Country)
FROM Customers;
```

---

## Notes

- `SELECT` retrieves data from a database table.
- `FROM` specifies the table containing the data.
- `*` selects all columns.
- `DISTINCT` removes duplicate values from the result.
- `COUNT(DISTINCT column)` counts the number of unique values.
- SQL keywords will normally be written in uppercase throughout this repository for readability.
