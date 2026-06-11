
## Create Source Table

``` sql
CREATE TABLE api_data (
    id      SERIAL PRIMARY KEY,
    payload JSONB
);
```


##  Insert JSON Records

``` sql
INSERT INTO api_data (payload) VALUES
('{
  "sale_id": 11,
  "rep_name": "Rohan Bajaj",
  "department": "Engineering",
  "city": "Hyderabad",
  "amount": 78000,
  "status": "open"
}'),
('{
  "sale_id": 12,
  "rep_name": "Pooja Iyer",
  "department": "HR",
  "city": "Chennai",
  "amount": 44000,
  "status": "open"
}');
```



## View Stored JSON Data

``` sql
SELECT * FROM api_data;
```

### Output

  id   payload
  ---- -------------
  1    JSON Record
  2    JSON Record

This displays the raw JSON stored in the table.

------------------------------------------------------------------------

##  Create Destination Table

``` sql
CREATE TABLE sales_flat (
    sale_id INT,
    rep_name VARCHAR(100),
    department VARCHAR(100),
    city VARCHAR(100),
    amount NUMERIC,
    status VARCHAR(50)
);
```


## Extract Values from JSON

``` sql
SELECT
    payload->>'sale_id' AS sale_id,
    payload->>'rep_name' AS rep_name,
    payload->>'department' AS department
FROM api_data;
```



##  Flatten JSON and Insert into Relational Table

``` sql
INSERT INTO sales_flat
(
    sale_id,
    rep_name,
    department,
    city,
    amount,
    status
)
SELECT
    (payload->>'sale_id')::INT,
    payload->>'rep_name',
    payload->>'department',
    payload->>'city',
    (payload->>'amount')::NUMERIC,
    payload->>'status'
FROM api_data;
```


## Verify Flattened Data

``` sql
SELECT * FROM sales_flat;
```

### Expected Output

  sale_id   rep_name      department    city        amount   status
  --------- ------------- ------------- ----------- -------- --------
  11        Rohan Bajaj   Engineering   Hyderabad   78000    open
  12        Pooja Iyer    HR            Chennai     44000    open

------------------------------------------------------------------------


