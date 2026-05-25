# How `SETSEED()` and `RANDOM()` Work Together in Databases

## 1. What is `RANDOM()`?

`RANDOM()` is a database function that generates a pseudo-random number.

Example in PostgreSQL:

```sql
SELECT RANDOM();
```

Possible output:

```text
0.7348291
```

The value is usually between:

```text
0 <= value < 1
```

---

# 2. Why is it called "Pseudo-Random"?

Databases do **not** generate truly random values.

Instead, they use an algorithm called a:

```text
Pseudo Random Number Generator (PRNG)
```

A PRNG generates numbers using:

- mathematical formulas
- an internal state
- a starting point called a **seed**

If the same seed is used again:

- the same sequence of random numbers is produced again.

---

# 3. What does `SETSEED()` do?

`SETSEED()` initializes the internal state of the PRNG.

Syntax:

```sql
SELECT SETSEED(0.5);
```

After this, every call to `RANDOM()` follows a deterministic sequence.

Example:

```sql
SELECT SETSEED(0.5);

SELECT RANDOM();
SELECT RANDOM();
SELECT RANDOM();
```

You may get:

```text
0.9851677
0.8253018
0.1297461
```

If you run the exact same statements again:

```sql
SELECT SETSEED(0.5);

SELECT RANDOM();
SELECT RANDOM();
SELECT RANDOM();
```

You will again get:

```text
0.9851677
0.8253018
0.1297461
```

---

# 4. Internal Working (Backend Logic)

Simplified backend flow:

```text
SETSEED(seed)
        ↓
Initialize PRNG internal state
        ↓
RANDOM() called
        ↓
PRNG formula calculates next value
        ↓
Internal state changes
        ↓
Next RANDOM() gives next value in sequence
```

---

# 5. Simplified Mathematical Idea

Most databases use algorithms similar to:

```text
next = (a × current + c) mod m
```

Where:

- `current` = current internal state
- `a`, `c`, `m` = fixed constants
- `next` = next pseudo-random value

This is why:

- same seed → same sequence
- different seed → different sequence

---

# 6. Example of Sequence Generation

Suppose:

```text
Seed = 10
```

Internal state becomes:

```text
current = 10
```

Then:

```text
next1 = formula(10)
next2 = formula(next1)
next3 = formula(next2)
```

So each `RANDOM()` depends on the previous state.

---

# 7. Important Property

Without `SETSEED()`:

- database automatically picks a seed
- usually based on:
  - current timestamp
  - process state
  - system entropy

Therefore:

```sql
SELECT RANDOM();
```

gives different outputs every execution.

---

# 8. Why `SETSEED()` is Useful

## A. Reproducible Testing

Useful in:

- testing
- debugging
- simulations

Example:

```sql
SELECT SETSEED(0.25);
```

Now every developer gets identical random outputs.

---

## B. Consistent Sampling

Example:

```sql
SELECT *
FROM users
ORDER BY RANDOM()
LIMIT 5;
```

With `SETSEED()`:

- same rows can appear repeatedly
- useful for testing queries

---

# 9. Important Limitation

`RANDOM()` is:

- fast
- predictable

Therefore:

❌ NOT suitable for:

- passwords
- cryptography
- security tokens

Because if someone knows the seed and algorithm:

- future random values can be predicted.

---
