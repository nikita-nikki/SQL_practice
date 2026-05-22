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

2. 