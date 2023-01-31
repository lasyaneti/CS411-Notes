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

## In-Class exercise (SQL2.10)
```sql
CREATE PROCEDURE Result()
BEGIN
    -- define local variables -- 
    DECLARE varCustomerId INT;
    DECLARE varFirstName VARCHAR(255);
    DECLARE varLastName VARCHAR(255);
    DECLARE varCustomerStatus VARCHAR(30);
    DECLARE varAvgPrice REAL;
    
    -- define and setup cursor -- 
    -- we are using extended sql because we include loops, branches, recursion -- 
    -- just sql is declarative, always define what we want -- 
    
    DECLARE exit_loop BOOLEAN DEFAULT FALSE; 

    DECLARE custCur CURSOR FOR (SELECT CustomerId, FirstName, LastName, avg(Price) as avgPrice
                                FROM Customers NATURAL JOIN Purchases 
                                GROUP BY CustomerId);
    
    -- declare cursor handler to figure out when cursor finishes --
    -- NOT FOUND is an event that is flagged when we are done reading records -- 
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET exit_loop = TRUE; 
                                
    DROP TABLE IF EXISTS NewTable;
    
    CREATE TABLE NewTable (
        CustomerID  INT Primary Key,
        FirstName VARCHAR(255),
        LastName VARCHAR(255),
        CustomerStatus VARCHAR(30)
    );
    
    -- everything runs from here -- 
    -- create loop structure to iterate through records --
    OPEN custCur;
        cloop : LOOP 
        FETCH custCur INTO varCustomerId, varFirstName, varLastName, varAvgPrice;
        IF exit_loop THEN
            LEAVE cloop;
        END IF;
    
    -- finally set status -- 
    IF varAvgPrice > 4000 THEN
        SET varCustomerStatus = "Top-Tier";
    ELSE 
        SET varCustomerStatus = "Middle-Tier";
    END IF;
    
    INSERT INTO NewTable VALUE (varCustomerId, varFirstName, varLastName, varCustomerStatus);
    
    END LOOP cloop
    
    -- important to free memory space -- 
    CLOSE custCur 
    
    -- finally obtain what question wants -- 
    SELECT CustomerId, FirstName, LastName, CustomerStatus 
    FROM NewTable
    ORDER BY CustomerId DESC 
    
END;
```