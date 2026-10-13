# SQL Aggregate Functions

Aggregate functions perform calculations on multiple rows and return a single result.

The aggregate functions covered in this course are:

```text
MIN()
MAX()
COUNT()
SUM()
AVG()
```

---

# MIN()

The `MIN()` function returns the smallest value from the selected column.

Basic syntax:

```sql
SELECT MIN(column_name)
FROM table_name;
```

Example:

```sql
SELECT MIN(Price)
FROM Products;
```

A condition can also be added using `WHERE`:

```sql
SELECT MIN(Price)
FROM Products
WHERE Category = 'Technology';
```

---

# MAX()

The `MAX()` function returns the largest value from the selected column.

Basic syntax:

```sql
SELECT MAX(column_name)
FROM table_name;
```

Example:

```sql
SELECT MAX(Price)
FROM Products;
```

---

# Using Aliases with Aggregate Functions

An aggregate result can be given a temporary name using `AS`.

Example:

```sql
SELECT MIN(Price) AS SmallestPrice
FROM Products;
```

Another example:

```sql
SELECT MAX(Price) AS HighestPrice
FROM Products;
```

This makes the result easier to identify.

---

# COUNT()

The `COUNT()` function returns the number of rows or values depending on how it is used.

---

## COUNT(*)

`COUNT(*)` counts the total number of rows.

Syntax:

```sql
SELECT COUNT(*)
FROM table_name;
```

Example:

```sql
SELECT COUNT(*)
FROM Products;
```

---

## COUNT(column)

`COUNT(column_name)` counts the values present in a specific column.

Syntax:

```sql
SELECT COUNT(column_name)
FROM table_name;
```

Example:

```sql
SELECT COUNT(ProductName)
FROM Products;
```

---

## COUNT(DISTINCT column)

`COUNT(DISTINCT column_name)` counts the number of unique values in a column.

Syntax:

```sql
SELECT COUNT(DISTINCT column_name)
FROM table_name;
```

Example:

```sql
SELECT COUNT(DISTINCT Country)
FROM Customers;
```

Conceptually:

```text
COUNT(*)                  → Count rows
COUNT(column_name)        → Count values in a column
COUNT(DISTINCT column)    → Count unique values
```

---

# SUM()

The `SUM()` function calculates the total of a numeric column.

Basic syntax:

```sql
SELECT SUM(column_name)
FROM table_name;
```

Example:

```sql
SELECT SUM(Quantity)
FROM OrderDetails;
```

A condition can also be added:

```sql
SELECT SUM(Quantity)
FROM OrderDetails
WHERE ProductID = 10;
```

---

# AVG()

The `AVG()` function calculates the average value of a numeric column.

Basic syntax:

```sql
SELECT AVG(column_name)
FROM table_name;
```

Example:

```sql
SELECT AVG(Price)
FROM Products;
```

---

# Aggregate Functions with WHERE

Aggregate functions can be combined with a `WHERE` clause.

Example:

```sql
SELECT MIN(Price)
FROM Products
WHERE CategoryID = 1;
```

Another example:

```sql
SELECT AVG(Price)
FROM Products
WHERE CategoryID = 2;
```

The `WHERE` condition filters the rows before the aggregate function performs its calculation.

---

# Quick Reference

| Function | Purpose |
|---|---|
| `MIN()` | Return the smallest value |
| `MAX()` | Return the largest value |
| `COUNT(*)` | Count rows |
| `COUNT(column)` | Count values in a column |
| `COUNT(DISTINCT column)` | Count unique values |
| `SUM()` | Calculate the total of a numeric column |
| `AVG()` | Calculate the average of a numeric column |

---

## Examples

### Find the lowest price

```sql
SELECT MIN(Price)
FROM Products;
```

### Find the highest price

```sql
SELECT MAX(Price)
FROM Products;
```

### Count all rows

```sql
SELECT COUNT(*)
FROM Products;
```

### Count unique countries

```sql
SELECT COUNT(DISTINCT Country)
FROM Customers;
```

### Calculate total quantity

```sql
SELECT SUM(Quantity)
FROM OrderDetails;
```

### Calculate average price

```sql
SELECT AVG(Price)
FROM Products;
```

### Use an alias

```sql
SELECT MIN(Price) AS SmallestPrice
FROM Products;
```

---

## Notes

- Aggregate functions perform calculations across multiple rows.
- `MIN()` returns the smallest value.
- `MAX()` returns the largest value.
- `COUNT()` counts rows or values.
- `COUNT(DISTINCT ...)` counts unique values.
- `SUM()` calculates a total.
- `AVG()` calculates an average.
- `SUM()` and `AVG()` are used with numeric data.
- Aggregate functions can be combined with `WHERE`.
- `AS` can be used to give an aggregate result a temporary column name.
