# Transaction

Pitfalls of data systems
- failurs in the middle of operations (e.g. writes)
- interruptions in the network
- race conditions
- read partially updated data

Transaction
- a way to group reads and writes into a logical unit.
- either all operations in the transaction completes (commit) or all fails (fail/rollback).
- 
