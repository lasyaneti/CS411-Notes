# PRE3 Advanced SQL: Subqueries

## Subqueries 
- Runtime error if there is no tuple or more than one tuple

```sql
SELECT cafe 
FROM Sells
WHERE drink = "Latte" AND 
price = (SELECT price
        FROM Sells
        WHERE cafe = "Cafe Benne"
        AND drink = "Mocha")
```
Example:
- Inner query (price =) will return the price for a mocha at cafe benee 
- Then we find all cafes that sell lattes at that price 

## The IN Operator 
- (tuple) in (relation) is true IFF value exists in set 

```sql
SELECT * 
FROM Drinks b1
WHERE EXISTS (SELECT * 
            FROM Sells
            WHERE drink = b1.name AND price >= 4.99)
```
Example: want to find name and manufacturer of each drink that Fred likes
- b1 refers to outer relation, thus this is a **correlation query**
- Typically want to avoid these unless it is absolutely necessary 

## The ANY Operator
- x = ANY (relation) means that x equals at least one tuple in the relation 
- x is greater than or equal to at least one tuple in the relation
- i.e. "does it match at least one"

## The ALL Operator 
- x = ALL (relation) means that for every tuple t in the relation, x != t 
- i.e. "does it match ALL of them"

```sql
SELECT drink
FROM Sells
WHERE price >= ALL(
                SELECT price 
                FROM Sells);
```
Example: find drinks with highest price without max function