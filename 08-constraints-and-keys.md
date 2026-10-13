# SQL Constraints and Keys

SQL constraints are rules applied to table columns to control which data can be stored.

Constraints help maintain:

```text
Data integrity
Consistency
Uniqueness
Relationships between tables
```

The constraints covered in this course are:

```text
NOT NULL
UNIQUE
PRIMARY KEY
FOREIGN KEY
CHECK
DEFAULT
```

---

# NOT NULL

The `NOT NULL` constraint prevents a column from containing `NULL` values.

Example:

```sql
CREATE TABLE Persons (
    ID INT NOT NULL,
    LastName VARCHAR(255) NOT NULL,
    FirstName VARCHAR(255) NOT NULL,
    Age INT
);
```

In this example:

```text
ID        → Cannot be NULL
LastName  → Cannot be NULL
FirstName → Cannot be NULL
Age       → Can be NULL
```

---

## Add NOT NULL with ALTER TABLE

A column definition can also be modified after the table has been created.

The exact syntax depends on the database management system.

Conceptually:

```sql
ALTER TABLE table_name
MODIFY column_name datatype NOT NULL;
```

> `ALTER TABLE` syntax can differ between MySQL, SQL Server, PostgreSQL, and other database systems.

---

# UNIQUE

The `UNIQUE` constraint ensures that values in a column are unique.

Example:

```sql
CREATE TABLE Persons (
    ID INT NOT NULL,
    LastName VARCHAR(255) NOT NULL,
    FirstName VARCHAR(255),
    Age INT,
    Email VARCHAR(255) UNIQUE
);
```

This prevents two rows from using the same value in the `Email` column.

---

## Named UNIQUE Constraint

A constraint can also be given a name.

Example:

```sql
CREATE TABLE Persons (
    ID INT NOT NULL,
    LastName VARCHAR(255),
    FirstName VARCHAR(255),
    Age INT,
    CONSTRAINT UC_Person UNIQUE (ID, LastName)
);
```

This creates a named `UNIQUE` constraint across multiple columns.

---

## Add UNIQUE with ALTER TABLE

Example:

```sql
ALTER TABLE Persons
ADD UNIQUE (Age);
```

A named constraint can also be used:

```sql
ALTER TABLE Persons
ADD CONSTRAINT UC_Person UNIQUE (ID, LastName);
```

---

# PRIMARY KEY

A `PRIMARY KEY` uniquely identifies each row in a table.

A primary key must contain unique values and cannot contain `NULL`.

A table can have only one primary key constraint, although that key can contain multiple columns.

Example:

```sql
CREATE TABLE Persons (
    ID INT PRIMARY KEY,
    LastName VARCHAR(255) NOT NULL,
    FirstName VARCHAR(255),
    Age INT
);
```

Here:

```text
ID → Primary Key
```

Each row must therefore have a unique `ID`.

---

## Named PRIMARY KEY

A primary key can also be defined as a named table constraint.

```sql
CREATE TABLE Persons (
    ID INT NOT NULL,
    LastName VARCHAR(255) NOT NULL,
    FirstName VARCHAR(255),
    Age INT,
    CONSTRAINT PK_Person PRIMARY KEY (ID)
);
```

---

# Composite Primary Key

A primary key can contain multiple columns.

Example:

```sql
CREATE TABLE Persons (
    ID INT NOT NULL,
    LastName VARCHAR(255) NOT NULL,
    FirstName VARCHAR(255),
    Age INT,
    CONSTRAINT PK_Person PRIMARY KEY (ID, LastName)
);
```

This is known as a:

```text
Composite Primary Key
```

The combination of:

```text
ID + LastName
```

must be unique.

---

## Add PRIMARY KEY with ALTER TABLE

Example:

```sql
ALTER TABLE Persons
ADD PRIMARY KEY (ID);
```

For multiple columns:

```sql
ALTER TABLE Persons
ADD CONSTRAINT PK_Person PRIMARY KEY (ID, LastName);
```

---

# FOREIGN KEY

A `FOREIGN KEY` creates a relationship between two tables.

It references a key in another table.

Conceptually:

```text
Parent Table
     │
     │ Primary Key
     ↓
Child Table
     │
     └── Foreign Key
```

Example tables:

```text
Persons
-------
PersonID
LastName
FirstName

Orders
------
OrderID
OrderNumber
PersonID
```

`Persons.PersonID` can be the primary key.

`Orders.PersonID` can reference it as a foreign key.

---

## FOREIGN KEY Example

```sql
CREATE TABLE Persons (
    PersonID INT PRIMARY KEY,
    LastName VARCHAR(255),
    FirstName VARCHAR(255)
);
```

Then:

```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    OrderNumber INT NOT NULL,
    PersonID INT,
    CONSTRAINT FK_PersonOrder
        FOREIGN KEY (PersonID)
        REFERENCES Persons(PersonID)
);
```

The relationship is:

```text
Persons.PersonID
        ↑
        │
Orders.PersonID
```

This helps maintain **referential integrity** between the tables.

---

## Add FOREIGN KEY with ALTER TABLE

A foreign key can also be added after creating the table.

```sql
ALTER TABLE Orders
ADD CONSTRAINT FK_PersonOrder
FOREIGN KEY (PersonID)
REFERENCES Persons(PersonID);
```

---

## Drop a FOREIGN KEY Constraint

Named constraints can be removed later.

The exact command depends on the database system.

Conceptually:

```sql
ALTER TABLE table_name
DROP CONSTRAINT constraint_name;
```

Example:

```sql
ALTER TABLE Orders
DROP CONSTRAINT FK_PersonOrder;
```

> Some database systems use different syntax for dropping foreign keys.

---

# CHECK

The `CHECK` constraint restricts values based on a condition.

Example:

```sql
CREATE TABLE Persons (
    ID INT PRIMARY KEY,
    LastName VARCHAR(255) NOT NULL,
    FirstName VARCHAR(255),
    Age INT CHECK (Age >= 18)
);
```

This condition requires:

```text
Age >= 18
```

If the inserted value does not satisfy the condition, the database rejects it.

---

## Named CHECK Constraint

A `CHECK` constraint can also be named.

Example:

```sql
CREATE TABLE Persons (
    ID INT PRIMARY KEY,
    LastName VARCHAR(255) NOT NULL,
    FirstName VARCHAR(255),
    Age INT,
    City VARCHAR(255),

    CONSTRAINT CHK_Person
    CHECK (Age >= 18 AND City = 'Bogota')
);
```

---

## Add CHECK with ALTER TABLE

Example:

```sql
ALTER TABLE Persons
ADD CHECK (Age >= 18);
```

A named constraint can also be added:

```sql
ALTER TABLE Persons
ADD CONSTRAINT CHK_Person
CHECK (Age >= 18);
```

---

# DEFAULT

The `DEFAULT` constraint provides a default value when no value is specified for a column.

Example:

```sql
CREATE TABLE Persons (
    ID INT PRIMARY KEY,
    LastName VARCHAR(255) NOT NULL,
    FirstName VARCHAR(255),
    Age INT,
    City VARCHAR(255) DEFAULT 'Bogota'
);
```

If no city is provided, the database can use:

```text
Bogota
```

as the default value.

---

## DEFAULT Example

Consider:

```sql
INSERT INTO Persons (ID, LastName, FirstName, Age)
VALUES (1, 'Leyva', 'Mateo', 23);
```

No value was provided for:

```text
City
```

Because the column has:

```sql
DEFAULT 'Bogota'
```

the resulting row can contain:

```text
City = Bogota
```

---

## Add DEFAULT with ALTER TABLE

Default-constraint syntax differs between database systems.

Conceptually, the goal is:

```text
Select table
    ↓
Select column
    ↓
Assign default value
```

> Always check the syntax for the specific database system being used.

---

# Constraint Naming

Constraints can optionally have names.

Example:

```sql
CONSTRAINT PK_Person
PRIMARY KEY (ID)
```

The name:

```text
PK_Person
```

makes the constraint easier to identify and manage later.

Common naming examples:

```text
PK_Person      → Primary Key
FK_PersonOrder → Foreign Key
UC_Person      → Unique Constraint
CHK_Person     → Check Constraint
```

Constraint names are especially useful when a constraint needs to be modified or removed.

---

# Primary Key vs Foreign Key

| Primary Key | Foreign Key |
|---|---|
| Identifies a row uniquely | Creates a relationship with another table |
| Must be unique | Values can repeat |
| Cannot be NULL | May allow NULL depending on its definition |
| Defined in its own table | References a key in another table |

Conceptually:

```text
Customers
---------
CustomerID  ← PRIMARY KEY


Orders
------
OrderID
CustomerID  ← FOREIGN KEY
                 │
                 └── References Customers.CustomerID
```

---

# UNIQUE vs PRIMARY KEY

Both can enforce uniqueness, but they serve different purposes.

```text
PRIMARY KEY
→ Main identifier for each row

UNIQUE
→ Prevent duplicate values in another column or set of columns
```

Example:

```text
PersonID → PRIMARY KEY
Email    → UNIQUE
```

---

# Quick Reference

| Constraint | Purpose |
|---|---|
| `NOT NULL` | Prevent NULL values |
| `UNIQUE` | Prevent duplicate values |
| `PRIMARY KEY` | Uniquely identify each row |
| `FOREIGN KEY` | Create relationships between tables |
| `CHECK` | Restrict values using a condition |
| `DEFAULT` | Provide a value when none is specified |

---

# Example Table

Several constraints can be combined in the same table.

```sql
CREATE TABLE Users (
    UserID INT PRIMARY KEY,
    Username VARCHAR(100) NOT NULL,
    Email VARCHAR(255) UNIQUE,
    Age INT CHECK (Age >= 18),
    City VARCHAR(100) DEFAULT 'Bogota'
);
```

This means:

```text
UserID
→ Unique identifier

Username
→ Required

Email
→ Cannot be duplicated

Age
→ Must satisfy the CHECK condition

City
→ Defaults to Bogota when no value is provided
```

---

## Notes

- Constraints define rules for the data stored in tables.
- `NOT NULL` prevents missing values.
- `UNIQUE` prevents duplicate values.
- `PRIMARY KEY` uniquely identifies rows.
- A table has one primary key constraint, but it can contain multiple columns.
- A primary key containing multiple columns is called a composite primary key.
- `FOREIGN KEY` creates relationships between tables.
- Foreign keys help maintain referential integrity.
- `CHECK` validates data against a condition.
- `DEFAULT` provides a predefined value when one is not supplied.
- Constraints can be created together with a table or added later with `ALTER TABLE`.
- Some constraint syntax differs between database management systems.
