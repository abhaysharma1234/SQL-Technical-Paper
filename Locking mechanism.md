# Locking Mechanism in SQL

## Overview

In multi-user database systems, many users can access and modify data at the same time. To prevent conflicts and maintain data accuracy, databases use a locking mechanism. Locks control how transactions interact with data and ensure safe concurrent execution. This paper explains the concept of locking, types of locks, and their importance in transaction management.

---

## 1. Introduction

In real-world systems such as banking or e-commerce applications, multiple users may try to update the same data simultaneously.

For example:

- Two users try to withdraw money from the same bank account.
- Two employees try to update the same record at the same time.

Without control, this can cause data inconsistency.

The locking mechanism prevents such conflicts.

---

## 2. What is a Lock?

A lock is a restriction placed on database data during a transaction.

When a transaction locks a row or table:

- Other transactions may be restricted from modifying it.
- Some operations may have to wait until the lock is released.

Locks ensure safe execution of concurrent transactions.

---

## 3. Why Locking is Needed

Locking helps in:

- Preventing lost updates  
- Avoiding dirty reads  
- Maintaining transaction isolation  
- Protecting data integrity  

Without locks, concurrent transactions could overwrite each other’s changes.

---

## 4. Types of Locks

### 4.1 Shared Lock (Read Lock)

- Used when a transaction reads data.
- Multiple transactions can hold shared locks at the same time.
- No transaction can modify the data while it is being read.

Example scenario:
A user viewing account balance places a shared lock.

---

### 4.2 Exclusive Lock (Write Lock)

- Used when a transaction modifies data.
- Only one transaction can hold an exclusive lock.
- Other transactions cannot read or write until the lock is released.

Example scenario:
Updating account balance requires an exclusive lock.

---

## 5. Lock Levels

Locks can be applied at different levels:

- Row-level lock (specific row)
- Page-level lock (group of rows)
- Table-level lock (entire table)
- Database-level lock (entire database)

Row-level locking is more efficient because it allows higher concurrency.

---

## 6. Example of Locking in Action

Transaction 1:

```sql
START TRANSACTION;
UPDATE accounts
SET balance = balance - 500
WHERE account_id = 101;
```

Transaction 2:

```sql
UPDATE accounts
SET balance = balance + 100
WHERE account_id = 101;
```

If Transaction 1 has not committed yet, Transaction 2 must wait because the row is locked.

After:

```sql
COMMIT;
```

The lock is released.

---

## 7. Locking and Isolation Levels

Isolation levels control how locks behave.

Common levels:

- READ UNCOMMITTED  
- READ COMMITTED  
- REPEATABLE READ  
- SERIALIZABLE  

Higher isolation levels use stricter locking, which increases data safety but may reduce performance.

---

## 8. Problems Related to Locking

Although locking is necessary, it can cause:

- Blocking (transactions waiting)
- Reduced performance
- Deadlocks (two transactions waiting for each other)

Proper database design helps reduce these issues.

---

## 9. Importance in Real Systems

Locking mechanisms are essential in:

- Banking systems  
- Online payment systems  
- Inventory management  
- Reservation systems  
- Multi-user enterprise applications  

They ensure safe data modification in concurrent environments.

---
