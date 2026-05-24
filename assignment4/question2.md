ARRAY_AGG vs STRING_AGG in SQL

1. ARRAY_AGG()

ARRAY_AGG() stores values as an actual array.

Example:

SELECT ARRAY_AGG(name)
FROM users;

Output:

{Amit,Rahul,Neha}

2. STRING_AGG()

STRING_AGG() combines values into a single string.

Example:

SELECT STRING_AGG(name, ', ')
FROM users;

Output:
Amit, Rahul, Neha



Major Practical Advantages

1. Individual Element Access

With ARRAY_AGG():

SELECT (ARRAY_AGG(name))[1]
FROM users;

You can directly access elements.

With STRING_AGG(), you first need splitting functions.

2. No Delimiter Problems

STRING_AGG() may break if values already contain commas.

Example:

Amit, Kumar, Rahul

You cannot know whether Amit, Kumar is one value or two.

ARRAY_AGG() avoids this issue because values stay separate internally.

