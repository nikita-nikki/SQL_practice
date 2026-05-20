# ASSIGNMENT 2

## Problem Statement: Database Selection Framework

For each category below:

* Compare the available options
* Explain when you would pick one over another
* Justify your choice with a real-world scenario

Categories:

1. Relational Databases
2. NoSQL Databases
3. Cloud Data Warehouses
4. In-Memory Databases
5. Object Storage

---

# Solution

## 1. SQL vs NoSQL

### SQL

SQL databases are better when:

* The structure is fixed
* Tables are predefined
* Relationships between tables are important

Examples:

* School management systems
* Banking systems

---

### NoSQL

NoSQL databases are better when:

* Schema is flexible
* Different documents can have different fields

Example:

In an e-commerce application, different products belong to different categories.
Each category may have different attributes.

Using SQL here may result in many `NULL` values, while NoSQL handles this flexibility better.

---

## 2. MySQL vs PostgreSQL vs Oracle

### MySQL

* Simple and easy to learn
* Suitable for beginners and small projects

Examples:

* Learning projects
* School or college projects

---

### PostgreSQL

Used when:

* Complex queries are required
* ACID properties are important
* High concurrency handling is needed

Advantages:

* Cheaper than Oracle
* Supports both JSON and SQL
* More flexible

Examples:

* Analytics dashboards
* Banking systems

---

### Oracle

* Mainly used by large enterprises
* Suitable for enterprise-scale applications

---

## 3. Cloud Data Warehouse: Snowflake vs Databricks

Cloud data warehouses are used for analytics problems.

Example:

* Finding which product increased revenue the most in the last 2 years

---

### Snowflake

* Simpler and easier to manage
* Mainly focused on analytics and warehousing

---

### Databricks

* Supports Machine Learning workflows
* Useful when training models on large datasets

---

## 4. In-Memory Databases: Memcached vs Redis

In-memory databases store data in RAM instead of disk.

Advantages:

* Very fast access speed

---

### Memcached

* Used mainly for simple caching
* Fast and lightweight

---

### Redis

Provides additional features such as:

* Session storage
* Queue storage
* Pub/Sub systems

Redis is more flexible compared to Memcached.

---

## 5. Object Storage

Object storage is used to store large unstructured data such as:

* Images
* Videos
* Backups
* Logs

Examples:

* Amazon S3
* Google Cloud Storage
* Azure Blob Storage

### Vendor Lock-in

Vendor lock-in becomes a concern when:

* Applications become highly dependent on one cloud provider
* Migration cost becomes very high
* APIs and storage formats are tightly integrated with one vendor

Example:

If a company stores petabytes of data in Amazon S3 and heavily uses AWS-specific services, migrating to another cloud provider becomes difficult and expensive.
