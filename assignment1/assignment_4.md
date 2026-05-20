# Clients Table Documentation

## Overview

The `clients` table is used to store information about clients in the database. It contains basic details such as client name, contact information, company address, and record creation timestamp.

---

## Table Structure

| Column Name       | Data Type    | Constraints                 | Description                                                                                   |
| ----------------- | ------------ | --------------------------- | --------------------------------------------------------------------------------------------- |
| `client_id`       | SERIAL       | Primary Key, Auto Increment | Unique identifier for each client record. Automatically increases for every new client added. |
| `client_name`     | VARCHAR(100) | NOT NULL                    | Stores the name of the client or company. This field is mandatory.                            |
| `contact_person`  | VARCHAR(100) | None                        | Stores the name of the main contact person for the client.                                    |
| `email`           | VARCHAR(100) | UNIQUE                      | Stores the email address of the client. Duplicate emails are not allowed.                     |
| `phone`           | VARCHAR(15)  | None                        | Stores the contact phone number of the client.                                                |
| `company_address` | TEXT         | None                        | Stores the complete address of the client company.                                            |
| `created_at`      | TIMESTAMP    | Default: CURRENT_TIMESTAMP  | Stores the date and time when the client record was created automatically.                    |

---

## Detailed Explanation

### 1. `client_id`

* Data Type: `SERIAL`
* Purpose:

  * Acts as the primary key of the table.
  * Ensures every client has a unique identifier.
  * Automatically increments whenever a new row is inserted.

Example:

```sql
1
2
3
```

---

### 2. `client_name`

* Data Type: `VARCHAR(100)`
* Constraint: `NOT NULL`
* Purpose:

  * Stores the official name of the client or organization.
  * Cannot be left empty.

Example:

```sql
'ABC Technologies'
```

---

### 3. `contact_person`

* Data Type: `VARCHAR(100)`
* Purpose:

  * Stores the name of the individual responsible for communication.
  * Optional field.

Example:

```sql
'Rahul Sharma'
```

---

### 4. `email`

* Data Type: `VARCHAR(100)`
* Constraint: `UNIQUE`
* Purpose:

  * Stores the client's email address.
  * Prevents duplicate email entries.

Example:

```sql
'client@example.com'
```

---

### 5. `phone`

* Data Type: `VARCHAR(15)`
* Purpose:

  * Stores the contact phone number.
  * Kept as `VARCHAR` instead of numeric type because phone numbers may contain `+`, `-`, or leading zeros.

Example:

```sql
'+91-9876543210'
```

---

### 6. `company_address`

* Data Type: `TEXT`
* Purpose:

  * Stores the complete address of the client company.
  * `TEXT` is used because addresses can vary in length.

Example:

```sql
'221B Baker Street, London'
```

---

### 7. `created_at`

* Data Type: `TIMESTAMP`
* Default Value: `CURRENT_TIMESTAMP`
* Purpose:

  * Automatically stores the date and time when a client record is created.
  * Useful for tracking record creation history.

Example:

```sql
2026-05-20 11:30:45
```

---

## SQL Table Definition

```sql
CREATE TABLE clients (
    client_id SERIAL PRIMARY KEY,
    client_name VARCHAR(100) NOT NULL,
    contact_person VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    phone VARCHAR(15),
    company_address TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

## Example Insert Query

```sql
INSERT INTO clients (
    client_name,
    contact_person,
    email,
    phone,
    company_address
)
VALUES (
    'ABC Technologies',
    'Rahul Sharma',
    'abc@example.com',
    '+91-9876543210',
    'Lucknow, Uttar Pradesh, India'
);
```

---

## Key Features of This Table

* Ensures unique client identification using `client_id`.
* Prevents duplicate emails using the `UNIQUE` constraint.
* Automatically tracks creation time with `created_at`.
* Flexible storage for addresses using the `TEXT` datatype.
* Maintains mandatory client information using `NOT NULL` constraint.
