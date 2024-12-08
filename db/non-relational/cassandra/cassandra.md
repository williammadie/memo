# Cassandra

## Table of Contents

- [Introduction](#introduction)
- [cqlsh basics](#cqlsh-basics)
- [CRUD Operations](#crud-operations)

## Introduction

Cassandra uses the CQL (Cassandra Query Language). There is a CLI available called cqlsh.

The CQL syntax is highly similar to SQL which makes Cassandra very user-friendly. 

## cqlsh basics

Connect to local server instance
```bash
cqlsh -u admin -p admin 
```

Create a database (called keyspace in Cassandra)
```cassandra
CREATE KEYSPACE IF NOT EXISTS resto_NY
    WITH REPLICATION = { 'class': 'SimpleStrategy', 'replication_factor': 1};
```

List available keyspaces
```cassandra
DESC[RIBE] keyspaces;
```

Connect to a specific keyspace
```cassandra
USE resto_NY;
```

Show the structure of a specific table
```cassandra
DESC Restaurant;
```

List all tables in keyspace
```cassandra
DESC tables;
```

### CRUD Operations

#### Create

```cassandra
CREATE TABLE Restaurant (
    id INT, Name VARCHAR, borough VARCHAR, BuildingNum VARCHAR, Street VARCHAR,
    ZipCode INT, Phone text, CuisineType VARCHAR,
    PRIMARY KEY ( id )
);
```

#### Read

```cassandra
```

Get all elements in a table
```cassandra
SELECT * FROM Restaurant;
```

Filter on a column that does not have an index
```cassandra
SELECT name FROM restaurant WHERE borough = 'BROOKLYN'

InvalidRequest: Error from server: code=2200 [Invalid query] message="Cannot execute this query as it might involve data filtering and thus may have unpredictable performance. If you want to execute this query despite the performance unpredictability, use ALLOW FILTERING"

# We can execute this request with ALLOW FILTERING but it might had bad performance.
```


#### Update

#### Delete

### Cassandra specificities

#### Null Comparison

In CQL, both `!=` operator does not exist. `null` value does not exist either.

A null value is represented by `""` for a text and `0` for a number. In order to avoid obtaining null values, we can filter like that: `> 0` or `> ""`.

#### Filtering on non-indexed columns

Cassandra is not efficient at filtering columns that do not have an index. The system will show it when trying to do:
```cassandra
SELECT name FROM restaurant WHERE borough = 'BROOKLYN'
```

It can be skipped with `ALLOW FILTERING` if it is a once-in-a-while request:
```cassandra
SELECT name FROM restaurant WHERE borough = 'BROOKLYN'
```

However, if this request needs to be executed very often. It is advised to add an index on the column:
```cassandra
CREATE INDEX fk_Restaurant_borough ON restaurant (borough);
```

#### Strings

Strings are between  `''` and not `""`

#### Joins

In Cassandra, joins do not exist.