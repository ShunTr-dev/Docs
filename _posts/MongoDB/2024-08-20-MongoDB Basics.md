---
title: MongoDB Basics
date: 2024-08-20 00:00:00 -100
categories: [MongoDB]
tags: [mongodb]
---

show dbs //Show Databases
db // prints the current database

use shop // crea la base de datos cuando se cree la PRIMERA inserción

To get rid of your data, you can simply load the database you want to get rid of (use databaseName) and then execute db.dropDatabase().
Similarly, you could get rid of a single collection in a database via db.myCollection.drop().

Create collection with validation
db.createCollection("posts", { validator: {$jsonSchema: { bsonType: "object", required: ["title, text, creator"]} } })

explain() antes de lo que quiera hacer verbose de lo que pasa

-   executionsStats

```js
db.runCommand({
  collMod: 'posts',
  validator: {
    $jsonSchema: {
      bsonType: 'object',
      required: ['title', 'text', 'creator', 'comments'],
      properties: {
        title: {
          bsonType: 'string',
          description: 'must be a string and is required'
        },
        text: {
          bsonType: 'string',
          description: 'must be a string and is required'
        },
        creator: {
          bsonType: 'objectId',
          description: 'must be an objectid and is required'
        },
        comments: {
          bsonType: 'array',
          description: 'must be an array and is required',
          items: {
            bsonType: 'object',
            required: ['text', 'author'],
            properties: {
              text: {
                bsonType: 'string',
                description: 'must be a string and is required'
              },
              author: {
                bsonType: 'objectId',
                description: 'must be an objectid and is required'
              }
            }
          }
        }
      }
    }
  },
  validationAction: 'warn'
});
```

CREATE

```js
db.coll.insertOne({name: "Max"})
db.coll.insertMany([{name: "Max"}, {name:"Alex"}])
db.coll.insertMany([{name: "Max"}, {name:"Alex"}], {ordered: false}) //continua metiendo datos aunque algo falle
// insert se puede usar pero está NO recomendado
db.coll.insert([{name: "Max"}, {name:"Alex"}]) // ordered bulk insert
db.coll.insert([{name: "Max"}, {name:"Alex"}], {ordered: false}) // unordered bulk insert
db.coll.insert({date: ISODate()})
db.coll.insert({name: "Max"}, {"writeConcern": {"w": "majority", "wtimeout": 5000}})
```

-   insertOne(): https://docs.mongodb.com/manual/reference/method/db.collection.insertOne/
-   insertMany(): https://docs.mongodb.com/manual/reference/method/db.collection.insertMany/
-   Atomicity: https://docs.mongodb.com/manual/core/write-operations-atomicity/#atomicity
-   Write Concern: https://docs.mongodb.com/manual/reference/write-concern/
-   Using mongoimport: https://docs.mongodb.com/manual/reference/program/mongoimport/index.html

FIND

```js
db.coll.findOne() // returns a single document (the first that finds)
db.coll.find()    // returns a cursor - show 20 results - "it" to display more
db.coll.find().pretty() //human readable
db.coll.find({name: "Max", age: 32}) // implicit logical "AND".
db.coll.find({date: ISODate("2020-09-25T13:57:17.180Z")})
db.coll.find({name: "Max", age: 32}).explain("executionStats") // or "queryPlanner" or "allPlansExecution"
db.coll.find({"status.description": "description"}).pretty() // To access children
db.coll.find({elements: ["Exact element"]}) // Para sacar un elemento literalmente con ese contenido
db.coll.distinct("name")

// Count
db.coll.count({age: 32})          // estimation based on collection metadata
db.coll.estimatedDocumentCount()  // estimation based on collection metadata
db.coll.countDocuments({age: 32}) // alias for an aggregation pipeline - accurate count

// Comparison
db.coll.find({"year": {$gt: 1970}}) // greater than
db.coll.find({"year": {$gte: 1970}}) // greater than or equal
db.coll.find({"year": {$lt: 1970}}) // lower than
db.coll.find({"year": {$lte: 1970}})
db.coll.find({"year": {$ne: 1970}}) // not equial
db.coll.find({"year": {$in: [1958, 1959]}})
db.coll.find({"year": {$nin: [1958, 1959]}})

// Logical
db.coll.find({name:{$not: {$eq: "Max"}}})
db.coll.find({$or: [{"year" : 1958}, {"year" : 1959}]})
db.coll.find({$nor: [{price: 1.99}, {sale: true}]})
db.coll.find({
  $and: [
    {$or: [{qty: {$lt :10}}, {qty :{$gt: 50}}]},
    {$or: [{sale: true}, {price: {$lt: 5 }}]}
  ]
})

// Element
db.coll.find({name: {$exists: true}})
db.coll.find({"zipCode": {$type: 2 }})
db.coll.find({"zipCode": {$type: "string"}})

// Aggregation Pipeline
db.coll.aggregate([
  {$match: {status: "A"}},
  {$group: {_id: "$cust_id", total: {$sum: "$amount"}}},
  {$sort: {total: -1}}
])

// Text search with a "text" index
db.coll.find({$text: {$search: "cake"}}, {score: {$meta: "textScore"}}).sort({score: {$meta: "textScore"}})

// Regex
db.coll.find({name: /^Max/})   // regex: starts by letter "M"
db.coll.find({name: /^Max$/i}) // regex case insensitive

// Array
db.coll.find({tags: {$all: ["Realm", "Charts"]}}) // para que la búsqueda no sea literal y no busque el MISMO ORDEN
db.coll.find({field: {$size: 2}}) // impossible to index - prefer storing the size of the array & update it
db.coll.find({results: {$elemMatch: {product: "xyz", score: {$gte: 8}}}})

// expresions
db.coll.find({$expr: {$gt : ["val1", "val2"]}}) //Esto no funciona por que es literalmente una comparación de carácteres
db.coll.find({$expr: {$gt : ["$val1", "$val2"]}})
db.coll.find({$expr: {$gt : [{$cond: {if: {$gte: ["$val1", 90]}, then: {$subtract: ["$val1", 10]}, else: "$val1" }}, "$target"]}})

// Cursors
db.coll.find().next() //siempre nos va a devolver el artículo 21, para que devuelva el resto tenemos que usar un cursor
const dataCursor = db.coll.find()
dataCursor.next();
dataCursor.forEach(doc => {printjson(doc)})
dataCursor.hasNext


// Projections
db.coll.find({"x": 1}, {"actors": 1})               // actors + _id
db.coll.find({"x": 1}, {"actors": 1, "_id": 0})     // actors
db.coll.find({"x": 1}, {"actors": 0, "summary": 0}) // all but "actors" and "summary"

// Sort, skip, limit
db.coll.find({}).sort({"year": 1, "rating": -1}).skip(10).limit(3) // 1 ascendente, -1 desdendente

// Read Concern
db.coll.find().readConcern("majority")
```

-   https://www.mongodb.com/docs/manual/reference/operator/query/
-   More on find(): https://docs.mongodb.com/manual/reference/method/db.collection.find/
-   More on Cursors: https://docs.mongodb.com/manual/tutorial/iterate-a-cursor/
-   Query Operator Reference: https://docs.mongodb.com/manual/reference/operator/query/

UPDATE

```js
db.coll.updateOne({$set: {values} })

unset // quita campos
rename

db.coll.update({"_id": 1}, {"year": 2016}) // WARNING! Replaces the entire document
db.coll.update({"_id": 1}, {$set: {"year": 2016, name: "Max"}})
db.coll.update({"_id": 1}, {$unset: {"year": 1}})
db.coll.update({"_id": 1}, {$rename: {"year": "date"} })
db.coll.update({"_id": 1}, {$inc: {"year": 5}}) // incrementa los años en 5
db.coll.update({"_id": 1}, {$mul: {price: NumberDecimal("1.25"), qty: 2}}) // multiplica por el valor
db.coll.update({"_id": 1}, {$min: {"imdb": 5}}) // si el valor seleccionado es menor que el que hay en la bdd se cambia
db.coll.update({"_id": 1}, {$max: {"imdb": 8}}) // si el valor seleccionado es mayor que el que hay en la bdd se cambia
db.coll.update({"_id": 1}, {$currentDate: {"lastModified": true}})
db.coll.update({"_id": 1}, {$currentDate: {"lastModified": {$type: "timestamp"}}})

// Array
db.coll.update({"_id": 1}, {$push :{"array": 1}})
db.coll.update({"_id": 1}, {$pull :{"array": 1}}) // saca elementos array
db.coll.update({"_id": 1}, {$addToSet :{"array": 2}}) // añade sin meter duplicados
db.coll.update({"_id": 1}, {$pop: {"array": 1}})  // last element
db.coll.update({"_id": 1}, {$pop: {"array": -1}}) // first element
db.coll.update({"_id": 1}, {$pullAll: {"array" :[3, 4, 5]}})
db.coll.update({"_id": 1}, {$push: {scores: {$each: [90, 92, 85]}}})
db.coll.updateOne({"_id": 1, "grades": 80}, {$set: {"grades.$": 82}})
db.coll.updateMany({}, {$inc: {"grades.$[]": 10}}) // para que sea en todos los elementos
db.coll.update({}, {$set: {"grades.$[element]": 100}}, {multi: true, arrayFilters: [{"element": {$gte: 100}}]}) // "element" es un filtro

// Update many
db.coll.update({"year": 1999}, {$set: {"decade": "90's"}}, {"multi":true})
db.coll.updateMany({"year": 1999}, {$set: {"decade": "90's"}})

// FindOneAndUpdate
db.coll.findOneAndUpdate({"name": "Max"}, {$inc: {"points": 5}}, {returnNewDocument: true})

// Upsert
db.coll.updateOne({"_id": 1}, {$set: {item: "apple"}, $setOnInsert: {defaultQty: 100}}, {upsert: true}) // si el documento no existe lo crea

// Replace
db.coll.replaceOne({"name": "Max"}, {"firstname": "Maxime", "surname": "Beugnet"})

// Save
db.coll.save({"item": "book", "qty": 40})

// Write concern
db.coll.update({}, {$set: {"x": 1}}, {"writeConcern": {"w": "majority", "wtimeout": 5000}})
```

elementMatch se usa para cuando tenemos un array que dentro del mismo están los valores que le pasemos y desperdigados por el resto de elementos

Official Document Updating Docs: https://docs.mongodb.com/manual/tutorial/update-documents/

DELETE

```js
delete, deleteMany¿?

db.coll.remove({name: "Max"})
db.coll.remove({name: "Max"}, {justOne: true})
db.coll.remove({}) // WARNING! Deletes all the docs but not the collection itself and its index definitions
db.coll.remove({name: "Max"}, {"writeConcern": {"w": "majority", "wtimeout": 5000}})
db.coll.findOneAndDelete({"name": "Max"})
```

-   Official Document Deletion Docs: https://docs.mongodb.com/manual/tutorial/remove-documents/

---

-   Learn more about the MongoDB Drivers: https://docs.mongodb.com/ecosystem/drivers/
-   Dive into the official Getting Started Docs: https://docs.mongodb.com/manual/tutorial/getting-started/
-   The MongoDB Limits: https://docs.mongodb.com/manual/reference/limits/
-   The MongoDB Data Types: https://docs.mongodb.com/manual/reference/bson-types/
-   More on Schema Validation: https://docs.mongodb.com/manual/core/schema-validation/

DATA TYPES

MongoDB has a couple of hard limits - most importantly, a single document in a collection (including all embedded documents it might have) must be <= 16mb. Additionally, you may only have 100 levels of embedded documents.
You can find all limits (in great detail) here: https://docs.mongodb.com/manual/reference/limits/
For the data types, MongoDB supports, you find a detailed overview on this page: https://docs.mongodb.com/manual/reference/bson-types/
Important data type limits are:

-   Normal integers (int32) can hold a maximum value of +-2,147,483,647
-   Long integers (int64) can hold a maximum value of +-9,223,372,036,854,775,807
-   Text can be as long as you want - the limit is the 16mb restriction for the overall document
    It's also important to understand the difference between int32 (NumberInt), int64 (NumberLong) and a normal number as you can enter it in the shell. The same goes for a normal double and NumberDecimal.
    NumberInt creates a int32 value => NumberInt(55)
    NumberLong creates a int64 value => NumberLong(7489729384792)
    If you just use a number (e.g. insertOne({a: 1}), this will get added as a normal double into the database. The reason for this is that the shell is based on JS which only knows float/ double values and doesn't differ between integers and floats.
    NumberDecimal creates a high-precision double value => NumberDecimal("12.99") => This can be helpful for cases where you need (many) exact decimal places for calculations.
    When not working with the shell but a MongoDB driver for your app programming language (e.g. PHP, .NET, Node.js, ...), you can use the driver to create these specific numbers.
    Example for Node.js: http://mongodb.github.io/node-mongodb-native/3.1/api/Long.html
    This will allow you to build a NumberLong value like this:

```js
const Long = require('mongodb').Long;

db.collection('wealth').insert( {
    value: Long.fromString("121949898291")
});
```

By browsing the API docs for the driver you're using, you'll be able to identify the methods for building int32s, int64s etc.
