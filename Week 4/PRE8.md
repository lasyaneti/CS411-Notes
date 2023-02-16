# PART1: Introduction to Normalization (Schema Refinement)

## Desirable Properties of Relationships
1. **lossless**: must preserve the information of R 
2. must have minimum amount of redundancy
3. must be "dependency preserving"
4. good query performance! (optional because might conflict with 1-3)

## Normal Forms 
- DB Schemas that follow certain rules made by DB researchers = **normalization** is coverting scheme to fit these rules 

## Functional Dependencies 
- If two tuples agree on attributes (A_1, A2_, ... A_N)
- Then they MUST also agree on attributes (B_1, B2_, ... B_N)
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
$A_1, A_2 ... A_n \arrow B_1, B_2 ... B_n$