# PRE2 Structured Query Language (Joins)

## Multi-Relation Queries (JOINS) 
- List several relations in one query to combine data from multiple relations 

```sql
SELECT A.Owner, A.Balance
FROM Account A, Deposit D
WHERE D.AcctNum = A.Number and A.Balance > 1000;
```

- Use relation.attribute to distinguish attributes with the same name
- Correlation names are local vars you can send when writing the query

## Cross Product 
```sql
SELECT * 
FROM Department, Employee
```

This creates a huge table so using a **Equijoin** helps us be more specfic 

```sql
SELECT * 
FROM Employee emp JOIN Department dept
    ON emp.DepartmentID = dept.DepartmentID
```

Now we are only outputting rows where department ID matches.

```sql
SELECT *
FROM Employee emp NATURAL JOIN Department dept 
```
More concise output because unlike Equijoin it doesn't list both emp and dept ID's (redundant because it is the same), it only outputs dept ID

## NULL Values 
Two meanings!
- **Missing value**: database on cafes, but we don't have the address yet so it can be left as NULL
- **Inapplicable**: attribute on spouses, but unmarried people will be left as NULL

## Logical conditions in SQL
- **Query only produces tuple if resulting value is 1!!!**
- TRUE = 1, FALSE = 0, UNKNOWN = 0.5
- AND = MIN, OR = MAX, NOT(x) = 1 - x

Ex: TRUE AND (FALSE OR NOT(UNKNOWN)) = MIN(1, MAX(0, (1 - 0.5))) => simplify in this manner

## NULLs and JOINs
- **Left outer join**: include left tuple even if there is no match, mostly what we use in class
- **Right outer join**: include right tuple even if there is no match
- **Full outer join**: include both tuples even if there is no match

```sql
SELECT * 
FROM Employee emp LEFT OUTER JOIN Department dept
    ON emp.DepartmentID = dept.DepartmentID
```
This includes rows with matching dept ID, but ALSO includes rows that exist in the left table but not the right table - pads with nonexist info using NULL in the resulting table 

[Link to lecture](https://mediaspace.illinois.edu/media/t/1_1j2dfx59)