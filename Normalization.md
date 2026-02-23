# Normalization in SQL

## Overview

Normalization is a database design technique used to organize data efficiently in relational databases. It reduces data redundancy and improves data integrity by dividing large tables into smaller related tables. This paper explains the concept of normalization, different normal forms, and its importance in real-world database systems.

---

## 1. Introduction

In relational databases, data is stored in tables.  
If tables are not designed properly, problems may occur such as:

- Duplicate data  
- Data inconsistency  
- Difficulty in updating records  
- Increased storage usage  

Normalization solves these problems by structuring data logically.

---

## 2. What is Normalization?

Normalization is the process of organizing data into multiple tables to:

- Remove duplicate data  
- Ensure logical relationships  
- Maintain data consistency  
- Improve database efficiency  

It is done by applying rules called **Normal Forms**.

---

## 3. First Normal Form (1NF)

### Rule:
- Each column must contain atomic (single) values.
- No repeating groups.
- Each record must be unique.

### Example (Not in 1NF)

| student_id | name   | subjects        |
|------------|--------|----------------|
| 1          | Ravi   | Math, Science  |

Problem: Multiple values in one column.

### Converted to 1NF

| student_id | name  | subject  |
|------------|-------|----------|
| 1          | Ravi  | Math     |
| 1          | Ravi  | Science  |

Now each column contains a single value.

---

## 4. Second Normal Form (2NF)

### Rule:
- Must be in 1NF.
- No partial dependency.
- Non-key attributes must depend on the entire primary key.

### Example

If a table has a composite primary key:

| order_id | product_id | product_name | quantity |
|----------|------------|--------------|----------|

If `product_name` depends only on `product_id`, not on the full key, this violates 2NF.

Solution:
- Create separate table for products.

---

## 5. Third Normal Form (3NF)

### Rule:
- Must be in 2NF.
- No transitive dependency.
- Non-key attributes should depend only on the primary key.

### Example

| employee_id | employee_name | department_name | department_location |

If `department_location` depends on `department_name`, not directly on `employee_id`, this violates 3NF.

Solution:
- Create a separate department table.

---

## 6. Higher Normal Forms

Beyond 3NF, there are advanced forms:

- BCNF (Boyce-Codd Normal Form)
- 4NF (Fourth Normal Form)
- 5NF (Fifth Normal Form)

These handle more complex dependency cases, mostly used in advanced database design.

---

## 7. Advantages of Normalization

- Reduces data redundancy  
- Prevents update anomalies  
- Improves data integrity  
- Saves storage space  
- Makes database easier to maintain  

---

## 8. Disadvantages of Over-Normalization

- Too many tables  
- Complex queries  
- More joins required  
- Slight performance impact  

In some cases, controlled denormalization is used for performance optimization.

---

## 9. Real-World Importance

Normalization is important in:

- Banking systems  
- Student management systems  
- Inventory systems  
- HR and payroll systems  

Proper normalization ensures clean and structured database design.

---
