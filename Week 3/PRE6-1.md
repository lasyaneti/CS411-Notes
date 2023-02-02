# PRE6 Advanced SQL: Constraints and Triggers

## Constraints 
- Help make sure that data in databse "make sense" i.e. real-world properties are maintained 
- Constraint is relationship between data elements that databases enforce 

Examples:
- Primary keys 
- Foreign keys 
- Value based constraints 

```sql
CREATE TABLE Drinks (
    name CHAR(20) PRIMARY KEY,
    mand CHAR(20)
);

CREATE TABLE Sells (
    cafe CHAR(20),
    drink CHAR(20),
    price REAL,
    FOREIGN KEY (drink) REFERENCES Drink(name)
);
-- this way no drink that doesn't exist in drinks table can be inserted into sells table --
```

## Cascading
- Changes carry forward across tables 

```sql
CREATE TABLE Sells (
    cafe CHAR(20),
    drink CHAR(20),
    price REAL,
    FOREIGN KEY (drink) REFERENCES Drink(name)
    ON DELETE SET NULL
    ON UPDATE CASCADE
);
```

## Attribute-Based Checks 
- Place a constrain on the value of a particular attribute 
- CHECK(<\condition>) must be added to declaration for attribute 
- Checked only when a value for that attribute is inserted or updated 

## Tuple-Based Checks 
- CHECK(<\condition>) must be added to another element of schema definition 
- Checked on insert or update only 

```sql
-- no one can insert if their mocha is higher than $5 except for cafe benne -- 
CREATE TABLE Sells (
    cafe CHAR(20),
    drink CHAR(20),
    price REAL,
    CHECK (cafe = "Cafe Benne" OR price <= 5.00)
);
```

- This checks more than one attribute 


## Assertions 
- Condition may reger to any relation or attribute
- Must be true at all times 

```sql
-- must always have more customers than cafes -- 
CREATE ASSERTION FewCafe CHECK (
    (SELECT COUNT (*) FROM Cafes) <=
    (SELECT COUNT (*) FROM Customers)
) 
```