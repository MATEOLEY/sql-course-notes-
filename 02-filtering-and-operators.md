# Filtering and Operators

This section covers SQL commands and operators used to filter, sort, and narrow query results.

---

# WHERE

The `WHERE` clause is used to filter rows based on a specific condition.

Basic syntax:

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

Example:

```sql
SELECT *
FROM Customers
WHERE Country = 'Colombia';
```

Another example:

```sql
SELECT *
FROM Customers
WHERE Age > 18;
```

---

## Comparison Operators

The following comparison operators can be used with `WHERE`:

| Operator | Meaning |
|---|---|
| `=` | Equal |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal |
| `<=` | Less than or equal |
| `<>` | Not equal |
| `BETWEEN` | Between a certain range |
| `LIKE` | Search for a pattern |
| `IN` | Specify multiple possible values |

For `NULL` values, the notes use:

```sql
IS NULL
```

and:

```sql
IS NOT NULL
```

---

# ORDER BY

The `ORDER BY` command is used to sort the result of a query.

Basic syntax:

```sql
SELECT column1, column2
FROM table_name
ORDER BY column1;
```

By default, the result is ordered in ascending order.

To explicitly use ascending order:

```sql
ORDER BY column1 ASC;
```

To sort in descending order:

```sql
ORDER BY column1 DESC;
```

Example:

```sql
SELECT *
FROM Products
ORDER BY Price;
```

---

## Ordering by Multiple Columns

Multiple columns can be used in the `ORDER BY` clause.

Example:

```sql
SELECT column1, column2
FROM table_name
ORDER BY column1 ASC, column2 DESC;
```

---

# AND

The `AND` operator is used to combine two or more conditions.

All conditions must be true for the row to be returned.

Syntax:

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1
AND condition2;
```

Example:

```sql
SELECT *
FROM Customers
WHERE Country = 'Spain'
AND CustomerName LIKE 'M%';
```

Both conditions must be true.

---

# OR

The `OR` operator is used to combine conditions.

Only one of the conditions needs to be true.

Syntax:

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1
OR condition2;
```

Example:

```sql
SELECT *
FROM Customers
WHERE CustomerName LIKE 'M%'
OR CustomerName LIKE 'S%';
```

---

# NOT

The `NOT` operator is used to negate a condition.

Syntax:

```sql
SELECT column1, column2, ...
FROM table_name
WHERE NOT condition;
```

Example:

```sql
SELECT *
FROM Customers
WHERE NOT Country = 'Spain';
```

---

# LIKE

The `LIKE` operator is used in a `WHERE` clause to search for a specified pattern in a column.

Syntax:

```sql
SELECT column1, column2, ...
FROM table_name
WHERE column_name LIKE pattern;
```

Example:

```sql
SELECT *
FROM Customers
WHERE CustomerName LIKE 'a%';
```

---

# Wildcards

Wildcards are used together with `LIKE` to create search patterns.

Common wildcard symbols from the course notes include:

| Wildcard | Meaning |
|---|---|
| `%` | Zero or multiple characters |
| `_` | One single character |
| `[]` | Any single character within brackets |
| `^` | Any character not in brackets |
| `-` | Specify a range inside brackets |
| `{}` | Any escaped character |

Example:

```sql
SELECT *
FROM Customers
WHERE CustomerName LIKE 'a%';
```

The `%` wildcard allows multiple characters after `a`.

---

# IN

The `IN` operator is used as a shorter alternative to multiple `OR` conditions.

It allows multiple possible values to be specified inside a `WHERE` clause.

Syntax:

```sql
SELECT column1, column2, ...
FROM table_name
WHERE column_name IN (value1, value2, value3);
```

Example:

```sql
SELECT *
FROM Customers
WHERE Country IN ('Colombia', 'Brazil', 'Argentina');
```

The notes also mention that `NOT` can be combined with `IN`:

```sql
SELECT *
FROM Customers
WHERE Country NOT IN ('Colombia', 'Brazil');
```

---

# BETWEEN

The `BETWEEN` operator is used to select values within a specified range.

Syntax:

```sql
SELECT column1, column2, ...
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```

Example:

```sql
SELECT *
FROM Products
WHERE Price BETWEEN 10 AND 20;
```

The notes also mention that `NOT` can be combined with `BETWEEN`:

```sql
SELECT *
FROM Products
WHERE Price NOT BETWEEN 10 AND 20;
```

---

# Combining Conditions

Different operators can be combined inside a `WHERE` clause.

Example:

```sql
SELECT *
FROM Customers
WHERE Country = 'Spain'
AND CustomerName LIKE 'M%';
```

Another example:

```sql
SELECT *
FROM Customers
WHERE Country = 'Spain'
AND (
    CustomerName LIKE 'M%'
    OR CustomerName LIKE 'S%'
);
```

Parentheses can be used to group conditions.

---

# Quick Reference

| Command / Operator | Purpose |
|---|---|
| `WHERE` | Filter rows |
| `=` | Equal |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal |
| `<=` | Less than or equal |
| `<>` | Not equal |
| `ORDER BY` | Sort query results |
| `ASC` | Ascending order |
| `DESC` | Descending order |
| `AND` | Require multiple conditions |
| `OR` | Require at least one condition |
| `NOT` | Negate a condition |
| `LIKE` | Search using a pattern |
| `IN` | Match multiple possible values |
| `BETWEEN` | Match a value inside a range |
| `IS NULL` | Check for a NULL value |
| `IS NOT NULL` | Check for a non-NULL value |

---

## Examples

### Filter by value

```sql
SELECT *
FROM Customers
WHERE Country = 'Colombia';
```

### Filter using multiple conditions

```sql
SELECT *
FROM Customers
WHERE Country = 'Spain'
AND CustomerName LIKE 'M%';
```

### Sort results

```sql
SELECT *
FROM Products
ORDER BY Price DESC;
```

### Match multiple values

```sql
SELECT *
FROM Customers
WHERE Country IN ('Colombia', 'Brazil', 'Argentina');
```

### Select a range

```sql
SELECT *
FROM Products
WHERE Price BETWEEN 10 AND 20;
```

---

## Notes

- `WHERE` filters query results.
- `ORDER BY` sorts query results.
- `AND` requires all connected conditions to be true.
- `OR` requires at least one connected condition to be true.
- `NOT` negates a condition.
- `LIKE` is used for pattern matching.
- `IN` is useful when comparing a column against multiple possible values.
- `BETWEEN` is used for ranges.
- Parentheses can be used to group multiple conditions.
