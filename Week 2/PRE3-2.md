# PRE3 Advanced SQL: Set Operations

## Union, Intersection, Difference 
(subquery) UNION (subquery)
- Must make sure both subqueries are union comparative!

```sql
-- this IS NOT union comparative
(SELECT name FROM Drink) UNION (SELECT drink FROM Sells)
-- this IS union comparative
(SELECT name FROM Drink) UNION (SELECT drink as name FROM Sells)
```

Similarly: (subquery) INTERSECT (subquery) and (subquery) EXCEPT (subquery)

## Controlling Duplicates 
- SELECT DISTINCT allows result to be a set
- UNION ALL forces the result to be a bag (doesn't eliminate duplicates)