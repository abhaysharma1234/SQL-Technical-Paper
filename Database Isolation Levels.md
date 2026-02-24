# Database Isolation Levels

## Overview

In multi-user database systems, many transactions run at the same time. To control how these transactions interact with each other, databases use isolation levels. Isolation levels define how visible the changes made by one transaction are to other transactions. This paper explains different isolation levels in SQL, common concurrency problems, and their importance in transaction management.

---

## 1. Introduction

When multiple users access a database simultaneously, problems may occur such as:

- Reading uncommitted data  
- Overwriting changes  
- Getting inconsistent results  

Isolation levels control these issues by defining rules for transaction visibility.

Isolation is one of the ACID properties of transactions.

---

## 2. Why Isolation Levels are Needed

Consider two transactions running at the same time:

Transaction A updates a value.  
Transaction B reads that value before A commits.

If not controlled properly, incorrect or temporary data may be visible.

Isolation levels help balance:

- Data accuracy  
- System performance  

Higher isolation increases safety but may reduce performance.

---

## 3. Common Concurrency Problems

Before understanding isolation levels, we must understand common issues.

### 3.1 Dirty Read

Reading data that has not been committed.

If the transaction rolls back later, the read data becomes invalid.

---

### 3.2 Non-Repeatable Read

Reading the same row twice but getting different results because another transaction updated it.

---

### 3.3 Phantom Read

Re-running a query returns additional rows because another transaction inserted new data.

---

## 4. Isolation Levels in SQL

SQL defines four standard isolation levels.

---

### 4.1 READ UNCOMMITTED

- Lowest isolation level  
- Allows dirty reads  
- High performance  
- Low data accuracy  

Example:

```sql
SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;
```

Transactions may see uncommitted changes.

---

### 4.2 READ COMMITTED

- Prevents dirty reads  
- Allows non-repeatable reads  
- Common default level in many databases  

Example:

```sql
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
```

A transaction can only read committed data.

---

### 4.3 REPEATABLE READ

- Prevents dirty reads  
- Prevents non-repeatable reads  
- Phantom reads may still occur (in some systems)  

Example:

```sql
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
```

Rows read cannot be modified by other transactions until commit.

---

### 4.4 SERIALIZABLE

- Highest isolation level  
- Prevents dirty reads  
- Prevents non-repeatable reads  
- Prevents phantom reads  
- Lowest concurrency  

Example:

```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```

Transactions behave as if executed one after another.

---

## 5. Comparison Table

| Isolation Level      | Dirty Read | Non-Repeatable Read | Phantom Read |
|----------------------|------------|---------------------|--------------|
| READ UNCOMMITTED     | Possible   | Possible            | Possible     |
| READ COMMITTED       | Not Allowed| Possible            | Possible     |
| REPEATABLE READ      | Not Allowed| Not Allowed         | Possible     |
| SERIALIZABLE         | Not Allowed| Not Allowed         | Not Allowed  |

---

## 6. Performance vs Consistency

Lower isolation levels:

- Higher performance  
- More concurrency  
- Less strict control  

Higher isolation levels:

- Better data accuracy  
- Reduced concurrency  
- Possible locking delays  

Database designers choose isolation level based on system requirements.

---

