# MongoDB

## Table of Contents

- [Basics](#basics)
- [Query Operators](#query-operators)

## Basics

Connect to a specific Database
```js
use('my_db');`
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