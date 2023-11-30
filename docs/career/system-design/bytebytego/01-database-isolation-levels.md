---
date:
  created: 2023-10-26
  updated: 2023-11-30

description: >
  Insight about "What are database isolation levels? What are they used for?"

tags:
  - System Design
  - ByteByteGo

comments: true
---
# What are database isolation levels? What are they used for?

Before we discuss about isolation levels, let's review some important features used in modern database.

## Locks

- S Lock (Shared Lock): S Lock locks the write permission for other transactions while read operation is still allowed.
- X Lock (Exclusive Lock): X Lock, on the other hand, locks both read and write operation once a transaction obtained it.

| Lock | Read | Write |
|------|------|-------|
| S    | Yes  | No    |
| X    | No   | No    |

- range lock: lock multiple records in a table when SQL containing description like `WHERE length > 10`.

## Read Phenomena

### Dirty Read

Dirty read occurs when a transaction reads some value while another transaction is updating the value without committing or even rollback at the end. Now, the first transaction reads may acquire non-committed value.

### Non-repeatable Read

Similar to dirty read but the second transaction commits the change. Then, the first transaction would have inconsistent value during reads.

### Phamtom Read

Phamtom read may occur when the query contains `WHERE` clause.

While a transaction have selected records with `WHERE` and another transaction modifies some records within the `WHERE` statement. The selected records would change if the first transaction selects again.

## Isolation Levels

There are four levels of isolation:

1. Serializable: higest level, transaction must obtain x lock and range lock if used and can avoid **phamtom read**. See [serializability](https://en.wikipedia.org/wiki/Serializability) for more. 
2. Repeatable read: transaction must get x lock (but not range lock) to read and write record. Phamtom read may occur but ensure non-repeatable read from happening. 
3. Read committed: transaction is allowed to read commited data during transaction so non-repeatable read may happend.
4. Read uncommitted: basically no limit. Dirty read could happen.

|                  | Phamtom read | Non-repeatable read | Dirty read |
|------------------|--------------|---------------------|------------|
| Serializable     | No           | No                  | No         |
| Repeatable read  | Yes          | No                  | No         |
| Read commited    | Yes          | Yes                 | No         |
| Read uncommitted | Yes          | Yes                 | Yes        |

## Other Important Knowledge

### Multiversion Concurrency Control

[Multiversion concurrency control](https://en.wikipedia.org/wiki/Multiversion_concurrency_control) (MCC or MVCC) is widely used in RDBMS for concurrent transactional management. The idea is to have multiple snapshots for concurrent transactions to achieve isolation.

### ACID

[ACID](https://en.wikipedia.org/wiki/ACID) stands for Atomicity, Consistency, Isolation and Durability.
