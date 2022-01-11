# DDIA: 221-230

## Ch 7 Transactions

Transaction: 

- a way for an application to group several reads and writes together into a logical unit.

- All reads and writes in a transaction as one operation: entire succeed (commit) or entire fail (abort, rollback).

Important concepts: 

- Concurrency control

- isolation levels: read committed, snapshot isolation, serializability

  

ACID

- Atomicity
  - If the writes are grouped together into an atomic transaction, and the transaction cannot be completed (*committed*) due to a fault, then the transaction is *aborted* and the database must **discard or undo any writes** it has made so far in that transaction.
- Consistency
  - A property of the application
  - You have certain statements about your data (*invariants*) that must always be true. If a transaction starts with a database that is valid according to these invariants, and any writes during the transac‐ tion preserve the validity, then you can be sure that the invariants are always satisfied.
- Isolation
  - Concurrently executing transactions are isolated from each other.
  - *serializability*: each transaction can pretend that it is the only transaction running on the entire database. Rarely use.
  - snapshot isolation: weaker guarantee than serializability
- Durability
  - Once a transaction has com‐ mitted successfully, any data it has written will not be forgotten, even if there is a hardware fault or the database crashes
  - Perfect durability does not exist



BASE

- Do not meet the ACID criteria
- Basically Available, Soft state, and Eventual consistency



dirty read: one transaction reads another transaction’s uncommit‐ ted writes



In relational database

- Everything between `BEGIN TRANSACTION` and a `COMMIT` statement is considered to be part of the same transaction.



Single object writes

- Atomicity can be implemented using a log for crash recovery
- Isolation can be implemented using a lock on each object (allowing only one thread to acess an object at any one time)

