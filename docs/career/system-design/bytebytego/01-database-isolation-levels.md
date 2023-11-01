---
date:
  created: 2023-10-26
  updated: 2023-10-26

tags:
  - System Design
  - ByteByteGo

comments: true
---
# What are database isolation levels? What are they used for?

## Locks

Before we discuss about isolation levels, let's review the locks used in database.

- S Lock (Shared Lock): S Lock locks the write permission for other transactions while read operation is still allowed.
- X Lock (Exclusive Lock): X Lock, on the other hand, locks both read and write operation once a transaction obtained it.

| Lock | Read | Write |
|---|---|---|
| S | Yes | No |
| X | No | No |