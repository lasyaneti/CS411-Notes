# Graph Data Model
- graph databases are better than relational databases to represent large datasets 
- node:
  - can have more than 1 label, key-val pairs
  - has system-assigned id 
  - there is a reference node (starting point)
- edges: 
  - directed but can be traversed in any direction 
  - have types: key-val pairs 

### Why Graph Databases 
- no need to perform joins 
- performance is much better
- flexible: no need to define scheme upfront 
- agility: graph data model if schema-free, 

# Neo4j Cypher Part 1
CYPHER is the query language for Neo4j 
- syntax is similar to SQL 
- **paterns** describe path connecting nodes, **identifiers** allow us to refer same node

![](/assets/pre22.1.png)

### Queries 
- MATCH
- WHERE
- RETURN 

### Query Nodes
Get all people nodes 
```cypher
MATCH(x:Person)
RETURN x
```

Get Tom Hanks dob
```cypher
MATCH(x:Person{name:"Tom_Hanks"})
RETURN x.born
```

### Query Relationships 
- relationship type: `-[:KNOWS]->` or `<-[:LIKE]-`
- variable name: `-[rel:KNOWS]->` before the colon
- additional properties `-[rel:KNOWS{since:2018}]->`

```cypher
MATCH(x:Person{name: "Tom Hanks"})-->(y:Movie)
RETURN y
```

### Patterns
Types of pattern matching 
- friend of a friend 
```
(user)-[:KNOWS]-(friend)-[:KNOWS]-(foaf)
```

- shortest path within 5 hops
```
path = shortestPath((user)-[:KNOWS*..5]-(other))
```

- collaborative filtering 
```
(user-[:PURCHASED]->(product)<-[:PURCHASED]-()-[:PURCHASED]->(otherProduct))
```

### Deleting 
Delete a node 
```cypher
MATCH(p:Person{name:"Abdu"})
DELETE p;
```

Delete a node and all it's relationships
```cypher
MATCH(a:Person{name:"Abdu"})
DETACH DELETE a;
```

Delete a property 
```cypher
MATCH (abdu: {name: "Abdu"})
REMOVE abdu.age
RETURN abdu
```

### Updating 
```cypher 
MATCH (n: {name: "Abdu"})
SET n.name = "Abdussalam"
RETURN n
```

Updating property for each 
```cypher
MATCH p=(begin)-[*]->(END)
WHERE begin.name="A" AND END.name="D"
FOREACH (n IN nodes(p) | SET n.marked=TRUE)
```

### Merging
checks if data exists before creating, combination of MATCH or CREATE. if pattern already exists, it creates it, if part of the pattern exists but another part doesn't, it keeps the existing part and creates the new part.

```cypher
MATCH (m:Person {name:"Abdu"})
MERGE (m)-[:Words_With]->(s:Person {name:"Susan"})
RETURN m,s
```
