# PRE4 Advanced SQL: Views

- Views are defined queries, i.e. query with a name 
- Views are virtual tables
```sql
CREATE VIEW <name> AS <query>;
```
- **Base table** already exists when we use CREATE TABLE command 

```sql
CREATE VIEW CanDrink AS
    SELECT customer, drink
    FROM Frequents, Sells
    WHERE Frequents.cafe = Sells.cafe 


-- accessing a view 
-- hidden execution of creating CanDrink 
SELECT drink FROM CanDrink 
WHERE customer = "Sally"; 
```

## Why Views?
- Security reasons, not all admins need all information of users in database
- Simplifies how you write queries 
- Important for transformation, how to integrate and migrate data 

## Views Should Stay Fresh!
- They should be up to date with the BASE TABLE 
- Must propagate view changes to base relations 
- Some views are NOT updatable!!!!! You just cannot propogate view changes 

## Updatable Views
- Very strict rules
- NO aggregates, NO distinct 
- Defined as a single base table 
- Only selection and projection allowed 