3.How DISTINCT Works With *

When you write:

SELECT DISTINCT *
FROM employees;

the DB removes duplicate entire rows.
It does NOT check just one column.
It compares all columns together.