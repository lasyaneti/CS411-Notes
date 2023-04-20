# Neo4J Part 2

### Aggregation 
Supports `count`, `sum`, `avg`, `min`, `max`

```cypher
MATCH (p:Person)
RETURN count(*) as headcount;
```

All grouping stated in `RETURN` clause, no `GROUP BY` clause like in SQL

### Collect
- `collect()` collects aggregated values into a list 
```cypher
MATCH (m:Movie)<-[:ACTED_IN]-(a:Person)
RETURN m.title AS movie, collect(a.name) AS cast, count(*) AS actors
```

### UNION 
`UNION` combines the results of two statements that have the same result structure 

### WITH
`WITH` is basically return clause but doesn't finish query, just prepares the input for the next part 

```cypher
MATCH (person:Person)-[:ACTED_IN]->(m:Movie)
WITH person, count(*) AS appearances, collect(m.title) AS movies
WHERE appearances > 1
RETURN person.name, appearances, movie 
```

### Indexing, Constraints 
- Purpose of indexing = find starting point in graph 

```cypher
CREATE INDEX ON :ACTOR(name);
MATCH (p:ACTOR {name: 'Michael'}) RETURN p
```

### SQL vs Neo4J
__QUERYING__
```sql
SELECT p * 
FROM Products as p;
```

```cypher
MATCH (p:Product)
RETURN p;
```

__PROJECTING__
```sql
SELECT p.ProductName, p.UnitPrice
FROM products p 
ORDER BY p.UnitPrice
LIMIT 10;
```

```cypher
MATCH (p:Product)
RETURN p.ProductName, p.UnitPrice
ORDER BY p.UnitPrice
LIMIT 10;
```

__FILTERING__
```sql
SELECT p.ProductName, p.UnitPrice
FROM products AS p
WHERE p.ProductName='Chocolate';
```

```cypher
MATCH (p.Product)
WHERE p.ProductName = 'Chocolate';
RETURN p.ProductName, p.UnitPrice;
```

OR!!!

```cypher
MATCH (p.Product{productName:'Chocolate'})
RETURN p.ProductName, p.UnitPrice;
```

__JOINING__
```sql
SELECT DISTINCT c.CompanyName
FROM customers c JOIN orders o ON (c.CustomerID = o.CustomerID)
JOIN order_details od ON (od.OrderId = o.OrderId)
JOIN products p ON (p.ProductID = od.productID)
WHERE p.ProductName='Chocolate';
```

```cypher
MATCH (p:Product{productName:'Chocolate'})<-
[:PRODUCT]-(:Order)<-[:PURCHASED]-(c:Customer)
RETURN distinct c.CompanyName;
```