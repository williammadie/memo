# SQL

## Table of Contents

- [What is a Database?](#what-is-a-database)
- [How to choose a DBMS](#how-to-properly-choose-a-dbms)
- [Types of Data](#types-of-data)
- [SQL vs NoSQL](#sql-vs-nosql)
    - [SQL](#sql)
    - [NoSQL](#nosql)
- [Operational VS Relational DBs](#operational-vs-relational-dbs)
- [SQL Cheatsheet](#sql-cheatsheet)
    - [Comments](#comments)
    - [SELECT](#select)
    - [Joint Types](#joint-types)
    - [Tables](#tables)
    - [Data](#data)
- [Example of Requests](#example-of-requests)

## What is a Database

`database`: service whose goal is to store information required to make an application run.

`DBMS`: (DataBase Management Service) it is the system software which allow end users to interact with databases.

A database supports **CRUD** operations through a DBMS:
- **C** => **Create**
- **R** => **Read**
- **U** => **Update**
- **D** => **Delete**

## How to properly choose a DBMS

- **Usage**:
    - What kind of information do you want to store?
    - How long do you want to store it?
    - Why do you want to store it?
    - How are you gonna use this information?
- **Open Source or Licensed**: Can be more or less expensive
- **Complexity of setup and usage**
- **Performance**:
    - Write/Read performances
    - Transactional support?
    - Is it good for Concurrency?
- **Popularity and Documentation**: Use tools like the **Gartner Magic Quadrant** to have a clear view of trending softwares.

## Types of Data

There are 3 main types of data:

![forms-data](/db/sql/resources/forms-data.png)


Here, we're going to detail **Structured Data** which is typically handled by **SQL Databases**.

## SQL vs NoSQL

There are 2 main types of databases which are categorized as `SQL` also called `relational` and `NoSQL`.

### SQL

`SQL`: (Structured Query Language) It refers to a language used to communicate with relational database services. It is the support used to do CRUD operations.

**SQL DBMS for Structured Data**:
- MariaDB
- Oracle
- SQL Server
- PostgreSQL
- MySQL
- SQLite
- Access (for small databases only, not secured and expensive)

SQL is used to **build** queries that allow you to **read** or **modify** data.

SQL is based on **queries**.

`query`: set of instructions used to get data out of a database.

SQL queries are divided into **2 big sub-categories** which are the following:

![dml-ddl](/db/sql/resources/dml-ddl.png)

### NoSQL

`NoSQL`: (Not Only SQL) document oriented form of storage for semi-structured data.

**NoSQL DBMS for Semi-Structured Data**:
- MongoDB
- Cassandra
- ScyllaDB
- Redis (Cache Data, Low Latency, In-Memory DB)
- ElasticSearch (Search Engine)

## Operational VS Relational DBs

DBMS can also be divided into categories. Two important categories are **RDBMS** and **Operational DB**.

`operational database`: a real-time data-gathering system where data is continuously collected.

Operational Databases ared used in weather stations, financial systems and more. Generally it stores a relatively **small amount of information** and has to **handle a lot of operations concurrently**.

`relational database`: a system organizing data based on set theory and relational algebra.

Relational Databases are the most used type of databases when it comes to Web Applications and Software Development. The idea behind it is **to manipulate them through batches**, be able to store an **important amount of information** and to **make massive write/read operations**

`batch`: set of SQL instructions/queries

MySQL and big names of DBMS support both type of databases. It only depends on the engine `InnoDB` (relational) and `MyISAM` (operational).

## Tables

`table`: logical set of columns.

A **table** is uniquely named. It has a set of attributes (columns). Each row represents a different entry.

Here is an overview of an **Employees** table:

![sql-table](/db/sql/resources/sql-table.png)

SQL Tables all follow the same rules:

![sql-table-structure](/db/sql/resources/sql-table-structure.png)


### Primary & Foreign Key

Tables contains different entries. Each row is a different entry uniquely identified by what we call a **primary key**.

`primary key`: column of a table which acts as an identifier of entries inside a table. It has to be unique and distinctive for each record/row.

Generally, all tables have a **primary key** but there are some cases where unicity is not important such as log tables for instance. These king table can have no primary key at all

Once each record is uniquely identified by a primary key, another issue comes into the equation: how can we link tables together?

Good news: if each and every tables have its own primary key, it is possible to link them (= join them) without trouble. In order to to that, we use a **foreign key** that references a **primary key** inside another table.

`foreign key`: column of a table that refers to the primary key of another table.

![primary-foreign-key](/db/sql/resources/pk-fk.png)

## Functions

## Views

## SQL Cheatsheet

### Comments

```sql
-- one line comment

/* multi-line comment */
```

### SELECT

In `SQL`, request structure is ordered. **Keywords order can't be changed**

Order of keywords:
```sql
SELECT      -- item(s), aggregates or clauses of aggregation
FROM        -- table on which we search items
WHERE       -- filter on each row of the table
JOIN        -- add information from another table
GROUP BY    -- axis of aggregation (create aggregates)
HAVING      -- filter on aggregates only
ORDER BY    -- sort the returned data
LIMIT/OFFSET       -- limit the number of returned rows and add an offset
```

Example of SQL query with HAVING clause:
```sql
SELECT col1, SUM(col2)
FROM tablename
GROUP BY col1
HAVING function(col2)
```

For a better understanding, keep in mind that the **order of the keywords inside the query** is different from the **execution order of the keywords by the DBMS**:

![sql-keywords](/db/sql/resources/sql-keyword-order.jpg)

Additional note: `JOIN + FROM` is firstly executed in the query. (it is not written on the above picture).

> SELECT Structure (Simple)
```sql
SELECT what_to_select
FROM which_table
WHERE condition_to_satisfy;
```

> Order a result (ascending order (default) 0 -> 10)
```sql
SELECT what_to_select
FROM which_table
WHERE condition_to_satisfy
ORDER BY reference_column;
```

> Order a result (descending order 10 -> 0)
```sql
SELECT what_to_select
FROM which_table
WHERE condition_to_satisfy
ORDER BY reference_column DESC;
```

> Aggregate a result
```sql
SELECT SUM(salary), department_code
FROM employee
GROUP BY department_code;
```

In the example above, we print the agregated information `SUM(salary)` and we also print the column name `department_code`. Because, we added a column without an agregated function inside the select, we have to add it to the GROUP BY.

> Filter on an aggregated funcion
```sql
SELECT SUM(salary), department_code
FROM employee
GROUP BY department_code
HAVING SUM(salary) > 50000.00;
```

Keep in mind that having is used because this kind of request is not possible:
```sql
SELECT SUM(salary), department_code
FROM employee
WHERE SUM(salary) > 50000.00
GROUP BY department_code;
```

> Join another table
```sql
SELECT employee.firstname, employee.lastname, department.code
FROM employee
LEFT OUTER JOIN department
    ON employee.department_code = department.code
ORDER BY department_code;
```

Is it possible to make a joint on the same table than the one in FROM ?

-> Yes, it is possible

> Use an alias
```sql
SELECT employee.firstname + ' ' + employee.lastname AS 'Full Name'
```

### Joins Types

- `INNER JOIN` => most used
- `NATURAL JOIN` => bad practice because can have unexpected behaviors
- `LEFT JOIN` => most used
- `RIGHT JOIN`
- `ANTI` => when we precise somthing like `ON A.key = B.key WHERE X.key IS NULL`
- `CROSS` => cartesian product

![sql-joins](/db/sql/resources/SQL_Joins.png)

### Tables

Create, Modify, Delete a table
```sql
CREATE
ALTER
DROP
```

### Data

Insert new rows in a table (no col names)
```sql
INSERT INTO tablename VALUES 
('val1', 'val2', 'valn'),
('val1', 'val2', 'valn'),
('val1', 'val2', 'valn');
```

Insert new rows in a table (with col names)
```sql
INSERT INTO tablename (col1, col2, col3) VALUES 
('val1', 'val2', 'valn'),
('val1', 'val2', 'valn'),
('val1', 'val2', 'valn');
```

Update an already existing row
```sql
UPDATE tablename
SET coln = 'valn'
WHERE col2 = 'valm';
```

## Example of Requests

![example-schema](/db/sql/resources/example-schema.png)

List clients which are in Switzerland, Germany and Belgium 
```sql
SELECT *
FROM Client
WHERE Pays IN ("Suisse", "Allemagne", "Belgique");
```

Clients with no known Fax
```sql
SELECT *
FROM Client
WHERE Fax IS NULL;
```

Clients with "restaurant" in their company's name
```sql
SELECT *
FROM Client
WHERE Societe LIKE "%restaurant%";
```

Client countries and cities order by country and city (alphabetical order)
```sql
SELECT DISTINCT Pays, Ville
FROM Client
ORDER BY Pays, Ville;
```

Product name in uppercase, reference and rename the whole thing to make it clear
```sql
SELECT UPPER(Nomprod) AS "Product Name", Refprod AS "Product Reference"
FROM Produit
WHERE NoFour = 8 AND PrixUnit >= 10 AND PrixUnit <= 100;
```

Concatenate the fields X,Y,Z...
```sql
SELECT Adresse || ", " || CodePostal || " " || Ville || ", " || Pays
FROM Client;
```

Extract the last 2 characters of client's name
```sql
SELECT SUBSTR(CodeCli, -2), CodeCli
FROM Client;
```

Replace a word by another in a given column
```sql
SELECT REPLACE(Fonction, "marketing", "mercatique")
FROM Client;
```

Look for a given word in a given column
```sql
SELECT INSTR(Fonction, "Chef")
FROM Client;
```