# Transaction

Pitfalls of data systems
- failurs in the middle of operations (e.g. writes)
- interruptions in the network
- race conditions
- read partially updated data

Transaction
- a way to group reads and writes into a logical unit.
- either all operations in the transaction completes (commit) or all fails (fail/rollback).
  - when it fails, we can safely retry.
- db provides safety guaranttees so the application don't have to deal with the messy details.
  - trade off with performance and availability
- ACID
  - atomicity
    - not about concurrency in the context of ACID
    - abortability - if a transaction is aborted then there's no side effect left.
  - consistency
    - certain statements or invariants about the data is always true.
    - depends on the application, e.g. debits and credits are balanced.
  - isolation
    - concurrently executing transaction are isolated from each other, they cannot overlap.
    - serializable: each transaction can think itself as the only transaction running on the db.
  - durability
    - once a transaction is committed, all the data it writes will not be lost even if there's a hw fault or crash.
