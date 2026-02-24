# Indexes in SQL 

## Overview

Indexes in SQL are special database objects used to improve the speed of data retrieval. They help the database system find rows quickly without scanning the entire table. Although indexes improve read performance, they also add some overhead during insert and update operations. This paper explains the concept of indexes, their types, advantages, and practical usage in database systems.

---

## 1. Introduction

When a table contains a large amount of data, searching for specific rows can become slow.

For example:

```sql
SELECT * 
FROM employees
WHERE employee_id = 1050;
```

If no index exists, the database may scan every row to find the result.  
This is called a **full table scan**.

Indexes help avoid this by providing faster lookup mechanisms.

---

## 2. What is an Index?

An index is a data structure that improves the speed of search operations.

It works similarly to an index in a book:

- Instead of reading the entire book  
- You directly go to the page number  

In databases, indexes store references to table rows in a structured format.

---

## 3. Creating an Index

Basic syntax:

```sql
CREATE INDEX index_name
ON table_name (column_name);
```

Example:

```sql
CREATE INDEX idx_employee_id
ON employees (employee_id);
```

Now searches based on `employee_id` become faster.

---

## 4. Types of Indexes

### 4.1 Single-Column Index

Created on one column.

```sql
CREATE INDEX idx_salary
ON employees (salary);
```

---

### 4.2 Composite Index

Created on multiple columns.

```sql
CREATE INDEX idx_name_dept
ON employees (name, department);
```

Useful when queries filter using multiple columns.

---

### 4.3 Unique Index

Ensures all values in a column are unique.

```sql
CREATE UNIQUE INDEX idx_email
ON employees (email);
```

Often automatically created for primary keys.

---

### 4.4 Primary Key Index

When a primary key is defined:

```sql
PRIMARY KEY (employee_id)
```

The database automatically creates an index.

---

## 5. How Indexes Improve Performance

Without index:

- Database checks each row  
- Time complexity increases with table size  

With index:

- Database uses structured search (like B-tree)  
- Faster lookup  
- Reduced query time  

Indexes are especially helpful in:

- Large tables  
- Frequently searched columns  
- JOIN conditions  
- WHERE clauses  

---

## 6. When Not to Use Indexes

Indexes are not always beneficial.

Disadvantages:

- Extra storage space required  
- Slower INSERT operations  
- Slower UPDATE operations  
- Slower DELETE operations  

Because every change must also update the index.

Indexes should be created only on important columns.

---

## 7. Example Scenario

Suppose a table has 1 million rows.

Query:

```sql
SELECT *
FROM orders
WHERE order_id = 500000;
```

With index on `order_id`, the result is returned quickly.  
Without index, the database scans all rows.

This difference becomes significant in large systems.

---

