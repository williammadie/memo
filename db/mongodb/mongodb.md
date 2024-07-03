# MongoDB

## Table of Contents

- [Basics](#basics)
- [Query Operators](#query-operators)
- [DB Sharding](#db-sharding)

## Introduction

Mongodb uses the MQL (MongoDB Query Language) for queries. MongoDB is not ACID compliant.

## Basics

```mongo
show dbs
```

Connect to a specific Database
```mongo
use my_db
```

List all tables
```mongo
show tables
```

Create a new collection inside the current database
```js
db.createCollection("my_collection");
```

Create a new document in the collection.
```js
db.getCollection('publis').insertOne({
    "type": "Book",
    "title": "Modern Database Systems: The Object Model, Interoperability, and Beyond.",
    "year": 1995,
    "publisher": "ACM Press and Addison-Wesley",
    "authors": [
        "Won Kim"
    ],
    "source": "DBLP"
});
```

Get all documents inside a collection
```js
db.getCollection('my_collection').find();
```
```js
[
  {
    "_id": {
      "$oid": "664711d26e6deb1c30e54f1a"
    },
    "type": "Book",
    "title": "Modern Database Systems: The Object Model, Interoperability, and Beyond.",
    "year": 1995,
    "publisher": "ACM Press and Addison-Wesley",
    "authors": [
      "Won Kim"
    ],
    "source": "DBLP"
  },
  ...
]
```

Import a json file inside collection
```bash
mongoimport --host localhost:27017 -u "root" --db test --collection publis --jsonArray --type json --file book.json --authenticationDatabase=admin
```

## Query Operators

Find documents where field is equal to a specific value
```js
db.getCollection('publis').find({"year": 2010});
db.getCollection('publis').find({"type": "Book"});

// Author name in a list of authors
db.getCollection('publis').find({"authors": "Toru Ishida"});
```

Find documents where field is greater than or equal to a specific value
```js
db.getCollection('publis').find({"year": { "$gte": 2010}});
db.getCollection('publis').find({
    "year": { "$gte": 2010},
    "type": "Book"}
);
```

Find the list of distinct values for a field
```js
db.getCollection('publis').distinct("publisher");
```

Find the publications of Toru Ishida sorted by title and by starting page
```js
db.getCollection('publis').aggregate([

    // Stage 1: Filter Books by author
    {
        "$match": {"authors": "Toru Ishida"}
    },

    // Stage 2: Sort the result by title and starting page
    // (1 for ascending)
    {
        "$sort": {"title": 1, "pages.start": 1}
    }
])
```

Include and exclude fields according to what you want in the results of your query
```js
db.getCollection('publis').aggregate([

    // Stage 1: Filter Books by author
    {
        "$match": {"authors": "Toru Ishida"}
    },

    // Stage 2: Sort the result by title and starting page
    // (1 for ascending)
    {
        "$sort": {"title": 1, "pages.start": 1}
    },

    // Stage 3: Include wanted and exclude unwanted fields
    // 1 for including and 0 for excluding
    {
        "$project": {"title": 1, "pages": 1}
    }
])
```


```js
db.getCollection('publis').aggregate([

    // Stage 1: Filter Books by author
    {
        "$match": {"authors": "Toru Ishida"}
    },

    // Stage 2: Sort the result by title and starting page
    // (1 for ascending)
    {
        "$sort": {"title": 1, "pages.start": 1}
    },

    // Stage 3: Group the results and apply an aggregation function
     
```

## Mongosh

There is a CLI tool used to work with MongoDB called `mongosh`. It can be used to connect to the DBMS.

```bash
mongosh
```

## DB Sharding

Create the following directories:
- `referee`
- `01`
- `02`
- `03`
- `04`

Launch the referee instance
```bash
mongod --replSet rs0 --port 27110 -dbpath referee --oplogSize 128 --logpath referee/referee.log --fork
```

Launch another instance
```bash
mongod --replSet rs0 --port 27111 -dbpath 01 --oplogSize 128 --logpath 01/01.log --fork
```

See all launched instances
```bash
ps -ef | grep mongo
```

Configure one instance as the `primary server`
```bash
mongosh --port 27111
```

```mongo
use admin

mine={_id:"rs0",members:[{_id:0,host:"127.0.0.1:27111"},{_id:1,host:"127.0.0.1:
27112"},{_id:2,host:"127.0.0.1:27110",arbiterOnly:true}]}

rs.initiate(mine)
```

Is the current server master?
```mongo
db.isMaster()
```

See all instances belonging to the Replica Set
```mongo
rs.status()
```

Add an instance to the Replica Set
```
rs.add("127.0.0.1:27113")
```

