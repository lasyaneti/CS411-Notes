# 14.1 Introduction To Transactions

Transaction Manager is a subsystem in relational databases that ensures 

- transactions don't interfere with each other
- concurrent acesses are protected by user/system-defined rules 

Thus far we have interacted with databases that are made just for us, running independently in a docker container, no interference with more users running similar queries or queries accessing same resources. But this is not how the real world works - this is the motivation behind transactions. 

### Rules
1. Transaction is considered "unit of operation" on database
2. Either all or none execute, transactions must be atomic (can have a set of queries, select from where etc.)

### Transactions
- STATUS: success (changes in place, **commit**) vs. fail (no change, **abort or rollback**) 
- PURPOSE: concurrency control 

### ACID Properties 
- **Atomicity**: either all or none executed
- **Consistency**: each transaction executed in isolation 
- **Isolation**: effect of one transaction doesn't mess with another, if I am updating a row, no other transaction can touch it
- **Durability**: all updates stay in DBMS

```sql
set autocomit=0; -- turning off auto commit -- 

-- SQL statements --

commit; 
-- or -- 
rollback; 
```

### Transaction Types
READ-ONLY TRANSACTION
- promises the database that no updates will be made 
- now database allows concurrent reads 
- 

READ-WRITE TRANSACTION
- default mode 
- can actually update database

### Concurrent Execution Problems
**WR**: dirty read, inconsistent read
- transaction reads value written by another that is not yet committed
- ex: change made but not yet committed / rollbacked and another transaction accessed this unfinalized change

**RW**: unrepeatable read 
- transaction reads same object twice while another transaction modifies value between the two reads 

**WW**: lost update
- prohibited in all databases
- transaction makes an update, another transaction modifies even though the first one isn't done yet

**Phantom Reads**: inserting data into record WHILE another transaction is reading same records

# 14.2 Isolation Levels

### Isolation
- increased performance requires violating correctness contraints = need to find balance  

```sql
-- setting dirty read to acceptable --
SET TRANSACTION 
ISOLATION LEVEL READ UNCOMMITTED; 

-- setting unrepeatable read to acceptable --
SET TRANSACTION 
ISOLATION LEVEL READ COMMITTED; 
SET TRANSACTION 
ISOLATION LEVEL REPEATABLE READ;
```

![](/assets/pre14.png)

### Isolation Locks
- assuming for this course we are protecting at the tuple/row level, not table level
- approach to implementing isolation levels 
- LOCKED (shared or exclusive) or AVAILABLE (no lock) 
- BEFORE READ: need **shared** lock
- BEFORE WHITE: need **exclusive** lock 

![](/assets/pre14-1.png)

if transaction's requested lock is taken, it is put on **wait** (BLOCK) **until lock is granted**. 


### Levels & Locking 
- **READ UNCOMMITTED**: allows queries to read without any locks. access mode is read only, no updates allowed.
- **READ COMMITTED**: requires shared-lock but releases locks immediately after read. exclusive-lock needed for updates and kept till end of transaction.  
- **REPEATABLE READ**: holds lock until end of transaction for both shared- and exclusive-locks
- **SERIALIZABLE**: shared-lock on queries kept till end of transaction AS WELL AS INDEX 

### Notation 
- cannot change order of actions within transaction
- end of transaction is not end of schedule, make sure to release acquired locks at the right time based on the isolation level!