# PRE4 Database Updates

## Database Modifications
### Insert 
```sql
INSERT INTO Likes
VALUES("Lasya", "Chai");

-- or --

INSERT INTO Likes(drink, customer)
VALUES("Chai", "Lasya");
```
Can also insert multiple tuples seperated by comma

### Delete
```sql
SELECT * FROM Likes
-- DELETE FROM Likes -> also possible but LESS COMMON, prefer SEELCT * 
WHERE customer 
```

Delete multiple drinks produced by same manufacturers 
```sql
DELETE FROM Drinks 
WHERE name IN (
    FROM Drinks b1, Drinks b2
    WHERE b1.manf = b2.manf AND 
    b1.name <> b2.name
)
```

### Update
```sql
UPDATE Customer 
SET phone = '555-1212-'
WHERE name = 'Fred';
```