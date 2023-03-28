# The Scan Operator - Query Processing (Physical Operators)

### Scan
Table-Scan
- Given a sorted selection, we scan the relation in blocks 
- Blocks are known in system, can be traversed one by one

Index-Scan
- We have the index to find the blocks 
- Scan at index 

Sort-Scan
- We may have to sort as we read them (done for `ORDER BY` clause)
- HOW? 
	- If indexed, already sorted. 
	- Else if fits into main memory then tablescan or indexscan and sort in memory. 
	- Else if too large for memory so a multiway merge sort.

### EXAMPLE
```
m = 3, SORTED 3 BLOCKS AT A TIME. each block holds 2 values. 
data on disk: [3,9] [8,1] [7,6] [9,5] [2,0] [3,8]

step1: sort runs, COST = 2B(R)
[3,9] [8,1] [7,6] --> [1,3] [6,7] [8,9]
[9,5] [2,0] [3,8] --> [0,2] [3,5] [8,9]

step2: merge sorted runs, pick nums not used already, COST = B(R)
[R1] [R2] [min R1, min R2] --> find min 
[1,3] [0,2] [0,1] --> [0,1]
[1,3] [0,2] [2,3] --> [2,3]

[6,7] [3,5] [3,5] --> [3,5]
[6,7] [3,5] [6,7] --> [6,7]

[8,9] [8,9] [8,8] --> [8,8]
[8,9] [8,9] [9,9] --> [9,9]
```

TOTAL COST = 3B(R), ASSUMING THAT B(R) <= M(M-1)

UNCLUSTERED RELATION: T(R) + 2B(R) // what is this ?? lol .. 

# The One-Pass and Nested-Loop Join Algorithms

### When it does fit in memory
One pass algorithm
- load smaller table into memory
- load other table block by block
- cost = B(R) + B(S)

### When it does NOT fit in memory
Nested Loop join algorithm
- load M-2 blocks for R, 1 for S, 1 for output
- can be performed if we have at least 3 blocks in memory

```
for each (M-2) block r in R:
	for each block s in S:
		for each tuple r1 in r:
			for each tuple s1 in s:
				if r1 and s1 join
				output (r,s)
```

- cost = B(R)+ B(S)B(R)/(M-2) = R + outer loop
	- APPROX = B(R)B(S) / M

this is too expensive though because quadratic in cost `:(`

# Two-Pass Algorithms of Physical Operators
Binary operations (union, intersect, difference, etc.) need sort. What we sort on depends on what operation we are performing. 

Total cost: 3B(R) + 3B(S) assuming B(R) + B(S) <= M(M-1)


umm lol 