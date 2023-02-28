# PRE12: Introduction to B+ Trees

## Why?
- Index can be very large
- We need data structures such as B+ trees to have quicker access 

## B+Tree Basics 
- 3 levels: root, internal nodes, leaf (index entry)
- Leaf node has `n` number of search keys and `n+1` pointers 
- Once down at the lead level, you have scan that leaf level, you can't just go back up the levels 
- Data is sorted just CS 225 B Trees
    - Everything on the left is less than search key 
    - Everything on the right is greater than search key 
- `d` is the degree, `n` is max keys 
    - When `n` is even, each node has [2, 2d] keys except root 
- `d` is the minimum amount it needs to be full 

## B+Treein Practice 
- Typical fill factor is 66.5% 
- Height 4 = $133^2$ records 
- Height 3 = $133^3$ records 

We want all indices in memory! 
- Level 1 = 1 page = 8 kb 
- Level 2 = 133 pages = 1 mb
- Level 3 = 17689 pages = 133 mb

## More
B+Trees don't always help, ex: array of sorted ints 

### Exact key value
```sql
SELECT name FROM people WHERE age=20
```

### Range queries 
```sql
SELECT name FROM people WHERE age>=20 and age<=70
```