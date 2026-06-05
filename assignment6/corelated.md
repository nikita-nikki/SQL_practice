# Correlated Subquery Example

## Create Table

```sql
CREATE TABLE employees (
    emp_id INT,
    emp_name VARCHAR(50),
    department VARCHAR(20),
    salary INT
);
```

## Insert Data

```sql
INSERT INTO employees VALUES
(1, 'Alice',   'HR', 50000),
(2, 'Bob',     'HR', 60000),
(3, 'Charlie', 'IT', 70000),
(4, 'David',   'IT', 65000),
(5, 'Emma',    'IT', 80000);
```

## Employee Table

| emp_id | emp_name | department | salary |
|---------|----------|------------|---------|
| 1 | Alice | HR | 50000 |
| 2 | Bob | HR | 60000 |
| 3 | Charlie | IT | 70000 |
| 4 | David | IT | 65000 |
| 5 | Emma | IT | 80000 |

---

## Question

Find the employees whose salary is greater than the **average salary of their own department**.

---

## Solution

```sql
SELECT e1.emp_name,
       e1.department,
       e1.salary
FROM employees e1
WHERE e1.salary >
(
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department = e1.department
);
```

---

## Output

| emp_name | department | salary |
|-----------|------------|---------|
| Bob | HR | 60000 |
| Emma | IT | 80000 |

---

