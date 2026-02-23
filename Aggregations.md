# Aggregations and Filters in SQL Queries

## Overview

In relational databases, large amounts of data are stored in tables. To analyze this data, SQL provides aggregation functions and filtering techniques. Aggregations help summarize data, while filters help select specific records based on conditions. This paper explains how aggregation functions and filtering clauses work in SQL and why they are important in real-world database systems.

---

## 1. Introduction

Databases often contain thousands or millions of rows.  
Instead of viewing every row, we usually need summarized information such as:

- Total sales  
- Average salary  
- Number of students  
- Maximum or minimum value  

SQL provides aggregation functions to perform such calculations.  
Filters allow us to restrict results based on certain conditions.

---

## 2. What are Aggregation Functions?

Aggregation functions perform calculations on multiple rows and return a single value.

Common aggregation functions:

- `COUNT()` → Counts rows  
- `SUM()` → Adds values  
- `AVG()` → Finds average  
- `MIN()` → Smallest value  
- `MAX()` → Largest value  

---

## 3. Examples of Aggregation

### COUNT Example

```sql
SELECT COUNT(*) 
FROM employees;
```

Returns total number of employees.

---

### SUM Example

```sql
SELECT SUM(salary) 
FROM employees;
```

Returns total salary paid to all employees.

---

### AVG Example

```sql
SELECT AVG(salary) 
FROM employees;
```

Returns average salary.

---

### MIN and MAX Example

```sql
SELECT MIN(salary), MAX(salary)
FROM employees;
```

Returns lowest and highest salary.

---

## 4. Grouping Data using GROUP BY

Sometimes we need aggregated results for each category.

Example: Total salary per department.

```sql
SELECT department_id, SUM(salary)
FROM employees
GROUP BY department_id;
```

`GROUP BY` divides data into groups and applies aggregation to each group.

---

## 5. What are Filters in SQL?

Filters are used to limit the rows returned in a query.

The main filtering clause is:

```sql
WHERE
```

It selects rows based on conditions.

---

## 6. Using WHERE Clause

Example: Employees earning more than 50000.

```sql
SELECT name, salary
FROM employees
WHERE salary > 50000;
```

Only matching rows are returned.

Common operators:

- `=` Equal  
- `>` Greater than  
- `<` Less than  
- `>=`, `<=`  
- `<>` Not equal  
- `AND`, `OR`, `NOT`  

---

## 7. Filtering Groups using HAVING

When using aggregation with `GROUP BY`, we cannot use `WHERE` to filter aggregated results.  
Instead, we use `HAVING`.

Example: Departments with total salary greater than 200000.

```sql
SELECT department_id, SUM(salary)
FROM employees
GROUP BY department_id
HAVING SUM(salary) > 200000;
```

Difference:

- `WHERE` filters rows before grouping  
- `HAVING` filters groups after aggregation  

---

## 8. Combining Aggregation and Filters

Example: Average salary of employees in IT department.

```sql
SELECT AVG(salary)
FROM employees
WHERE department = 'IT';
```

Example with grouping and filtering:

```sql
SELECT department, COUNT(*)
FROM employees
WHERE salary > 30000
GROUP BY department
HAVING COUNT(*) > 5;
```

This query:

- Filters employees with salary > 30000  
- Groups them by department  
- Shows departments with more than 5 employees  

---

