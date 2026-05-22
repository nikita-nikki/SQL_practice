2. Fastest command to rollback things after delete And the slowest one:

Fastest Way to Rollback After DELETE
Fastest → ROLLBACK

Works ONLY before COMMIT.

Example:

START TRANSACTION;

DELETE FROM employees
WHERE id = 10;

ROLLBACK;
Why Fast?

Because DB has not permanently changed disk data yet.

It simply:

discards temporary changes
uses undo logs
restores old state internally

Time complexity is very small compared to restoring backups.





