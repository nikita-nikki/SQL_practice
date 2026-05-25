# Understanding SQL Query Execution Order with a Complex Query

## Goal

The purpose of this example is to understand:

- how SQL queries are written
- how SQL actually executes them internally
- logical execution order
- use of multiple clauses together

---

# Example Tables

## employees

| emp_id | full_name | dept_id | salary | city |
|---|---|---|---|---|
| 1 | Amit Kumar | 101 | 70000 | Lucknow |
| 2 | Neha Sharma | 102 | 50000 | Delhi |
| 3 | Om Verma | 101 | 80000 | Lucknow |
| 4 | Ravi Singh | 103 | 45000 | Mumbai |

---

## departments

| dept_id | dept_name |
|---|---|
| 101 | Engineering |
| 102 | HR |
| 103 | Marketing |

---

# Complex Query

```sql
SELECT 
    d.dept_name,
    COUNT(e.emp_id) AS total_employees,
    AVG(e.salary) AS avg_salary,
    MAX(e.salary) AS highest_salary
FROM employees e
INNER JOIN departments d
    ON e.dept_id = d.dept_id
WHERE e.salary > 40000
    AND LOWER(e.city) = 'lucknow'
GROUP BY d.dept_name
HAVING AVG(e.salary) > 60000
ORDER BY avg_salary DESC
LIMIT 5;
```

---

# Most Important Concept

SQL query is written in one order,

BUT

executed internally in another order.

---

# Actual SQL Execution Sequence

```text
FROM
JOIN
ON
WHERE
GROUP BY
HAVING
SELECT
ORDER BY
LIMIT
```

---

# Step-by-Step Internal Execution

---

# Step 1 → FROM

```sql
FROM employees e
```

Database first loads the `employees` table.

Intermediate result:

| emp_id | full_name | dept_id | salary | city |
|---|---|---|---|---|
| 1 | Amit Kumar | 101 | 70000 | Lucknow |
| 2 | Neha Sharma | 102 | 50000 | Delhi |
| 3 | Om Verma | 101 | 80000 | Lucknow |
| 4 | Ravi Singh | 103 | 45000 | Mumbai |

---

# Step 2 → INNER JOIN

```sql
INNER JOIN departments d
ON e.dept_id = d.dept_id
```

Tables are joined using matching `dept_id`.

Intermediate result:

| emp_id | full_name | dept_name | salary | city |
|---|---|---|---|---|
| 1 | Amit Kumar | Engineering | 70000 | Lucknow |
| 2 | Neha Sharma | HR | 50000 | Delhi |
| 3 | Om Verma | Engineering | 80000 | Lucknow |
| 4 | Ravi Singh | Marketing | 45000 | Mumbai |

---

# Step 3 → WHERE

```sql
WHERE e.salary > 40000
AND LOWER(e.city) = 'lucknow'
```

Filtering happens row by row.

Remaining rows:

| emp_id | full_name | dept_name | salary | city |
|---|---|---|---|---|
| 1 | Amit Kumar | Engineering | 70000 | Lucknow |
| 3 | Om Verma | Engineering | 80000 | Lucknow |

---

# Step 4 → GROUP BY

```sql
GROUP BY d.dept_name
```

Rows are grouped by department.

Groups formed:

```text
Engineering:
    70000
    80000
```

---

# Step 5 → HAVING

```sql
HAVING AVG(e.salary) > 60000
```

HAVING filters groups.

Engineering group:

```text
AVG = (70000 + 80000) / 2
    = 75000
```

Condition passes.

---

# Step 6 → SELECT

```sql
SELECT
    d.dept_name,
    COUNT(e.emp_id),
    AVG(e.salary),
    MAX(e.salary)
```

Columns and aggregate functions are calculated.

Result:

| dept_name | total_employees | avg_salary | highest_salary |
|---|---|---|---|
| Engineering | 2 | 75000 | 80000 |

---

# Step 7 → ORDER BY

```sql
ORDER BY avg_salary DESC
```

Sorting happens.

Since only one row exists:

No visible change.

---

# Step 8 → LIMIT

```sql
LIMIT 5
```

Only first 5 rows returned.

Still one row.

---

# Final Output

| dept_name | total_employees | avg_salary | highest_salary |
|---|---|---|---|
| Engineering | 2 | 75000 | 80000 |

---


## Query Writing Order

```sql
SELECT
FROM
JOIN
WHERE
GROUP BY
HAVING
ORDER BY
LIMIT
```

---

## Actual Execution Order

```sql
FROM
JOIN
ON
WHERE
GROUP BY
HAVING
SELECT
ORDER BY
LIMIT
```

---

# Final Summary Table

| Clause | Purpose |
|---|---|
| FROM | Load table |
| JOIN | Combine tables |
| WHERE | Filter rows |
| GROUP BY | Create groups |
| HAVING | Filter groups |
| SELECT | Choose output columns |
| ORDER BY | Sort result |
| LIMIT | Restrict rows |

---

```