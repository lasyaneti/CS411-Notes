# Serializability Theory

### Schedules
- Sequence of interleaved actions from a set of trasactions, where the actions of each individual transactions are the SAME as the original order 
- Example 
    - Trasactions: T1 -> T1-a T1-b T1-c ; T2 -> T2-x T2-y T2-z ;
    - Schedule: T1-a T2-x T1-b T1-c T2-y T2-z
    - abc and xyz order cannot be changed! 

### Serial Schedules
- Simplest way to organize schedules: avoid all concurrency 
- Not efficient at all because every trasaction runs entirely one by one in a series 
- Optimization requires interleaving 

### Serializable Schedule
- Result is equivalent to serial schedule, if you walk through all the steps it will update values in the same way 
- Non-serialiazable schedule is one that doesn't result in the same output as a serial schedule 

### Conflict Serializibility 
- Conflicts: WR, RW, WW 
- Schedule is conflict serializable if it can be transformed into a serial schedule by a series of **swapping non-conflicting ADJACENT actions** 
- By definition is a serializable schedule, but cannot assume the other way other 
- Usually used to **gauruntee serializability**
- Testing this: schedule is conflict serializabile IFF **precedence graph** contains no cycles
    - Vertices = all transactions 
    - Edges = Ti -> Tj if Ti precedes & conflicts with an action of Tj

__This is conflict serializable!__ 

![](/assets/3-21.jpeg)

Not everytime you have a cycle means that the schedule is not serializable! EXAMPLE: **blind-write** i.e. when none of the intermediary writes matter because the last action is a write that would overwrite all previous writes. 

### View Equivalent / View Serializable
If any of the following cases:
- Ti reads initial A in S1, then Ti reads initial A in S2 
- Ti reads A written by Tj in S1, then Ti reads A written by Tj in S2
- Ti writes final value of A in S1, then T1 writes final value of A in S2

# Two-Phase Locking

A transaction is **well-formed** if it acquires at least 
- 1 shared lock on Q before reading Q 
- OR 1 exclusive lock on Q before writing Q and doesn't release it until the action is performed 

A transaction is **two-phased** if it never acquires a lock after unlocking one 
- growing phase = acquiring lock 
- shrinking phase = releasing lock 

If all transactions are well-formed and two-phase gauruntees serializability 

### Two Phase Locking Protocol (2PL)
Way of managaging locks where T gets locks over time as needed, T cannot request any more locks once it releases a lock

![](/assets/3-21.1.png)

Checking if "schedule can arise under 2PL", any conflict would mean it cannot arise! 

Enforcing 2PL means to give the locks and create a schedule for given transactions (https://mediaspace.illinois.edu/media/t/1_gly538y6 @ 8:00)

Problem with 2PL: unrecoverable schedule, abort cannot be written after commit 

### Strict Two Phase Locking Protocol (S2PL)
Similar to 2PL but only release locks after transaction is completed - commit / abort

![](/assets/3-21.2.png)

This solves the problem of 2PL because we now have a recoverable schedule. 