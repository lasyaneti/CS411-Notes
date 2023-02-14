
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
- Current Instnace: Present (most up-to-date) instance