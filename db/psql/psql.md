# PostgreSQL

## Table of Contents

- [Introduction](#introduction)
- [Connect to DBMS](#connect-to-dbms)
- [Manage Users](#manage-users)
- [Manage DBs](#manage-dbs)
- [Manage Schemas](#manage-schemas)
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

## Manage Schemas

A `schema` is a **named collection of tables, view, functions, constraints, indexes, sequences and more**. PostgreSQL supports having multiple schemas inside a single database.

Schemas can be used for different features but also for different environments. For instance, if a team is developping an application. Each member can work on a separate issue without worrying for affecting an other member's work.

Show current schema
```sql
SELECT current_schema();
```

List all schemas
```sql
\dn
```

Switch from one schema to another
```sql
SET search_path TO schema_name;
```

Create a new schema and grant all privileges for a user
```sql
CREATE SCHEMA schema_name AUTHORIZATION user_X;
```

## Manage DBs

Show current database
```sql
SELECT current_database();
```

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