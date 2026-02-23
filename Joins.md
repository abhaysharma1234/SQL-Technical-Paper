# SQL Joins: Combining Data from Multiple Tables

## Overview

In relational databases, data is usually stored in multiple related tables instead of one large table. SQL Joins are used to combine rows from two or more tables based on a related column. Joins are essential for retrieving meaningful information from structured databases. This paper explains the concept of joins, their types, and their practical importance.

---

## 1. Introduction

In real-world database design, data is separated into different tables to reduce redundancy and improve organization.

For example:

- A `customers` table stores customer details.
- An `orders` table stores order information.

To see which customer placed which order, we must combine these tables.  
This is done using **JOIN**.

---

## 2. Why Joins are Important

Without joins:

- Data would need to be duplicated.
- Queries would become inefficient.
- Database design would violate normalization rules.

Joins allow:

- Efficient data retrieval  
- Clean database structure  
- Reduced redundancy  

They are fundamental in relational database systems.

---

## 3. Basic Syntax of JOIN

```sql
SELECT columns
FROM table1
JOIN table2
ON table1.column = table2.column;
```

The `ON` condition defines how the tables are related.

---

## 4. Types of SQL Joins

### 4.1 INNER JOIN

Returns only the matching rows from both tables.

Example:

```sql
SELECT customers.name, orders.order_id
FROM customers
INNER JOIN orders
ON customers.customer_id = orders.customer_id;
```

Only customers who have placed orders will appear.

---

### 4.2 LEFT JOIN (LEFT OUTER JOIN)

Returns:

- All rows from the left table  
- Matching rows from the right table  
- NULL if no match is found  

Example:

```sql
SELECT customers.name, orders.order_id
FROM customers
LEFT JOIN orders
ON customers.customer_id = orders.customer_id;
```

All customers appear, even those without orders.

---

### 4.3 RIGHT JOIN (RIGHT OUTER JOIN)

Returns:

- All rows from the right table  
- Matching rows from the left table  
- NULL if no match is found  

Example:

```sql
SELECT customers.name, orders.order_id
FROM customers
RIGHT JOIN orders
ON customers.customer_id = orders.customer_id;
```

All orders appear, even if customer details are missing.

---

### 4.4 FULL JOIN (FULL OUTER JOIN)

Returns:

- All rows from both tables  
- NULL where no match exists  

Example:

```sql
SELECT customers.name, orders.order_id
FROM customers
FULL JOIN orders
ON customers.customer_id = orders.customer_id;
```

Includes matched and unmatched records from both tables.

---

## 5. Visual Understanding

If we think of tables as sets:

- INNER JOIN → Common part  
- LEFT JOIN → Left table + common  
- RIGHT JOIN → Right table + common  
- FULL JOIN → Entire area of both tables  

This helps in understanding how results are formed.

---

## 6. Practical Example Scenario

Consider two tables:

### customers

| customer_id | name   |
|------------|--------|
| 1          | Rahul  |
| 2          | Ananya |
| 3          | Vikram |

### orders

| order_id | customer_id |
|----------|------------|
| 101      | 1          |
| 102      | 2          |

Using:

```sql
SELECT *
FROM customers
LEFT JOIN orders
ON customers.customer_id = orders.customer_id;
```

Customer Vikram will appear with NULL order value because no order exists.

---

