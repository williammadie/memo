# PostgreSQL

## Table of Contents

- [Introduction](#introduction)
- [Connect to DBMS](#connect-to-dbms)
- [Manage Users](#manage-users)
- [Manage DBs](#manage-dbs)
- [Manage Tables](#manage-tables)

## Introduction

**PostgreSQL** is a **DataBase Management System** (**DBMS**).

## Connect to DBMS

```bash
psql -U username -p 5432 -h 127.0.0.1
```

## Manage Users

List users
```sql
\du
```

Change user's password (also works for postgres)
```sql
\password username
```

## Manage DBs

List databases
```sql
\l
```

Create a Database
```sql
CREATE DATABASE db-name
```

Use the specified database (Required in order to manipulates tables of a specific database)
```sql
\c db-name
```

## Manage Tables

List tables
```sql
\dt
```