# Neo4j

## Table of Contents

- [Introduction](#introduction)
- [Relations](#relations)
- [Commands](#commands)

## Introduction

Neo4j is the most popular **graph-oriented** DBMS. This type of databases are used to store networks, graphs. There are nodes/vertices and edges. Neo4j is ACID compliant.

Vertices can store **properties** too.

![neo4j](/db/neo4j/resources/neo4j.png)

There are two types of graph databases:
- Properties graph (labelled graph) <-- **Neo4j**
- RDF-graph (Resource Description Framework)

Neo4j is implemented in Java. It uses the **Cypher** language for queries. 

## Nodes

Nodes represent an entity of the real world. For instance, it can be a person, a movie, an animal, etc.

Nodes can have **properties**.

## Relations

Relations **are directionals** and **have a name**:

![neo4j](/db/neo4j/resources/introduction_schema.png)

(A)-[: ACTED_IN ]->(B)

Relations can also have **properties**.

## Commands

### CREATE

#### Node

Create a node
```neo4j
CREATE (s: Software {name: 'Windows'})
```

#### Relation

Create the relation (William)-[: IS_ENNEMY_WITH ]->(Anthony)
```neo4j
MATCH (p: Person {name: 'William'})
MATCH (x: Person {name: 'Anthony'})
CREATE (p)-[:IS_ENNEMY_WITH]->(x)
```

We use MERGE to avoid duplication when we want to update an entity
```neo4j
MERGE
```

### READ

#### Nodes

Get a specific node
```neo4j
MATCH (p:Person {name: 'Jennifer'})
RETURN p;
```

Get all nodes of all types 
(**does not show relations**)
```neo4j
MATCH (p) return p
```

Get all unique nodes
```neo4j
MATCH (n) RETURN DISTINCT(n)
```

Get a node of a specific type
```
MATCH (p: Person) return p
```

Get all nodes of given type excepted...
(`<>` is the `not` operator)
```neo4j
MATCH (n: Person) WHERE n.name <> 'William' RETURN n
```

Get all nodes where attributes is between two dates
```neo4j
MATCH (n: Person) WHERE date('2000-01-01') <= n.birthdate <= date('2023-01-01') RETURN n
```

Get the nodes where names start with the letter A
```neo4j
MATCH (n: Person) WHERE n.name STARTS WITH 'A' RETURN n
```

Get the nodes where names contain the letter a or A
```neo4j
MATCH (n: Person) WHERE toLower(n.name) CONTAINS 'a' RETURN n
```

#### Relations

Show all relations  
```neo4j
MATCH p=()-[]->() RETURN p;
```

Show all nodes and relations
```no4j
MATCH (n) OPTIONAL MATCH (n)-[r]-() RETURN n, r;
```

### UPDATE

Modify a property
```neo4j
MATCH (p:Person {name: 'Jennifer'})
SET p.birthday = date('1980-01-01')
RETURN p
```

Add a property
```neo4j
MERGE (j:Person {name: 'Jennifer'})
ON CREATE SET p.age = 29
RETURN p
```

### DELETE

Delete a node/a relation
```neo4j
MERGE (p:Person {name: 'Jennifer'})
DELETE p
```

Delete all relations
```neo4j
MATCH ()-[r]-()
DELETE r
```

Delete all nodes (and consequently all relations)
```neo4j
MATCH (n) DETACH DELETE n
```

Delete a property of a node
```neo4j
MERGE (p:Person {name: 'Jennifer'})
REMOVE p.birthday
```

### Aggregators

Get Unique records only
```neo4j
DISTINCT()

MATCH (p: User) RETURN DISTINCT(p)
```

```neo4j
COUNT()
```

```neo4j
collect()
```

```neo4j
size()
```

### Tools

- `arrows.app` is a website that allows you to draw a graph and then export it to **Cypher language**.

## Other examples

Retrieve all messages SENT and FORWARDED by Katia
```neo4j
MATCH (u: User {name: 'Katia'})-[f1:SENT|REPLY_TO|FORWARD]-(m: Message)
RETURN m
```

Retrieve all users following Katia
```neo4j
MATCH (u: User)-[f:FOLLOWS]-(u2: User {name: 'Katia'})
RETURN u
```

Show the number of followers and following for each user
```neo4j
MATCH (follower: User)-[:FOLLOWS]-(targetUser: User)-[:FOLLOWS]->(following:User)
RETURN targetUser AS User, COUNT(DISTINCT(follower)) AS Followers, COUNT(DISTINCT(following)) AS Following;
```

List the users followed by each user
```neo4j
MATCH (u: User)-[f:FOLLOWS]->(u1: User) RETURN u.id AS User, COLLECT(u1.id) AS Following
```

Show the user that has posted the most messages
```neo4j
MATCH (u: User)-[:FORWARD|REPLY_TO|SENT]->(m: Message) RETURN u, COUNT(m) AS Tweets ORDER BY Tweets DESC LIMIT 1;
```