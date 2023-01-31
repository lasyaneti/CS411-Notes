# PRE4 Stored Procedures

- Procedures are stored as static objects, not dynamic - can be changed but is complicated 
- Works like a function, set of queries, that can be executed


```sql
CREATE PROCEDURE sp_name 
    (proc_parameter, ...)
BEGIN
-- execution code
END;
```

proc_parameter
- [IN | OUT | INOUT] param_name and param_type 

## Ex: returns first & last name and avg gpa of student 
```sql
DELIMITER // -- this command changes delimiter from ";" to "//"
CREATE PRODECUDE GetAvgScore()
BEGIN
    SELECT s.FirstName, s.LastName, AVG(Score) as avgScore 
    FROM Enrollments e JOIN Students s ON (e.NetId = s.NetId)
    GROUP BY s.NetId;
END //
DELIMITER ; -- resets delimiter to ";"

-- calling the prodecure --
GetAvgScore()
```

## Cursor 
Cursors are used to iterate through a set of rows returned by a query so that we can process each individual row.

```sql
DELIMITER //
CREATE PROCEDURE GetTotalStds(IN dept VARCHAR(30), out TOTAL INT)
BEGIN
    DECLARE totalStds INT DEFAULT 0
    SELECT COUNT (*)
    INTO total
    FROM Students 
    WHERE Department=dept;

    SELECT totalStds;
END //
DELIMETER ;

-- calling procedure 
CALL GetTotalStds("CS", @total);
-- getting result from procedure call
SELECT @total;
```