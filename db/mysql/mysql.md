# MySQL

## Table of Contents

- [Service](#service)
- [Connection](#connection)
- [Most Used](#most-used)
    - [Navigation](#navigation)
- [MySQL Storage Engines](#mysql-storage-engines)

## Service

Start service
```bash
sudo /etc/init.d/mysql start
```

Stop service
```bash
sudo /etc/init.d/mysql stop
```

Restart service
```bash
sudo /etc/init.d/mysql start
```

## Connection
First connection :

```bash
sudo mysql -u root
```

Normal connection :

```bash
mysql -p
```

## Most used

### Navigation
> List all databases
```sql
SHOW DATABASES;
```
> Select a database
```sql
USE dbname;
```
> List all tables inside a database
```sql
SHOW TABLES;
```

> See columns information of a table
```sql
DESCRIBE tablename;
```

## MySQL Storage Engines

There are 2 possible **storage engines** for MySQL:
1. InnoDB (default storage engine) => relational databases
2. MyISAM                          => operational database

|       **Engine Name**      |               **MyISAM**              |                       **InnoDB**                      |
|:--------------------------:|:-------------------------------------:|:-----------------------------------------------------:|
|      **Release Date**      |              2009 (older)             |                          2010                         |
|      **Transactional**     |                   No                  |                          Yes                          |
|          **ACID**          |                   No                  |                          Yes                          |
|       **Performance**      |          Faster to read date          | Higher speed when dealing with a large amount of data |
| **Foreign Key Constraint** |             Not supported             |                          Yes                          |
|    **Row-Level Locking**   |                   No                  |                          Yes                          |
|   **Table-Level Locking**  |                  Yes                  |                           No                          |
|   **Internal Mechanism**   | Stores everything into a single table |   Each row is stored separately in a separate table   |

## MySQL Indexes

Indexes are a powerful feature in modern DMBS. Depending on the used DBMS, the internal mechanisms can be different. However, the goal remains the same. It is used to query faster on a bunch of specific columns.

In MySQL, indexes use **pointers** and **internal tables** which are maintained sorted. By doing so, it is possible to use the **Binary Search Algorithm** (FR: Recherche Dichotomique) to retrieve data quicker `O(log(n))` instead of `O(n)` for a row-by-row search.

It make queries a lot faster by hundred of milliseconds.

In the below diagram, `PX` represents the pointers used by the **index table**.

![mysql-indexes](/db/mysql/resources/mysql-indexes.png)