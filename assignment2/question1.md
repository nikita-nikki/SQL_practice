1. How DB Knows About the Last Commit?

A database keeps track of transactions using transaction logs (also called WAL — Write Ahead Log in PostgreSQL, Redo Log in MySQL/Oracle).


Internally-
Each transaction gets a unique Transaction ID (TXN ID).

Example:

TXN_ID	Action	Status
101	INSERT INTO users	COMMITTED
102	DELETE FROM orders	ROLLED BACK
103	UPDATE salary	COMMITTED

The DB engine checks these logs during:

Crash recovery
Rollback
Replication


Why This Matters?
Suppose system crashes after an UPDATE but before COMMIT.

DB checks log:

If transaction was committed → redo changes
If not committed → undo changes

This ensures:

Atomicity
Consistency
Durability (ACID properties)

NOTE: Meaning of Redo
When a DB says:
“If transaction was committed → redo changes”
it means:
The database ensures that all committed data is restored even after a crash.

Example:

Suppose this query runs:

UPDATE accounts
SET balance = balance - 100
WHERE id = 1;

Then:

COMMIT;
What Happens Internally

Before changing actual table data, DB first writes this into a log file:

TXN 101:
UPDATE accounts
old balance = 500
new balance = 400
STATUS = COMMITTED

This is called:

WAL (Write Ahead Log)
Redo Log

depending on DB.

Crash Scenario

Imagine:

DB wrote COMMIT into log
But system crashed BEFORE data page was fully saved to disk

Now disk may still contain:

balance = 500

even though transaction was committed.

During Recovery

When DB restarts:

it scans transaction logs.

It sees:

TXN 101 = COMMITTED

So DB says:

“This transaction MUST exist in database.”

Then it REAPPLIES the operation.

This is called:

REDO

Meaning:

Apply committed changes again

So balance becomes:

400

again.