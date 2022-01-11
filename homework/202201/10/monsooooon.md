DDIA p221-p228 transaction

# introduction
## why do we need txn?  
- in real world, system is not reliable, which makes programmers take care of many things
  - hw/sw/network failure in the middle of r/w
  - concurrent r/w btw diff clients
  - race conditions for w
- the db wants to provide an easy-to-use abstraction to programmers
- txn helps to simplify progrmming model for developers

## what is txn?
- a txn is a way for an application to group several reads and writes together into a logical unit
- conceptually, all the reads and writes in a txn are executed as one operation: 
  - either the entire txn succeeds (commit) 
  - or it fails (abort, rollback). and just like nothing happened
  - if a txn fails, the app can safely retry.
- with txn, there is no partial failure

# ACID of txn
## Atomicity
atomic refers to something that cannot be broken down into smaller parts.  
in multi-thread programming, atomicity is related to data operation, but in ACID, it means "together"
- r/w in a txn is grouped together
  - if the txn cannot be committed due to a fault, then the txn is aborted and the db must discard or undo any writes
  - no partial updates! all writes done / not done
- if a txn was aborted, the application can be sure that it didn’t change anything, so it can safely be retried.

## Consistency
ACID consistency has nothing to do with distributed data replication.  
it means that you have certain statements about your data (invariants) that must always be true. 
before and after the txn, these constraints are still satisfied.
this is __NOT a db feature__. Need to be guaranteed by app developers!

## Isolation
concurrent r/w cause data race.  Isolation means that concurrently executing txns are isolated from each other
- The classic db textbooks formalize isolation as __serializability__, which means that each txn can
__pretend that it is the only txn running on the entire db__.
  - in practice, serializable isolation is rarely used, because it carries a performance penalty.

## Durability
Durability is the promise that once a transaction has committed successfully, any data it has written will not be forgotten
  - even if there is a hardware fault or the database crashes.
  - not totally durable, only to some extent
durability can be increased by data replication
