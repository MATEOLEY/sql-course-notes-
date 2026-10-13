# Databases and Tables

This section covers SQL commands used to create, view, back up, modify, and delete databases and tables.

Topics covered:

```text
CREATE DATABASE
DROP DATABASE
BACKUP DATABASE
SHOW DATABASES
CREATE TABLE
SQL Data Types
DROP TABLE
TRUNCATE TABLE
ALTER TABLE
```

---

# CREATE DATABASE

The `CREATE DATABASE` statement is used to create a new database.

Basic syntax:

```sql
CREATE DATABASE database_name;
```

Example:

```sql
CREATE DATABASE testDB;
```

---

# Viewing Databases

The syntax used to display databases depends on the database management system.

## SQL Server

```sql
SELECT name
FROM sys.databases;
```

## MySQL

```sql
SHOW DATABASES;
```

This is an example of how SQL syntax can vary between database systems.

---

# DROP DATABASE

The `DROP DATABASE` statement deletes an existing database.

Basic syntax:

```sql
DROP DATABASE database_name;
```

Example:

```sql
DROP DATABASE testDB;
```

> `DROP DATABASE` removes the database and its contents.

---

# BACKUP DATABASE

A database backup creates a copy of a database that can be used for recovery.

The course notes show the following SQL Server-style syntax:

```sql
BACKUP DATABASE database_name
TO DISK = 'filepath';
```

Example structure:

```sql
BACKUP DATABASE testDB
TO DISK = 'D:\backups\testDB.bak';
```

---

## Differential Backup

The course also introduces differential backups.

A differential backup stores changes made since the previous full backup.

Basic syntax:

```sql
BACKUP DATABASE database_name
TO DISK = 'filepath'
WITH DIFFERENTIAL;
```

Conceptually:

```text
Full Backup
    ↓
Database changes
    ↓
Differential Backup
```

---

# CREATE TABLE

The `CREATE TABLE` statement creates a new table in a database.

Basic syntax:

```sql
CREATE TABLE table_name (
    column1 datatype constraint,
    column2 datatype constraint,
    column3 datatype constraint
);
```

Example:

```sql
CREATE TABLE Persons (
    PersonID INT,
    LastName VARCHAR(255),
    FirstName VARCHAR(255),
    Address VARCHAR(255),
    City VARCHAR(255)
);
```

Each column definition can include:

```text
Column name
Data type
Optional constraint
```

---

# Create a Table from Another Table

The course notes also show that a new table can be created using data from an existing table.

Basic structure:

```sql
CREATE TABLE new_table AS
SELECT column1, column2
FROM existing_table
WHERE condition;
```

This creates a new table based on the result of the `SELECT` statement.

---

# Common SQL Data Types

Different data types determine what kind of information a column can store.

| Data Type | Purpose |
|---|---|
| `INT` | Stores whole numbers |
| `VARCHAR(n)` | Stores variable-length text |
| `CHAR(n)` | Stores fixed-length text |
| `DATE` | Stores a date without time |
| `DATETIME` | Stores both date and time |
| `TIMESTAMP` | Stores date/time-related values depending on the SQL system |
| `BOOLEAN` | Represents true or false values |
| `TEXT` | Stores longer text |

Example:

```sql
CREATE TABLE Users (
    UserID INT,
    Username VARCHAR(50),
    Country CHAR(2),
    BirthDate DATE
);
```

---

# DROP TABLE

The `DROP TABLE` statement removes an existing table.

Basic syntax:

```sql
DROP TABLE table_name;
```

Some SQL implementations also support:

```sql
DROP TABLE IF EXISTS table_name;
```

This checks whether the table exists before attempting to remove it.

---

# TRUNCATE TABLE

`TRUNCATE TABLE` removes the data contained inside a table.

Basic syntax:

```sql
TRUNCATE TABLE table_name;
```

The table itself remains available after its data is removed.

---

# DELETE vs TRUNCATE vs DROP

These commands should not be confused.

```text
DELETE
→ Removes rows

TRUNCATE TABLE
→ Removes the data from the table

DROP TABLE
→ Removes the entire table
```

---

# ALTER TABLE

The `ALTER TABLE` statement is used to add, delete, or modify columns in an existing table.

Basic structure:

```sql
ALTER TABLE table_name
operation;
```

Operations covered in the course notes include:

```text
Add Column
Drop Column
Rename Column
Modify Column
Add Constraint
Remove Constraint
```

---

## Add a Column

Example structure:

```sql
ALTER TABLE table_name
ADD column_name datatype;
```

Example:

```sql
ALTER TABLE Persons
ADD Email VARCHAR(255);
```

---

## Drop a Column

Example structure:

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

Example:

```sql
ALTER TABLE Persons
DROP COLUMN Email;
```

---

## Modify a Column

`ALTER TABLE` can also be used to change the definition of an existing column.

The exact syntax may depend on the SQL implementation being used.

Conceptually:

```text
ALTER TABLE
    ↓
Select table
    ↓
Modify column definition
```

---

# Database vs Table

A database can contain multiple tables.

Conceptually:

```text
Database
│
├── Customers
├── Products
├── Orders
└── Employees
```

Each table contains:

```text
Columns
+
Rows
```

Example:

```text
Customers

CustomerID | CustomerName | Country
-----------|--------------|---------
1          | Mateo        | Colombia
2          | Samuel       | Colombia
```

---

# Quick Reference

| Command | Purpose |
|---|---|
| `CREATE DATABASE` | Create a database |
| `DROP DATABASE` | Delete a database |
| `BACKUP DATABASE` | Create a database backup |
| `SHOW DATABASES` | Display databases in MySQL |
| `CREATE TABLE` | Create a table |
| `DROP TABLE` | Delete a table |
| `TRUNCATE TABLE` | Remove data from a table |
| `ALTER TABLE` | Modify a table |
| `ADD` | Add a column |
| `DROP COLUMN` | Remove a column |

---

# Example Database Workflow

```sql
CREATE DATABASE StoreDB;
```

```sql
CREATE TABLE Customers (
    CustomerID INT,
    CustomerName VARCHAR(255),
    City VARCHAR(255)
);
```

Later, the table structure can be modified:

```sql
ALTER TABLE Customers
ADD Email VARCHAR(255);
```

The data can be removed while keeping the table:

```sql
TRUNCATE TABLE Customers;
```

Or the table itself can be removed:

```sql
DROP TABLE Customers;
```

---

## Notes

- `CREATE DATABASE` creates a new database.
- `DROP DATABASE` removes a database.
- Database backup syntax may depend on the database management system.
- `CREATE TABLE` defines a table and its columns.
- Every column has a data type.
- `DROP TABLE` removes the complete table.
- `TRUNCATE TABLE` removes the table's data while keeping the table itself.
- `ALTER TABLE` modifies an existing table.
- SQL syntax may vary between SQL Server, MySQL, and other database systems.
