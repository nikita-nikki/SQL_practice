1. UPPER & LOWER

-- Query 1
WHERE name IN ('ABC', 'DEF', 'XYZ')
vs
-- Query 2
WHERE LOWER(name) IN ('abc', 'def', 'xyz')

then:

Faster → Query 1
WHERE name IN (...)
because:

no function call on column
index can usually be used efficiently
direct comparison

Slower → Query 2
WHERE LOWER(name) IN (...)
because:

LOWER() runs for every row
DB must transform values before comparison
normal index on name may not be used

2. # Why `CONCAT(NULL, 'value', NULL)` Returns `value`

## Query

```sql
SELECT CONCAT(NULL, 'value', NULL);
```

## Output

```sql
value
```

## Reason

`CONCAT()` treats `NULL` as an empty string (`''`) in many databases like MySQL.

So internally it behaves like:

```sql
CONCAT('', 'value', '')
```

Which produces:

```sql
value
```

---

# Important Point

`CONCAT()` is designed to be user-friendly.

Instead of making the entire result `NULL`, it ignores `NULL` values during concatenation.

---

# Example

```sql
SELECT CONCAT('A', NULL, 'B');
```

## Output

```sql
AB
```

Because internally:

```sql
CONCAT('A', '', 'B')
```

---

# Contrast with `||`

```sql
SELECT 'A' || NULL || 'B';
```

## Output

```sql
NULL
```

Reason:

`||` follows standard SQL NULL propagation rules.

If any operand is `NULL`, the concatenation result becomes `NULL`.

Example:

```sql
'A' || NULL
= NULL
```

Hence:

```sql
'A' || NULL || 'B'
= NULL
```



