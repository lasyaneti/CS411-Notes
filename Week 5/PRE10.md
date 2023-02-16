Normal forms: first normal (all attributes are atomic), second normal (old and obselete), this PRE introduces 2 more
# PART1: Boyce-Codd Normal Form (BCNF)
## Main Idea
$X \rightarrow A$ is OK if $X$ is a superkey, else we must decompose the table

## EXAMPLE - PERSON
- Attibutes: Person(name, SSN, age, eyecolor, phone, haircolor)
- FD 1: SSN $\rightarrow$ name, age, eyecolor
- FD 2: age $\rightarrow$ haircolor

Combining FD 1 and 2 we know that  SSN $\rightarrow$ name, age, eyecolor, haircolor

**Iteration 1** split based on combined FD
- Person(SSN, name, age, eyecolor, haircolor)
- Phone(SSN, phone)

**Iteration 2** split based on FD 2 age $\rightarrow$ haircolor
- Person(SSN, name, age, eyecolor) **FD1**
- Hair(age, haircolor) **FD2**
- Phone(SSN, phone) **No FDs**

We are now in BCNF

## Properties of BCNF
- BCNF decomposition is not unique
- BNCF removes ALL redundancies based on FDs 
- BNCF avoids information loss 
- FAILS to preserve dependency

# PART2: Third Normal Form (3NF)
DEFINITION 
- WHENEVER there is a nontrivial dependency $A_1, A_2, ... A_n \rightarrow B$ for R
- THEN $A_1, A_2, ... A_n$ is a super key
- OR $B$ is part of a key 

## Minimal Basis 
- Basis with all RHS singletons, where any modifications lead to no longer a basis 
- Remove unnecessary attributes from LHS --> rule COMPACT = cannot drop any attribute from LHS and still maintain schema
- Remove FDs that can be inferred --> rule SMALL # of RULES = cannot drop any rules, minimal and still maintain schema

## EXAMPLE 
R(A, B, C) with
1. FD1 $A \rightarrow BC$
2. FD2 $B \rightarrow AC$
3. FD3 $C \rightarrow AB$

Basis is 
1. $A \rightarrow B$
2. $A \rightarrow C$
3. $B \rightarrow A$
4. $B \rightarrow C$
5. $C \rightarrow A$
5. $C \rightarrow B$

MINIMAL basis is 
1. $A \rightarrow B$
2. $B \rightarrow C$
3. $C \rightarrow A$

## 3NF algorithm 
1. get minimal basis given FDs
2. for each FD $a \rightarrow B$ in minimal basis G, use $AB$ as schema for new relation
3. keep going until superkey is found 

**Result will be lossless and dependency-preserving in 3NF** but may not be in BCNF (can't say)