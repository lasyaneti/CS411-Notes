# PRE1 The Relational Data Model 

## What is a Data Model? 
- Data model is a notion used to describe data or information 
    - **Structure**: how is it stored physically, the relation?
    - **Operation**: how to retrieve data, make changes and update the data?
    - **Constraints**: database usually describes real-world application, therefore has limitations.
- Ex: relational model (SQL), document (JSON), graph model (NeoJ4)

## Relational Data Model 
- Simplified design - we interact with the relations, i.e. tables, not the data itself 
- Describe the data and operations mathematically to allow for sophisticated queries 

## Table Structure 
- **Name**: name of table
- **Attributes**: name of columns 
- **Schema**: structure or definition of table - includes name, attributes, domain, etc. This is fixed!
- **Domain**: datatype stored in attribute, set of allowable values 
- **Instance**: records that exist in database. This is not fixed!
- **Size**: cardinality, # of rows vs. degree/arity, # of cols
- **Table keys**: value must be unique so we can uniquely identify data, AKA primary key when connecting tables. There can be more than one key in a table.
- **Foreign key**: points to primary key so we can connect tables. Ex: bank accounts have unique key, diposit table referencing that primary key to ensure we aren't dispositing to a nonexistant bank account. 

## Schema Specification
1. Select tables, name each table
2. Select columns for each table, give each column a domain
3. Specify key
4. Specify all appripriate foreign keys

## Example Database Schema 
relation(attribute:domain)
- STUDENT(netid:int, name:string)
- COURSE(cid:string, subj:string, sem:char\[3])

## Popular Database Systems using Relational Data Model 
- Oracle, MS SQL Server, mySQL, PostgreSQL, SQLLite, Microsoft Access

[Link to lecture](https://mediaspace.illinois.edu/media/t/1_qo56f9be)