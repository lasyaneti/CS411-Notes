
# An Overview of Data Models

### What is a data model?
- **Data Model**: Notation for describing data/information
- Has three main parts:
	- Structure of the Data: How the data is actually stored within a DB
	- Operations on the Data: What do we want to be able to do with the data?
	- Constraints on the Data: Basically limitations for how the data works

### Important Data Models
- Two data models:
	- Relational Model (all commercial database management systems)
	- Semistructured-data model

### The Relational Model in Brief
![[Pasted image 20230214112717.png]]
- Based on tables
- Might APPEAR similar to an array of structs, but this isn't guaranteed
	- i.e. might be too large to keep the whole database in memory
	- Large study of databases involves actual storage of these systems
- Relational Algebra formed  by all the operations possible in a relation

### The Semistructured Model in Brief
- Resembles trees or graphs, rather than tables or arrays
	- i.e. nested elements within XML
- Operations typically involve following paths down (i.e. BFS/DFS)
- Constraints depend on the types of values associated with a tag
	- i.e. is a string a date?

### Comparison of Modeling Approaches
Our Requirements:
- Databases are large
- Must have efficient access to data and modifications
- Must make programmers' lives easy
Relational model is great at doing this!

# Basics of the Relational Model
![[Pasted image 20230214112717.png]]
We have a simple way to represent data: a 2D table, called a relation
- Row represents an item
- Column represents a property of the item

### Attributes
- Columns of a relation
- Describes the meaning of entries in that column

### Schemas
- Name of a relation and set of its attributes
- i.e  `Movies(title, year, length, genre)`
- Note that attributes are a set, not a sequence (order is irrelevant)
- We still need a standard order, defined as the standard order
- Database Schema: Set of schemas in a database

### Tuples
- Each item within the actual database
- Has one nullable component for each attribute in the database
- Note that we need to keep in mind the relations involved with the tuple

### Domains 
- Each component of the tuple must be atomic (single element)
	- Cannot be a struct/list/set/array
- Therefore, each attribute must be a domain (type)
- Can be implicit or explicit, although explicit is better
- `Movies(title:string, year:integer, length:integer, genre:string)`

### Equivalent Relations
- Note that relations are sets of tuples, not lists of tuples
	- Order of items isn't deterministic
- Can also reorder the attributes (if we also change the columns) - many permutations

![[Pasted image 20230214112717.png]]
![[Pasted image 20230214113925.png]]

### Relation Instances
- Relations change over time
- Schema doesn't change as often (VERY EXPENSIVE)
- Instance: A set of tuples in a relation for the relation
- Current instance: Present (most up-to-date) instance

### Keys of Relations
- Lots of constraints, but KEYS are important
- Key: A set of attributes such that no two tuples can have the same value in all attributes of the key
- Express this with an underline
- Many companies try to create unique artificial keys, which they enforce 
	- i.e. employee IDs or SSNs


# Defining a Relation Schema in SQL
Two aspects to SQL:
- Data-Definition: Declaring database schemas
- Data-Manipulation: Querying and modifying databases

### Relations in SQL
3 types of relations:
- Stored Relations: Called tables, we deal with these normally
- Views: Relations defined by a computation. Aren't stored, just queried when needed.
- Temp Tables: Created in a query, thrown away and not stored.

### Data Types:
- Character strings of fixed length: `CHAR(n)` or `VARCHAR(n)`
	- Note that char adds padding, while varying doesnt
- Bitstrings of fixed length: `BIT(n)` or `BIT VARYING (n)`
- Logical attributes: `BOOLEAN` (T, F, U)
- Integers: `INT`/`INTEGER`, or `SHORTINT`
- Floating point numbers: `FLOAT`/`REAL`, `DOUBLE PRECISION`, `DECIMAL(n,d)``, `NUMERIC`
- Dates: `DATE`
- Times: `TIME`

### Simple Table Declarations
- Keyword `CREATE TABLE`, followed by a list of the relation/attribute names/types
```SQL
CREATE TABLE Movies (
	title CHAR(IOO),
	year INT,
	length INT,
	genre CHAR(10),
	studioName CHAR(30),
	producerC# INT
);
```

### Modifying Relation Schemas
- To delete a table, we can drop it: `DROP TABLE R`
- Alternatively, we can insert or remove columns with `ALTER TABLE R ADD/DROP X`

### Default Values
- Generally are inserted as NULL
- Can use the `DEFAULT` keyword to initialize them as something else

### Declaring Keys
- Can declare an attribute to be a key when listed in relational schema
- Can add a declaration that defines a key
- Two methods to indicate keyness:
	- `PRIMARY KEY`: May not be NULL
	- `UNIQUE`: More implicit, but permits NULL terms

#  Rules about Functional Dependencies

### Reasoning About Functional Dependencies
```If we are told that a relation R(A, B, C) satisfies the FD’s
A—>B and B—>C, then we can deduce that R also satisfies the FD A—>C.
How does that reasoning go? To prove that A—>C, we must consider two
tuples of R that agree on A and prove they also agree on C.
```

- Prove this by creating two tuples, that must agree on A.
- Then, they must agree on B.
- Then, they must agree on C.

We define:
- Equivalent Functional Dependencies: Set of instances satisfying FD S is the same as set of instances satisfying FD T
- Follows: Defines a subset operation, larger value in the set

### The Splitting/Combining Rule
- We can split up the right hand side of functional dependencies
	- i.e. if both B and C depend on A, then they also depend on A individually
- Can also do the inverse, and combine these