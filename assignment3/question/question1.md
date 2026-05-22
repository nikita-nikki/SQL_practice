# Convert Multiple Rows Into One Comma-Separated Line in PostgreSQL

## Table Data

| full_name |
|------------|
| amit kumar |
| arvind singh |

---

## Required Output

```text
amit kumar, arvind singh

Query
SELECT STRING_AGG(full_name, ', ') AS names
FROM users;

```
Explanation
STRING_AGG()

STRING_AGG() is an aggregate function in PostgreSQL used to combine multiple rows into a single string.

Syntax
STRING_AGG(column_name, separator)
column_name → values to combine
separator → text inserted between values