# MongoDB

## Table of Contents

- [](#)

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