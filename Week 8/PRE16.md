# Relational Algebra
- Uranary   R -> R
- Binary    R x R -> R

RA is set-based so we need to use distinct in all the SQL queries to make it equivalent 

![](/assets/16.3.jpg)

![](/assets/16.4.jpeg)

# Building Complex RA Expressions
1. Sequence of assignments
2. Expressions with several operators 
3. Expression trees = logical query plan, physical query plan

# Introduction to Physical Operators
Logical operators tell us what they do (union, selection, project, join, group) vs. physical operators tells us how they do it (nested loop, sort merge, hash join, index join)

Cost parameters 
- M = num of blocks that fit in main memory
- B(R) = num of blocks needed to hold R (best case # blocks)
- T(R) = num of tuples in R (worse case # blocks)
- V(R, a) = num of distinct values of attribute a

Compute cost to READ but NOT cost to write 

### Iterator mode
Each physical operation is implemented by 3 functions 
- open 
- getnext 
- close 

Enables pipelining! 

### Classification of physical operators 
Classification 1
- sorting-based
- hash-based
- index-based

Classification 2
- one pass (reading data only once from disk)
- two pass 
- multipass (no limit on datasize)

Classification 3
- blocking (pipelining won't work with these)
- nonblocking (can use iterator model)

Metrics 
- I/O cost = how many blocks to read to perform iteartion 
- Buffer requirement = how large memory should be perform operation
