# Transactions in SQL 

## Overview

A transaction in SQL is a sequence of one or more database operations executed as a single unit of work. Transactions ensure that data remains accurate and consistent, even when errors or system failures occur. This paper explains the concept of transactions, their properties, commands used in SQL, and their importance in real-world applications.

---

## 1. Introduction

In database systems, operations such as `INSERT`, `UPDATE`, and `DELETE` modify data.  
Sometimes multiple operations must be executed together.

For example, transferring money from one bank account to another requires:

- Deducting amount from one account  
- Adding amount to another account  

If one operation succeeds and the other fails, the data becomes incorrect.  
Transactions prevent such problems.

---

## 2. What is a Transaction?

A transaction is a group of SQL statements executed together as one logical unit.

Basic structure:

```sql
BEGIN;

SQL statements;

COMMIT;
```

If everything works correctly, the changes are saved permanently using `COMMIT`.

If something goes wrong:

```sql
ROLLBACK;
```

All changes made during the transaction are undone.

---

## 3. Main Transaction Commands

### 3.1 BEGIN / START TRANSACTION

Starts a new transaction.

```sql
START TRANSACTION;
```

---

### 3.2 COMMIT

Saves all changes permanently.

```sql
COMMIT;
```

After commit, changes cannot be reversed.

---

### 3.3 ROLLBACK

Cancels all changes made in the current transaction.

```sql
ROLLBACK;
```

The database returns to its previous state.

---

### 3.4 SAVEPOINT

Creates a temporary checkpoint inside a transaction.

```sql
SAVEPOINT sp1;
```

To rollback to savepoint:

```sql
ROLLBACK TO sp1;
```

This allows partial undo within a transaction.

---

## 4. Example of a Transaction

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 101;

UPDATE accounts
SET balance = balance + 1000
WHERE account_id = 202;

COMMIT;
```

If any update fails, we can use:

```sql
ROLLBACK;
```

This ensures money is not lost.

---

## 5. Why Transactions are Important

Transactions help in:

- Maintaining data accuracy  
- Preventing partial updates  
- Protecting against system crashes  
- Supporting multi-user environments  

They are especially important in banking, e-commerce, and financial systems.

---

## 6. Transactions and ACID

Transactions follow ACID properties:

- Atomicity → All operations succeed or fail together  
- Consistency → Database remains valid  
- Isolation → Transactions do not interfere  
- Durability → Committed data is permanent  

ACID ensures safe transaction management.

---

## 7. Transactions in Multi-User Systems

In real-world databases:

- Many users access data at the same time  
- Multiple transactions may run simultaneously  

Without proper transaction control:

- Data conflicts may occur  
- Incorrect results may appear  

Database systems use locks and isolation levels to manage concurrent transactions.

---

## 8. Auto-Commit Mode

Some database systems enable auto-commit by default.

In auto-commit mode:

- Every statement is treated as a separate transaction  
- Changes are automatically committed  

It can be disabled when manual transaction control is needed.

---

## Conclusion

Transactions are a fundamental part of SQL database systems. They ensure that multiple related operations are executed safely and correctly. By using commands like `BEGIN`, `COMMIT`, and `ROLLBACK`, databases maintain accuracy and reliability. Understanding transactions is essential for building secure and dependable database applications.