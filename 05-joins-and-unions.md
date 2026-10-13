# SQL Joins and Unions

This section covers SQL operations used to combine data from multiple tables or query results.

The topics covered are:

```text
INNER JOIN
LEFT JOIN
RIGHT JOIN
FULL JOIN
SELF JOIN
UNION
```

---

# SQL JOIN

A `JOIN` combines rows from two or more tables using a related column between them.

The main JOIN types covered in the course are:

| JOIN | Purpose |
|---|---|
| `INNER JOIN` | Returns rows with matching values in both tables |
| `LEFT JOIN` | Returns all rows from the left table and matching rows from the right table |
| `RIGHT JOIN` | Returns all rows from the right table and matching rows from the left table |
| `FULL JOIN` | Returns rows when there is a match in either table |
| `SELF JOIN` | Joins a table with itself |

---

# INNER JOIN

`INNER JOIN` returns only rows where there is a matching value in both tables.

Conceptually:

```text
TABLE 1        TABLE 2

   (   ( MATCH )   )
```

Only the matching section is returned.

Basic syntax:

```sql
SELECT column_names
FROM table1
INNER JOIN table2
ON table1.column_name = table2.column_name;
```

The `ON` clause defines the relationship between the two tables.

Example:

```sql
SELECT Products.ProductName, Categories.CategoryName
FROM Products
INNER JOIN Categories
ON Products.CategoryID = Categories.CategoryID;
```

In this example, the related column is:

```text
CategoryID
```

---

# LEFT JOIN

A `LEFT JOIN` returns:

```text
All rows from the left table
+
Matching rows from the right table
```

If there is no matching value in the right table, the result contains `NULL` values for the right-table columns.

Basic syntax:

```sql
SELECT column_names
FROM table1
LEFT JOIN table2
ON table1.column_name = table2.column_name;
```

Example:

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

This returns all customers, even when a customer does not have a matching order.

`LEFT OUTER JOIN` can also be written as:

```sql
LEFT JOIN
```

The `OUTER` keyword is optional.

---

# RIGHT JOIN

A `RIGHT JOIN` works similarly to a `LEFT JOIN`, but returns all rows from the right table.

Conceptually:

```text
Matching rows
+
All rows from Table 2
```

Basic syntax:

```sql
SELECT column_names
FROM table1
RIGHT JOIN table2
ON table1.column_name = table2.column_name;
```

Rows from the right table are returned even when no matching row exists in the left table.

---

# FULL JOIN

A `FULL JOIN` returns all rows when there is a match in either the left or right table.

This includes:

```text
Matching rows
+
Unmatched rows from Table 1
+
Unmatched rows from Table 2
```

When there is no matching value on one side, the missing values are returned as:

```text
NULL
```

Basic syntax:

```sql
SELECT columns
FROM table1
FULL JOIN table2
ON table1.column_name = table2.column_name;
```

Example:

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
FULL JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

---

# JOIN Comparison

A simple way to remember the different JOIN types:

```text
INNER JOIN
→ Only matching rows

LEFT JOIN
→ Everything from the left + matches from the right

RIGHT JOIN
→ Everything from the right + matches from the left

FULL JOIN
→ Everything from both tables
```

---

# SELF JOIN

A `SELF JOIN` is a regular join where a table is joined with itself.

Aliases are used so the same table can be treated as two different table references.

Basic structure:

```sql
SELECT column_names
FROM table_name T1, table_name T2
WHERE condition;
```

Example:

```sql
SELECT
    A.CustomerName AS CustomerName1,
    B.CustomerName AS CustomerName2,
    A.City
FROM Customers A, Customers B
WHERE A.CustomerID <> B.CustomerID
AND A.City = B.City;
```

Here:

```text
A → First reference to Customers
B → Second reference to Customers
```

The query compares rows from the same table.

---

# SQL UNION

The `UNION` operator combines the results of two or more `SELECT` statements.

Basic syntax:

```sql
SELECT column_name
FROM table1

UNION

SELECT column_name
FROM table2;
```

---

## UNION Requirements

According to the course notes, queries combined with `UNION` must follow these requirements:

1. Each `SELECT` statement must return the same number of columns.
2. The columns must have similar data types.
3. The columns should appear in the same order.

---

## UNION Removes Duplicates

`UNION` combines the results and removes duplicate rows from the final output.

Example:

```sql
SELECT City, Country
FROM Customers

UNION

SELECT City, Country
FROM Suppliers;
```

The result combines cities and countries from both queries.

Duplicate rows appear only once.

---

# JOIN vs UNION

Although both can combine information, they work differently.

```text
JOIN
→ Combines columns using relationships between tables

UNION
→ Combines rows from multiple SELECT results
```

Conceptually:

```text
JOIN
Table A + Table B
        ↓
More columns
```

```text
UNION
Query A
  +
Query B
  ↓
More rows
```

---

# Quick Reference

| Operation | Result |
|---|---|
| `INNER JOIN` | Matching rows from both tables |
| `LEFT JOIN` | All left rows + matching right rows |
| `RIGHT JOIN` | All right rows + matching left rows |
| `FULL JOIN` | All rows from both tables |
| `SELF JOIN` | A table joined with itself |
| `UNION` | Combines results from multiple `SELECT` statements |

---

## Example Summary

### INNER JOIN

```sql
SELECT Products.ProductName, Categories.CategoryName
FROM Products
INNER JOIN Categories
ON Products.CategoryID = Categories.CategoryID;
```

### LEFT JOIN

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

### RIGHT JOIN

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
RIGHT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

### FULL JOIN

```sql
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
FULL JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

### UNION

```sql
SELECT City, Country
FROM Customers

UNION

SELECT City, Country
FROM Suppliers;
```

---

## Notes

- `JOIN` combines information from related tables.
- The `ON` clause defines which columns relate the tables.
- `INNER JOIN` returns only matching rows.
- `LEFT JOIN` keeps all rows from the left table.
- `RIGHT JOIN` keeps all rows from the right table.
- `FULL JOIN` keeps rows from both tables.
- Missing values from unmatched rows appear as `NULL`.
- `SELF JOIN` compares rows within the same table.
- `UNION` combines the output of multiple `SELECT` statements.
- Queries used with `UNION` must return compatible columns in the same order.
