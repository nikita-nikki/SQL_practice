# ASSIGNMENT 1

## Problem Statement: Transaction Management at Scale

A nightly billing job needs to update 1 million records. It crashed midway last week and the entire job had to restart from scratch.

Write a SQL script that commits 1 million transactions efficiently. Your script should handle failures gracefully so the entire job never needs to restart from zero. Explain every decision you made and why.

---

## Solution: Use Batching

### Thought Process

Suppose we have 100 records.

### Case 1 – Update each record one by one

The problem with this approach is that if the system crashes, the process will start again from 0.

---

### Case 2 – Commit after every update

Using `COMMIT` after every update is expensive because commit operations are costly.
This reduces the overall speed of execution.

---

### Case 3 – Use Batching

Batching means dividing records into smaller groups.

Example:

* Total records = 100
* Batch size = 20

Process:

1. Update 20 records one by one
2. Commit the transaction
3. Move to the next 20 records
4. Repeat the process

We also track the last processed record number.

This ensures that if the system crashes, it resumes from the last committed batch instead of starting from zero again.

---

## SQL Query

```sql
START TRANSACTION;

UPDATE billing
SET status = 'PAID'
WHERE id BETWEEN 1 AND 10000
AND status != 'PAID';

COMMIT;
```

Repeat the same process for the remaining batches.

---

