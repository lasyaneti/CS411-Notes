# PRE2 Structured Query Language (Joins)

## SQL: Structured Query Language
- Seperated into **DDL** (Data Definition Language) and **DML** (Data Manipulation Language) 

## Single Relational Query 
- Input can take one or more table, output is always a SINGLE table
- Accesses in order FROM -> WHERE -> SELECT

```sql
SELECT Number, Owner
FROM Account
WHERE Type = "savings";
```

**Renaming Attributes**: use **AS** keyword to rename attribute in result output table
```sql
SELECT Number AS Acc_Num, Owner
FROM Accounts
WHERE Type = "savings";
```

Modify using arithmetic expressions
```sql
SELECT cafe, drink, price * 120 AS priceInYen
```

**Creating Temporary Tables** 
```sql
SELECT Owner INTO temp3 
```

**Complex Conditions**
```sql
SELECT price
FROM Sells
WHERE cafe = "Caffe bene" AND drink = "Mocha";
```

## Patterns
- WHERE clauses can pattern-match 
- % used for any string 
- _ used for any char 

```sql
SELECT name
FROM Customers
WHERE phone LIKE '%555-_ _ _ _';
```

## Ordering 
Results are not ordered, use ORDER BY keyword to specify this (ASC is default)
```sql
SELECT * 
FROM Account
ORDER BY Balance DESC
```

**Ties** are broken with second attribute
```sql
SELECT * 
FROM Account
ORDER BY Balance, age
```

[Link to lecture](https://mediaspace.illinois.edu/media/t/1_9st5fwsn)