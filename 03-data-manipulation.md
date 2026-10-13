# Data Manipulation

This section covers SQL commands used to insert, modify, and remove data from database tables.

The main commands covered are:

```text
INSERT INTO
UPDATE
DELETE
DROP TABLE
```

---

# INSERT INTO

The `INSERT INTO` statement is used to add new rows to a table.

Basic syntax:

```sql
INSERT INTO table_name (column1, column2, column3)
VALUES (value1, value2, value3);
```

Example:

```sql
INSERT INTO Customers (Name, Age, City)
VALUES ('Mateo', 23, 'Bogota');
```

The columns specified in the first section correspond to the values specified inside `VALUES`.

Conceptually:

```text
Name   → Mateo
Age    → 23
City   → Bogota
```

---

## Insert Multiple Rows

Multiple rows can be inserted by adding additional value groups.

Example:

```sql
INSERT INTO Customers (Name, Age, City)
VALUES
('Mateo', 23, 'Bogota'),
('Samuel', 24, 'Medellin'),
('Daniel', 22, 'Cali');
```

---

# UPDATE

The `UPDATE` statement is used to modify existing information in a table.

Basic syntax:

```sql
UPDATE table_name
SET column1 = value1,
    column2 = value2
WHERE condition;
```

Example:

```sql
UPDATE Customers
SET Email = 'new@email.com'
WHERE CustomerID = 1;
```

This changes the selected information only for the rows that match the `WHERE` condition.

---

## Updating Multiple Columns

Multiple columns can be modified in the same statement.

Example:

```sql
UPDATE Customers
SET City = 'Bogota',
    Age = 24
WHERE CustomerID = 1;
```

---

## Importance of WHERE with UPDATE

The `WHERE` clause determines which rows will be modified.

For example:

```sql
UPDATE Customers
SET City = 'Bogota'
WHERE CustomerID = 1;
```

Only the matching row is updated.

If the `WHERE` clause is omitted:

```sql
UPDATE Customers
SET City = 'Bogota';
```

the change applies to all rows in the table.

> Always verify the `WHERE` condition before running an `UPDATE` statement.

---

# DELETE

The `DELETE` statement removes rows from a table.

Basic syntax:

```sql
DELETE FROM table_name
WHERE condition;
```

Example:

```sql
DELETE FROM Customers
WHERE CustomerName = 'Mateo';
```

Only rows matching the condition are removed.

---

## DELETE Without WHERE

If the `WHERE` clause is omitted:

```sql
DELETE FROM Customers;
```

all rows in the table are removed.

The table itself still exists.

Its structure, such as its columns, remains in the database.

> Be especially careful when using `DELETE` without a `WHERE` clause.

---

# DELETE vs DROP TABLE

`DELETE` removes data from a table.

```sql
DELETE FROM Customers;
```

The table still exists.

`DROP TABLE` removes the table itself.

```sql
DROP TABLE Customers;
```

Conceptually:

```text
DELETE
   ↓
Remove rows
   ↓
Keep table structure
```

```text
DROP TABLE
   ↓
Remove the entire table
```

---

# Common Workflow

A typical data manipulation workflow may look like:

```text
INSERT
   ↓
Add data

UPDATE
   ↓
Modify data

DELETE
   ↓
Remove data
```

---

# Quick Reference

| Command | Purpose |
|---|---|
| `INSERT INTO` | Add new rows |
| `VALUES` | Specify values to insert |
| `UPDATE` | Modify existing rows |
| `SET` | Specify new values |
| `WHERE` | Select which rows are affected |
| `DELETE` | Remove rows |
| `DROP TABLE` | Remove an entire table |

---

## Examples

### Insert data

```sql
INSERT INTO Customers (Name, Age, City)
VALUES ('Mateo', 23, 'Bogota');
```

### Update data

```sql
UPDATE Customers
SET City = 'Medellin'
WHERE CustomerID = 1;
```

### Delete a row

```sql
DELETE FROM Customers
WHERE CustomerID = 1;
```

### Delete all rows

```sql
DELETE FROM Customers;
```

### Delete the table

```sql
DROP TABLE Customers;
```

---

## Important Notes

- `INSERT INTO` adds new records to a table.
- `UPDATE` modifies existing records.
- `SET` specifies the new values in an `UPDATE`.
- `WHERE` determines which rows are affected.
- An `UPDATE` without `WHERE` affects all rows.
- A `DELETE` without `WHERE` removes all rows.
- `DELETE` removes data but keeps the table.
- `DROP TABLE` removes the entire table.
- Always verify the condition before executing commands that modify or delete data.
