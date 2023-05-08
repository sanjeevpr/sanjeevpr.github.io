---
layout: post
title: "Database Isolation Levels"
description: "An introduction to database isolation levels"
comments: true
keywords: "isolation levels, database, transaction"
---

### What is Isolation in Databases?

- Database isolation level defines the degree to which a transaction must be isolated from data modification from other concurrently running transactions.
- It allows a transaction to run in isolation as if there are no other concurrently running transactions.

### What is the importance of this?

- We need to prevent reads and writes of incorrect or temporary data written by other concurrently running transactions.

### Phenomena defining isolation levels

1. **Dirty Reads**
   - This is when uncommitted data is read by a transaction.
   - For example: Transaction A updates a row and does not commit it. Meanwhile, transaction B reads this uncommitted data. If transaction A rolls back changes, transaction B would have the wrong and non-existing data.
2. **Non-repeatable Reads**
   - It is a situation when a transaction, upon re-reading the same data twice, does not get the same value.
   - For example: This can happen when T1 reads the data which had a value of 10. Meanwhile, a concurrent transaction T2 updated and committed the same data with 20. Now, upon reading again, T1 will get the updated value.
3. **Phantom Reads**
   - It is the same as the non-repeatable read but affects not a single row, rather a set of rows.

For example, T1 reads a search query that returns a set of rows. In the meantime, another concurrent transaction T2 also queried the same set of rows, updates them, and commits the changes. Now, upon running the same query, T1 will see an updated set of rows.

### Isolation Levels

Based on these phenomena discussed, there are four isolation levels defined.

1. **Read Uncommitted**
   - In this, transactions can see each others committed changes.
   - Transactions are not isolated to each other.
   - This level provides highest level of concurrency, but lowest level of consistency.
2. **Read Committed**
   - In this, transactions can only read the committed changes.
   - Reading uncommitted changes are not allowed.
3. **Repeatable Read**
   - Transaction sees only the committed changes before the transaction begins.
   - Data read during the transaction will remain same as the data in the beginning of transaction.
4. **Serializable**
   - It guarantees that the concurrent transactions are executed sequentially / serially.
   - This level provides the lowest level of concurrency and highest level of consistency./a

### Reference
[https://www.geeksforgeeks.org/transaction-isolation-levels-dbms/](https://www.geeksforgeeks.org/transaction-isolation-levels-dbms/)
