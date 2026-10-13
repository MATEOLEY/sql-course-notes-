# Indexes, Auto Increment, Views and Stored Procedures

This section covers SQL features used to improve data access, automatically generate identifiers, create virtual tables, and store reusable SQL logic.

Topics covered:

```text
CREATE INDEX
CREATE UNIQUE INDEX
AUTO_INCREMENT
IDENTITY
SQL Dates
CREATE VIEW
ALTER VIEW
DROP VIEW
Stored Procedures
EXEC
DROP PROCEDURE
```

---

# SQL Indexes

Indexes are used to help retrieve data from a database more efficiently.

They can improve the speed of queries that search or filter data.

Basic syntax:

```sql
CREATE INDEX index_name
ON table_name (column1, column2);
```

Example:

```sql
CREATE INDEX idx_lastname
ON Persons (LastName);
```

---

## Index on Multiple Columns

An index can contain more than one column.

Example:

```sql
CREATE INDEX idx_name
ON Persons (LastName, FirstName);
```

---

# UNIQUE INDEX

A unique index does not allow duplicate values in the indexed column or combination of columns.

Basic syntax:

```sql
CREATE UNIQUE INDEX index_name
ON table_name (column1);
```

Example:

```sql
CREATE UNIQUE INDEX idx_email
ON Customers (Email);
```

Conceptually:

```text
Regular Index
→ Helps improve data retrieval

Unique Index
→ Helps improve retrieval
+
Prevents duplicate indexed values
```

---

# DROP INDEX

An index can be removed when it is no longer needed.

The exact syntax for deleting an index depends on the database management system.

Because SQL Server, MySQL, and other systems may use different syntax, always verify which SQL implementation is being used before dropping an index.

---

# AUTO INCREMENT

Auto increment is used to automatically generate a new numeric value when a new row is inserted.

It is commonly used with primary key columns.

Example concept:

```text
First row  → ID 1
Second row → ID 2
Third row  → ID 3
```

---

## MySQL - AUTO_INCREMENT

MySQL uses:

```sql
AUTO_INCREMENT
```

Example:

```sql
CREATE TABLE Persons (
    PersonID INT NOT NULL AUTO_INCREMENT,
    LastName VARCHAR(255) NOT NULL,
    FirstName VARCHAR(255),
    Age INT,
    PRIMARY KEY (PersonID)
);
```

When a row is inserted without manually specifying `PersonID`, MySQL automatically generates the value.

By default, the sequence commonly starts at:

```text
1
```

and increases for new records.

---

## Change AUTO_INCREMENT Starting Value

The course notes also show that the next auto increment value can be modified.

Example:

```sql
ALTER TABLE Persons
AUTO_INCREMENT = 100;
```

This changes the next generated value.

---

# SQL Server - IDENTITY

SQL Server uses:

```sql
IDENTITY
```

for auto-generated numeric values.

Example:

```sql
CREATE TABLE Persons (
    PersonID INT IDENTITY(1,1) PRIMARY KEY,
    LastName VARCHAR(255) NOT NULL,
    FirstName VARCHAR(255),
    Age INT
);
```

Conceptually:

```text
IDENTITY(1,1)

First value → 1
Increment   → 1
```

---

# SQL Dates

SQL database systems provide data types for storing date and time information.

Common date-related types include:

```text
DATE
DATETIME
TIMESTAMP
TIME
```

The exact available data types and their behavior depend on the database management system.

---

## DATE

`DATE` stores a date.

Example format:

```text
YYYY-MM-DD
```

Example:

```text
2026-10-13
```

---

## DATETIME

`DATETIME` stores both a date and a time.

Conceptually:

```text
Date + Time
```

Example:

```text
2026-10-13 17:30:00
```

---

## Important Date Note

Different database systems may support different date and time data types.

For example:

```text
MySQL
SQL Server
```

do not have exactly the same set of date types or behavior.

Always verify the SQL implementation being used.

---

# SQL Views

A **view** is a virtual table based on the result of a SQL query.

A view can be created from one or more database tables.

Instead of repeatedly writing the same query, a view can provide a reusable way to access its result.

---

## CREATE VIEW

Basic syntax:

```sql
CREATE VIEW view_name AS
SELECT column1, column2
FROM table_name
WHERE condition;
```

Example:

```sql
CREATE VIEW CustomersFromBogota AS
SELECT CustomerID, CustomerName
FROM Customers
WHERE City = 'Bogota';
```

The view can then be queried similarly to a table:

```sql
SELECT *
FROM CustomersFromBogota;
```

---

## ALTER VIEW

An existing view can be modified.

Basic structure:

```sql
ALTER VIEW view_name AS
SELECT column1, column2
FROM table_name
WHERE condition;
```

Example:

```sql
ALTER VIEW CustomersFromBogota AS
SELECT CustomerID, CustomerName, City
FROM Customers
WHERE City = 'Bogota';
```

---

## DROP VIEW

A view can be removed using:

```sql
DROP VIEW view_name;
```

Example:

```sql
DROP VIEW CustomersFromBogota;
```

---

# Stored Procedures

A **stored procedure** is prepared SQL code that can be saved and reused.

Instead of rewriting the same SQL statements repeatedly, the procedure can be executed when needed.

Stored procedures can also receive parameters.

---

## SQL Server Stored Procedure

Basic structure:

```sql
CREATE PROCEDURE procedure_name
    @parameter1 datatype,
    @parameter2 datatype
AS
BEGIN
    -- SQL statements
END;
```

Example:

```sql
CREATE PROCEDURE GetCustomersByCity
    @City VARCHAR(50)
AS
BEGIN
    SELECT *
    FROM Customers
    WHERE City = @City;
END;
```

The procedure stores the query under the name:

```text
GetCustomersByCity
```

and accepts:

```text
@City
```

as a parameter.

---

# Execute a Stored Procedure

In SQL Server, a stored procedure can be executed using:

```sql
EXEC procedure_name;
```

If the procedure contains parameters:

```sql
EXEC GetCustomersByCity @City = 'Bogota';
```

Conceptually:

```text
Stored Procedure
      ↓
Receive parameter
      ↓
Execute stored SQL
      ↓
Return result
```

---

# Stored Procedure Parameters

Parameters allow values to be passed to a procedure when it is executed.

Example:

```sql
CREATE PROCEDURE GetCustomersByCity
    @City VARCHAR(50)
AS
BEGIN
    SELECT CustomerID, CustomerName
    FROM Customers
    WHERE City = @City;
END;
```

Then:

```sql
EXEC GetCustomersByCity @City = 'Bogota';
```

The same procedure can later be reused with another value:

```sql
EXEC GetCustomersByCity @City = 'Medellin';
```

---

# DROP PROCEDURE

A stored procedure can be deleted when it is no longer required.

Example:

```sql
DROP PROCEDURE GetCustomersByCity;
```

Some SQL implementations also support checking whether the procedure exists before removing it.

---

# View vs Stored Procedure

Although both can store reusable database logic, they serve different purposes.

```text
VIEW
→ Represents the result of a query as a virtual table

STORED PROCEDURE
→ Stores SQL statements that can be executed
```

A view is normally queried with:

```sql
SELECT *
FROM view_name;
```

A stored procedure is executed:

```sql
EXEC procedure_name;
```

---

# Index vs View vs Stored Procedure

```text
INDEX
→ Helps improve data retrieval

VIEW
→ Saves a query as a virtual table

STORED PROCEDURE
→ Saves SQL logic that can be executed
```

---

# Quick Reference

| Feature | Purpose |
|---|---|
| `CREATE INDEX` | Create an index |
| `CREATE UNIQUE INDEX` | Create an index that prevents duplicate indexed values |
| `AUTO_INCREMENT` | Automatically generate numeric values in MySQL |
| `IDENTITY` | Automatically generate numeric values in SQL Server |
| `DATE` | Store a date |
| `DATETIME` | Store a date and time |
| `CREATE VIEW` | Create a virtual table from a query |
| `ALTER VIEW` | Modify a view |
| `DROP VIEW` | Delete a view |
| `CREATE PROCEDURE` | Create a stored procedure |
| `EXEC` | Execute a stored procedure in SQL Server |
| `DROP PROCEDURE` | Delete a stored procedure |

---

## Examples

### Create an index

```sql
CREATE INDEX idx_lastname
ON Persons (LastName);
```

### Create a unique index

```sql
CREATE UNIQUE INDEX idx_email
ON Customers (Email);
```

### MySQL auto increment

```sql
PersonID INT AUTO_INCREMENT PRIMARY KEY
```

### SQL Server identity

```sql
PersonID INT IDENTITY(1,1) PRIMARY KEY
```

### Create a view

```sql
CREATE VIEW CustomersFromBogota AS
SELECT CustomerID, CustomerName
FROM Customers
WHERE City = 'Bogota';
```

### Execute a procedure

```sql
EXEC GetCustomersByCity @City = 'Bogota';
```

---

## Notes

- Indexes can improve data retrieval performance.
- A unique index also prevents duplicate indexed values.
- MySQL uses `AUTO_INCREMENT`.
- SQL Server uses `IDENTITY` for automatically generated numeric values.
- SQL date types vary between database systems.
- A view is based on a SQL query and behaves like a virtual table.
- Views can be created, modified, and removed.
- Stored procedures save SQL code that can be executed again.
- Stored procedures can receive parameters.
- Stored procedure syntax differs between database systems.
