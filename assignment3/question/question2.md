# Convert Names Into Camel Case / Proper Case in PostgreSQL

## Input Data

| full_name |
|------------|
| amit Kumar |
| Om kashyap |

---

## Required Output

| full_name |
|-------------|
| Amit Kumar |
| Om Kashyap |

---

## Query

```sql id="wz1r7q"
SELECT INITCAP(full_name) AS formatted_name
FROM users;
```
Explanation:

INITCAP() -
INITCAP() converts the first letter of each word to uppercase
and the remaining letters to lowercase.