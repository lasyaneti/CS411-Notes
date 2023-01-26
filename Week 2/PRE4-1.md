# PRE4 Advanced SQL: Grouping and Aggregation 

## Aggregations
- SUM
- AVE 
```sql
SELECT AVG(price)
FROM Sells
WHERE drink = "Mocha";
```
- COUNT
```sql
-- COUNT ALL
COUNT(*) 
-- counts number of tuples
-- but counts NULLS and duplicates 

-- VS DISTINCT --
SELECT COUNT(DISCOUNT price)
FROM Sells
WHERE drink = "Mocha";
-- only counts unique prices 
-- excludes NULLs
```
- MIN
- MAX 

## Grouping 
```sql
SELECT drink, AVG(price) -- third, averages all drinks grouped by price 
FROM Sells -- first 
GROUP BY drink; -- second 
```

## HAVING clauses 
```sql
SELECT drink, AVG(price) -- third 
FROM Sells -- first
-- if there was a WHERE, it would go before HAVING
GROUP BY drink -- second
HAVING COUNT(cafe) >= 3 -- fourth, excludes DRINK GROUP where cafe count is not >= 3 
```