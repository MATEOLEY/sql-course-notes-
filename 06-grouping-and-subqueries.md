# Grouping, Subqueries and Advanced Queries

This section covers SQL operations used to group results, filter aggregated data, work with subqueries, copy query results between tables, and return different values based on conditions.

Topics covered:

```text
GROUP BY
HAVING
EXISTS
ANY
ALL
SELECT INTO
INSERT INTO SELECT
CASE
```

---

# GROUP BY

The `GROUP BY` statement groups rows that have the same values into summary rows.

It is commonly used with aggregate functions such as:

```text
COUNT()
MAX()
MIN()
SUM()
AVG()
```

Basic syntax:

```sql
SELECT column1, aggregate_function(column2)
FROM table_name
WHERE condition
GROUP BY column1;
```

Example:

```sql
SELECT Country, COUNT(CustomerID) AS NumberOfCustomers
FROM Customers
GROUP BY Country;
```

This groups customers by country and counts the number of customers in each country.

Conceptually:

```text
Customers
    ↓
Group rows by Country
    ↓
Count customers in each group
```

---

## GROUP BY with ORDER BY

Grouped results can also be sorted.

Example:

```sql
SELECT Country, COUNT(CustomerID) AS NumberOfCustomers
FROM Customers
GROUP BY Country
ORDER BY NumberOfCustomers DESC;
```

---

# HAVING

The `HAVING` clause is used to filter grouped results.

It is commonly used after `GROUP BY`.

Basic syntax:

```sql
SELECT column1, aggregate_function(column2)
FROM table_name
WHERE condition
GROUP BY column1
HAVING condition;
```

Example:

```sql
SELECT Country, COUNT(CustomerID) AS NumberOfCustomers
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5;
```

This returns only countries that have more than five customers.

---

## GROUP BY and HAVING

A common structure is:

```sql
SELECT column1, COUNT(column2)
FROM table_name
GROUP BY column1
HAVING COUNT(column2) > value;
```

Example:

```sql
SELECT Country, COUNT(CustomerID)
FROM Customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5
ORDER BY COUNT(CustomerID) DESC;
```

Conceptually:

```text
GROUP BY
    ↓
Create groups
    ↓
Apply aggregate function
    ↓
HAVING
    ↓
Filter the grouped results
```

---

# WHERE vs HAVING

`WHERE` and `HAVING` both filter information, but they are used at different stages of a query.

```text
WHERE
→ Filters rows

GROUP BY
→ Creates groups

HAVING
→ Filters groups
```

Example:

```sql
SELECT Country, COUNT(CustomerID)
FROM Customers
WHERE Country IS NOT NULL
GROUP BY Country
HAVING COUNT(CustomerID) > 5;
```

---

# EXISTS

The `EXISTS` operator is used with a subquery to check whether the subquery returns any rows.

Basic syntax:

```sql
SELECT column_names
FROM table_name
WHERE EXISTS (
    SELECT column_name
    FROM another_table
    WHERE condition
);
```

If the subquery returns records, the `EXISTS` condition evaluates as true.

---

## EXISTS Example

```sql
SELECT SupplierName
FROM Suppliers
WHERE EXISTS (
    SELECT ProductName
    FROM Products
    WHERE Products.SupplierID = Suppliers.SupplierID
);
```

Conceptually:

```text
Main Query
    ↓
Run Subquery
    ↓
Does the subquery return a row?
    ↓
Yes → EXISTS is true
No  → EXISTS is false
```

---

# Subqueries

A **subquery** is a query placed inside another SQL query.

Example structure:

```sql
SELECT column_name
FROM table_name
WHERE column_name operator (
    SELECT column_name
    FROM another_table
);
```

Subqueries can be used with operators such as:

```text
EXISTS
ANY
ALL
```

---

# ANY

The `ANY` operator compares a value with the values returned by a subquery.

The comparison is true if the condition is true for at least one value returned by the subquery.

Basic syntax:

```sql
SELECT column_names
FROM table_name
WHERE column_name operator ANY (
    SELECT column_name
    FROM another_table
    WHERE condition
);
```

Comparison operators can include:

```text
=
>
<
>=
<=
<>
```

Example structure:

```sql
SELECT ProductName
FROM Products
WHERE ProductID = ANY (
    SELECT ProductID
    FROM OrderDetails
    WHERE Quantity = 10
);
```

Conceptually:

```text
ANY

Comparison with:
Value 1
Value 2
Value 3
...

If at least one comparison is true
→ Condition is true
```

---

# ALL

The `ALL` operator compares a value against all values returned by a subquery.

The condition must be true for all values returned by the subquery.

Basic syntax:

```sql
SELECT column_names
FROM table_name
WHERE column_name operator ALL (
    SELECT column_name
    FROM another_table
    WHERE condition
);
```

Example structure:

```sql
SELECT ProductName
FROM Products
WHERE ProductID = ALL (
    SELECT ProductID
    FROM OrderDetails
    WHERE Quantity = 10
);
```

Conceptually:

```text
ALL

Comparison with:
Value 1
Value 2
Value 3
...

All comparisons must satisfy the condition
```

---

# ANY vs ALL

A simple way to remember them:

```text
ANY
→ At least one result must satisfy the condition

ALL
→ Every result must satisfy the condition
```

---

# SELECT INTO

`SELECT INTO` creates a new table using data selected from an existing table.

It can be used to copy:

```text
All columns
or
Specific columns
```

---

## Copy All Columns

Basic syntax:

```sql
SELECT *
INTO new_table
FROM source_table
WHERE condition;
```

Example:

```sql
SELECT *
INTO CustomersBackup
FROM Customers;
```

This creates a new table based on the selected data.

---

## Copy Specific Columns

Specific columns can also be copied.

```sql
SELECT column1, column2
INTO new_table
FROM source_table
WHERE condition;
```

Example:

```sql
SELECT CustomerName, Country
INTO CustomersBackup
FROM Customers;
```

---

## Create an Empty Table Structure

The course notes also show that `SELECT INTO` can be used to create a new table structure without copying rows by using a condition that is always false.

Example:

```sql
SELECT *
INTO CustomersBackup
FROM Customers
WHERE 1 = 0;
```

Because:

```text
1 = 0
```

is never true, no rows are selected.

The new table is created without copying the existing records.

---

# INSERT INTO SELECT

`INSERT INTO SELECT` copies data from one table and inserts it into another existing table.

The source and destination data should be compatible.

---

## Copy All Columns

Basic structure:

```sql
INSERT INTO destination_table
SELECT *
FROM source_table
WHERE condition;
```

---

## Copy Specific Columns

Specific columns can also be copied.

```sql
INSERT INTO destination_table (column1, column2)
SELECT column1, column2
FROM source_table
WHERE condition;
```

Conceptually:

```text
Source Table
     ↓
SELECT data
     ↓
INSERT INTO
     ↓
Destination Table
```

---

# SELECT INTO vs INSERT INTO SELECT

These statements perform related tasks but are used differently.

```text
SELECT INTO
→ Creates a new table from query results

INSERT INTO SELECT
→ Inserts query results into an existing table
```

---

# CASE

The `CASE` expression allows different values to be returned based on specified conditions.

It evaluates conditions in order.

When a condition is true, the corresponding result is returned.

Basic syntax:

```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    WHEN condition3 THEN result3
    ELSE result
END
```

---

## CASE Example

```sql
SELECT ProductName, Price,
CASE
    WHEN Price < 30 THEN 'Low Cost'
    WHEN Price BETWEEN 30 AND 50 THEN 'Medium Cost'
    ELSE 'High Cost'
END AS PriceCategory
FROM Products;
```

Conceptually:

```text
Check condition 1
    ↓
True?
├── Yes → Return result
└── No
     ↓
Check condition 2
     ↓
True?
├── Yes → Return result
└── No
     ↓
ELSE
```

If none of the conditions match, the `ELSE` result is returned when one is provided.

---

# Quick Reference

| Command / Operator | Purpose |
|---|---|
| `GROUP BY` | Group rows with matching values |
| `HAVING` | Filter grouped results |
| `EXISTS` | Check whether a subquery returns rows |
| `ANY` | Compare against any value returned by a subquery |
| `ALL` | Compare against all values returned by a subquery |
| `SELECT INTO` | Create a new table from query results |
| `INSERT INTO SELECT` | Copy query results into an existing table |
| `CASE` | Return different values based on conditions |

---

# Query Execution Concept

A useful conceptual structure is:

```text
SELECT
    ↓
FROM
    ↓
WHERE
    ↓
GROUP BY
    ↓
HAVING
    ↓
ORDER BY
```

This helps visualize how filtering and grouping work together.

---

## Notes

- `GROUP BY` groups rows that contain the same values.
- Aggregate functions are commonly used with `GROUP BY`.
- `HAVING` filters grouped results.
- `EXISTS` checks whether a subquery returns records.
- `ANY` requires at least one comparison to satisfy the condition.
- `ALL` compares against every value returned by the subquery.
- A subquery is a query contained inside another query.
- `SELECT INTO` creates a new table from selected data.
- `INSERT INTO SELECT` inserts selected data into an existing table.
- `CASE` evaluates conditions and returns a corresponding result.
