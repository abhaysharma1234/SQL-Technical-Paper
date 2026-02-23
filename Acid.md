# ACID Properties in SQL

## Introduction

In database systems, transactions must be handled carefully to prevent data errors. ACID is a set of four rules that help databases stay accurate and reliable. ACID stands for Atomicity, Consistency, Isolation, and Durability. These properties make sure that data remains correct even when many users access the system or when unexpected failures happen.

---

## 1. What is a Transaction in SQL?

A transaction is a group of SQL operations executed together as one unit.

For example:

```sql
BEGIN;

INSERT INTO orders (order_id, amount)
VALUES (1, 500);

UPDATE customers
SET total_spent = total_spent + 500
WHERE customer_id = 10;

COMMIT;
```

If any statement fails, the database should not save partial results.  
This protection is provided by ACID properties.

---

## 2. Why ACID is Needed

Modern applications like banking systems, shopping websites, and ticket booking platforms process thousands of transactions every second.

Without strict control:

- Money could be deducted but not credited.
- Orders could be recorded without updating stock.
- Data could become inconsistent.

ACID rules prevent such problems.

---

## 3. Atomicity – Complete or Nothing

Atomicity means a transaction must either:

- Fully complete  
- Or completely fail  

There is no middle state.

If something goes wrong:

```sql
ROLLBACK;
```

The database cancels all changes made during that transaction.

Example:  
If money is transferred from Account A to Account B and the system crashes after deducting money from A, the database will undo the deduction.

Atomicity protects against partial updates.

---

## 4. Consistency – Data Must Stay Valid

Consistency ensures that the database always follows defined rules.

These rules include:

- Primary key constraints  
- Foreign key relationships  
- Data type rules  
- Check conditions  

Example:

```sql
CHECK (salary > 0)
```

If a transaction tries to insert a negative salary, the database rejects it.

After every successful `COMMIT`, the database remains in a valid state.

---

## 5. Isolation – Safe Concurrent Access

In real systems, many users use the database at the same time.

Isolation ensures that one transaction does not see incomplete data from another transaction.

Common problems without isolation:

- Dirty read (reading uncommitted data)
- Lost update
- Phantom read

SQL databases provide isolation levels such as:

```sql
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
```

Higher isolation gives more accuracy but may reduce performance.

---

## 6. Durability – Data is Permanently Saved

Durability means once a transaction is committed, its changes will not be lost.

Even if:

- Power failure happens  
- System crashes  
- Server restarts  

The committed data remains safe.

Databases use transaction logs and disk storage systems to ensure durability.

After:

```sql
COMMIT;
```

Changes become permanent.

---

## 7. Real-World Importance of ACID

ACID properties are very important in:

- Banking systems  
- Online payments  
- Hospital databases  
- Inventory systems  
- Government record systems  

If ACID rules are not followed, serious financial and data errors can occur.

---
