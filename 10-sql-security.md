# SQL Security

This section covers basic SQL security concepts introduced in the course.

The main topics are:

```text
SQL Injection
SQL Parameters
Prepared Statements
```

The main idea is to avoid treating user input as executable SQL code.

---

# SQL Injection

**SQL Injection** is a security vulnerability that can occur when user-controlled input is included directly inside an SQL query.

An attacker may attempt to provide input that changes the intended behavior of the SQL statement.

Conceptually:

```text
User Input
    ↓
Application
    ↓
SQL Query
    ↓
Database
```

If user input is inserted directly into the query without proper protection, the input may be interpreted as part of the SQL command.

---

## Why SQL Injection Is Dangerous

A successful SQL Injection vulnerability may allow unintended interaction with a database.

The main security problem is that:

```text
User data
```

and:

```text
SQL instructions
```

should not be treated as the same thing.

Applications should clearly separate the SQL query structure from the values provided by users.

---

# Unsafe Query Construction

A risky approach is building an SQL query by directly combining SQL code with user input.

Conceptually:

```text
SQL Query + User Input
        ↓
   One SQL String
```

The application may then be unable to distinguish between:

```text
Expected user data
```

and:

```text
SQL syntax introduced through the input
```

This can create an SQL Injection vulnerability.

---

# SQL Parameters

SQL parameters are used to safely provide values to SQL queries.

Instead of inserting user input directly into the SQL statement, the query contains parameters.

Conceptually:

```text
SQL Statement
     +
Parameter Values
     ↓
Database
```

The SQL statement and the user-provided values remain separated.

---

## Parameterized Query Concept

Instead of constructing a query directly from user input:

```text
User input
    ↓
Concatenate into SQL
    ↓
Execute
```

a parameterized query follows this structure:

```text
SQL statement with parameter
            +
      Parameter value
            ↓
          Execute
```

This helps prevent user input from being interpreted as SQL instructions.

---

# Prepared Statements

A **prepared statement** is an SQL statement that is prepared before user-supplied values are provided.

The query structure is defined first.

The values are then supplied separately.

Conceptually:

```text
1. Prepare SQL statement
        ↓
2. Bind parameters
        ↓
3. Provide values
        ↓
4. Execute statement
```

Prepared statements are an important technique for helping prevent SQL Injection.

---

# Prepared Statement Workflow

A prepared statement commonly follows this process:

```text
Prepare
   ↓
Bind
   ↓
Execute
```

### 1. Prepare

The SQL statement is created using placeholders instead of inserting the values directly.

Conceptually:

```sql
INSERT INTO table_name (column1, column2)
VALUES (?, ?);
```

The `?` characters represent values that will be supplied later.

---

### 2. Bind Parameters

The application associates values with the placeholders.

Conceptually:

```text
? → First value
? → Second value
```

The values remain separate from the SQL statement itself.

---

### 3. Execute

After the parameters are provided, the prepared statement is executed.

```text
Prepared SQL
     +
Parameters
     ↓
Execute
```

---

# Prepared Statements and User Input

Prepared statements are especially useful when a query contains values received from users.

For example, an application may receive:

```text
First Name
Last Name
Email
Username
```

Instead of manually inserting these values into the SQL query, they can be passed as parameters.

This reduces the risk that the provided values will be interpreted as SQL commands.

---

# Parameters vs Direct String Construction

Conceptually:

```text
Direct Construction

SQL + User Input
       ↓
Combined Query
```

Compared with:

```text
Parameterized Query

SQL Structure
     +
Parameter Values
     ↓
Database
```

The second approach keeps:

```text
SQL code
```

and:

```text
User data
```

separate.

---

# SQL Injection Prevention

The course introduces two closely related approaches for reducing SQL Injection risk:

```text
SQL Parameters
Prepared Statements
```

The key principle is:

> User-controlled data should be treated as data, not as SQL instructions.

---

# Security Mindset

When an application communicates with a database, input received from users should not automatically be trusted.

Conceptually:

```text
User Input
    ↓
Treat as Data
    ↓
Use Parameters
    ↓
Execute Query
```

Instead of:

```text
User Input
    ↓
Insert directly into SQL
    ↓
Execute
```

---

# Quick Reference

| Concept | Purpose |
|---|---|
| SQL Injection | Vulnerability caused by unsafe interaction between user input and SQL queries |
| SQL Parameter | Represents a value supplied separately from the SQL statement |
| Prepared Statement | SQL statement prepared before parameter values are supplied |
| Placeholder | Position where a parameter value will be used |
| Parameterized Query | Query where SQL code and input values remain separated |

---

# Prepared Statement Summary

```text
Prepare Query
     ↓
Use Placeholders
     ↓
Bind Values
     ↓
Execute
```

The important distinction is:

```text
SQL Code ≠ User Data
```

---

## Notes

- SQL Injection can occur when user input is handled unsafely inside SQL queries.
- User input should not be treated as SQL code.
- SQL parameters keep input values separate from the SQL statement.
- Prepared statements define the SQL structure before supplying values.
- Prepared statements use parameters or placeholders for data.
- Parameterized queries are an important defense against SQL Injection.
- Values received from users should be handled as data rather than executable SQL instructions.
