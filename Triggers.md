# Triggers in SQL

## Overview

Triggers are special database objects that automatically execute in response to specific events such as INSERT, UPDATE, or DELETE operations. They are used to enforce business rules, maintain data integrity, and automate tasks inside the database. This paper explains the concept of triggers, their types, syntax, advantages, and real-world applications.

---

## 1. Introduction

In database systems, certain actions need to happen automatically when data changes.

For example:

- When a new employee is added, a log entry should be created.
- When a product is deleted, related records should also be updated.
- When salary is updated, audit information should be stored.

Triggers allow these actions to run automatically without manual intervention.

---

## 2. What is a Trigger?

A trigger is a stored procedure that automatically executes when a specified event occurs on a table.

Common triggering events:

- INSERT  
- UPDATE  
- DELETE  

Triggers are attached to tables and are executed by the database engine.

---

## 3. Basic Syntax of a Trigger

Example syntax:

```sql
CREATE TRIGGER trigger_name
BEFORE INSERT
ON table_name
FOR EACH ROW
BEGIN
   -- SQL statements
END;
```

Triggers can be defined as:

- BEFORE trigger  
- AFTER trigger  

---

## 4. Types of Triggers

### 4.1 BEFORE Trigger

- Executes before the actual operation.
- Used for validation or modifying values.

Example:

```sql
CREATE TRIGGER check_salary
BEFORE INSERT
ON employees
FOR EACH ROW
BEGIN
   IF NEW.salary < 0 THEN
      SET NEW.salary = 0;
   END IF;
END;
```

This ensures salary cannot be negative.

---

### 4.2 AFTER Trigger

- Executes after the operation is completed.
- Often used for logging or auditing.

Example:

```sql
CREATE TRIGGER log_update
AFTER UPDATE
ON employees
FOR EACH ROW
BEGIN
   INSERT INTO employee_log(employee_id, change_date)
   VALUES (NEW.employee_id, CURRENT_DATE);
END;
```

This stores update history.

---

## 5. Row-Level vs Statement-Level Triggers

### Row-Level Trigger

- Executes once for each affected row.
- Uses `FOR EACH ROW`.

### Statement-Level Trigger

- Executes once per SQL statement.
- Does not depend on number of rows.

Most commonly used type is row-level trigger.

---

## 6. Uses of Triggers

Triggers are commonly used for:

- Maintaining audit logs  
- Enforcing complex business rules  
- Updating related tables automatically  
- Preventing invalid data entry  
- Maintaining derived values  

They reduce manual coding in applications.

---

## 7. Advantages of Triggers

- Automatic execution  
- Improves data integrity  
- Centralized business logic  
- Reduces application complexity  
- Ensures consistency across operations  

---

## 8. Disadvantages of Triggers

- Hard to debug  
- Hidden execution (not visible in normal queries)  
- May affect performance  
- Can cause complex dependency issues  

Triggers should be used carefully.

---
