# CAP Theorem

## Overview

CAP Theorem explains an important limitation in distributed database systems. It states that a distributed system cannot guarantee Consistency, Availability, and Partition Tolerance at the same time. A system can provide only two out of these three properties during a network failure. This paper explains the meaning of CAP, its components, and its importance in modern database design.

---

## 1. Introduction

Modern applications often use distributed databases.  
A distributed database stores data across multiple servers instead of a single machine.

This improves:

- Scalability  
- Fault tolerance  
- Performance  

However, distributed systems face network failures. CAP Theorem describes what happens in such situations.

The theorem was introduced by computer scientist Eric Brewer.

---

## 2. The Three Components of CAP

CAP stands for:

- Consistency (C)  
- Availability (A)  
- Partition Tolerance (P)  

Let us understand each one in simple terms.

---

## 3. Consistency (C)

Consistency means all users see the same data at the same time.

If one user updates a value, every other user should immediately see the updated value.

Example:

If a bank balance becomes 5000, no user should see the old value 4000 after the update is completed.

Consistency ensures data correctness.

---

## 4. Availability (A)

Availability means the system always responds to requests.

Every request receives a response:

- Success  
- Or failure  

But the system should not hang or stop responding.

Even if some servers fail, the system should continue working.

Availability focuses on uptime and responsiveness.

---

## 5. Partition Tolerance (P)

Partition Tolerance means the system continues working even if communication between servers is broken.

A partition happens when:

- Network connection fails  
- Servers cannot communicate  
- Data centers are disconnected  

In distributed systems, network failures are unavoidable. Therefore, Partition Tolerance is usually required.

---

## 6. Why All Three Cannot Be Achieved Together

During a network partition, a system must choose between:

- Consistency  
- Availability  

It cannot guarantee both at the same time.

If the system chooses:

- **Consistency** → It may reject some requests to keep data accurate.  
- **Availability** → It may return outdated data to keep responding.  

This trade-off is the core idea of CAP Theorem.

---

## 7. Types of CAP Systems

Distributed databases are usually classified as:

### 1. CP (Consistency + Partition Tolerance)

- Maintains correct data  
- May reduce availability during failures  

Example: Traditional distributed SQL databases.

---

### 2. AP (Availability + Partition Tolerance)

- Always responds to requests  
- Data may not be immediately consistent  

Example: Many NoSQL systems.

---

### 3. CA (Consistency + Availability)

- Possible only when there is no network partition  
- Not realistic in large distributed systems  

---

## 8. CAP Theorem in Real Systems

Different databases prioritize different properties:

- Banking systems prefer Consistency  
- Social media platforms prefer Availability  
- Large cloud systems must support Partition Tolerance  

Design decisions depend on application requirements.

---

