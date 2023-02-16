# PART1: Introduction to Normalization (Schema Refinement)

## Desirable Properties of Relationships
1. **lossless**: must preserve the information of R 
2. must have minimum amount of redundancy
3. must be "dependency preserving"
4. good query performance! (optional because might conflict with 1-3)

## Normal Forms 
- DB Schemas that follow certain rules made by DB researchers = **normalization** is coverting scheme to fit these rules 

## Functional Dependencies 
- If two tuples agree on attributes ($A_1, A_2, ... A_N$)
- Then they MUST also agree on attributes ($B_1, B_2, ... B_N$)
- We should see the same value, **same idea as key-value pairs**
- EX: ssn to employee name 
- NOT AN EX: bday to ssn
- **UNLIKE key-value constraints FDs are not enforced!** 

## Anomalies 
- UPDATE ANOMALY: people might update one attribute but forget to update the others in that attribute. 
- INSERT ANOMALY: cannot insert into an attribute till there is at least one entity to fit it
- DELETE ANOMALY: if an entity is deleted, it might impact the whole attribute 

## Process
1. Identify all non-trivial FDs
2. Identify those that are implied by keys
3. Identify troublesome FDs

# PART2: Functional Dependencies

## Keys (review)
- Key has to be **minimal** (no subset of the fields comprise a key is a key) set of attributes 
- Every key is automatically a superkey, but not every superkey is a key

## Splitting/Combining Rule 
Funtional dependency of the form $A_1, A_2 ... A_n \rightarrow B_1, B_2 ... B_m$ is equivalent to (breaking down only RHS)
- $A_1, A_2 ... A_n \rightarrow B_1$;
- $A_1, A_2 ... A_n \rightarrow B_2$;
- ... 
- $A_1, A_2 ... A_n \rightarrow B_m$;

The reverse is true for combining, all RHS can be combined into one if same LHS

## Inference Rules for FDs
Trivial dependency $A_1, A_2, .. A_n \rightarrow A_1$ because set of attributes contains the key (for example), which is the result value we want ($A_1$ in this case).

## EXAMPLE Closure of Set of Attributes 
- Set of attributes $A, B, C, D, E, F$
- List of FDs (all RHS are singleton, no need to split)
    1. $A B \rightarrow C$
    2. $A D \rightarrow E$
    3. $B \rightarrow D$
    4. $A F \rightarrow B$
- **CLOSURE OF** {{$A, B$}}$^+$ is {{$A, B, C, D, E$}} because
    - A gives us A (trivial dependency)
    - B gives us B (trivial dependency)
    - FD (1) gives us C
    - FD (3) gives us D
    - given D, applying FD (2) gives us E
- **CLOSURE OF** {{$A, F$}}$^+$ is {{$A, F, B, C, D, E$}} because
    - A gives us A
    - F gives us F
    - FD (4) gives us B 
    - given B, FD (1) gives us C
    - given B, FD (3) gives us D
    - given D, FD (2) gives us E
    - **THIS IS A SUPER KEY** it has all attributes! 

## Finding Keys
- LEFT = attributes only in LHS of FDs
- MIDDLE = attributes in some LHS and some RHS of FDs
- RIGHT = attributes only in RHS of FDs
- NONE = attributes appear in none of the FDs

Computer the attribute closure for the **LEFT & NONE** together are see where it takes us, in the example above it was $AF$

## Computing Attribute Closure for ALL FDs
1. Computer $X+$ for every attribute X 
2. Enumerate all FDs $X \rightarrow Y$ such that $Y \subseteq X+$ and $X \cap Y = \emptyset$