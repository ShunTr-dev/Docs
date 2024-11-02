---
title: MongoDB básico
date: 2024-08-20 00:00:00 -100
categories: [MongoDB]
tags: [mongodb, basico]
---
# Guía Básica de MongoDB

MongoDB es una base de datos NoSQL orientada a documentos que utiliza una estructura flexible de esquemas para almacenar datos en documentos JSON. Esta guía cubre los comandos básicos para manejar bases de datos y colecciones, además de operaciones comunes de CRUD, búsqueda avanzada y actualización en MongoDB.

Sintácticamente Mongo cambia un poco a lo que respecta de las BDD SQL, tenemos `Documentos` en vez de `Tuplas` y `Colecciones` en vez de `Tablas`.

---

## Mostrar Bases de Datos y Selección de Base de Datos

1. **Mostrar todas las bases de datos**:
   ```js
   show dbs
   ```
   Muestra una lista de todas las bases de datos existentes.

2. **Imprimir la base de datos actual**:
   ```js
   db
   ```
   Muestra la base de datos seleccionada actualmente.

3. **Seleccionar (o crear) una base de datos**:
   ```js
   use shop
   ```
   La base de datos `shop` se creará solo cuando se haga la primera inserción.

---

## Eliminar Bases de Datos y Colecciones

Para eliminar una base de datos o colección, simplemente selecciónala y usa los comandos correspondientes.

1. **Eliminar una base de datos completa**:
   ```js
   use nombreBaseDatos
   db.dropDatabase()
   ```
   
2. **Eliminar una colección específica**:
   ```js
   db.nombreColeccion.drop()
   ```

---

## Crear Colección con Validación de Esquema

Podemos crear una colección con validación de esquema para asegurar que los documentos cumplan ciertos criterios:

```js
db.createCollection("posts", { 
    validator: { 
        $jsonSchema: { 
            bsonType: "object", 
            required: ["title", "text", "creator"]
        } 
    } 
})
```

---

## Insertar Documentos

1. **Insertar un solo documento**:
   ```js
   db.coll.insertOne({name: "Max"})
   ```

2. **Insertar varios documentos**:
   ```js
   db.coll.insertMany([{name: "Max"}, {name: "Alex"}])
   ```

3. **Insertar con `ordered: false` (continúa incluso si algunos documentos fallan)**:
   ```js
   db.coll.insertMany([{name: "Max"}, {name: "Alex"}], {ordered: false})
   ```

4. **Insertar Control de Escritura con `writeConcern`**:
   ```js
   db.coll.insert({name: "Max"}, {writeConcern: {w: "majority", wtimeout: 5000}})
   ```

   **Control de Escritura**: Puedes especificar el nivel de confirmación con `w` y el tiempo de espera con `wtimeout`.

5. **Inserción de fechas**:
   ```js
   db.coll.insert({date: ISODate()})
   ```

---

## Buscar Documentos

1. **Buscar un documento (devuelve el primero encontrado)**:
   ```js
   db.coll.findOne()
   ```

2. **Buscar varios documentos**:
   ```js
   db.coll.find()
   ```

   Devuelve un cursor con los 20 primeros resultados.

3. **Búsqueda con filtro y formato legible**:
   ```js
   db.coll.find({name: "Max", age: 32}).pretty()
   ```

4. **Buscar con operadores de comparación**:
   ```js
   db.coll.find({year: {$gt: 1970}})   // greater than
   b.coll.find({"year": {$gte: 1970}}) // greater than or equal
   db.coll.find({"year": {$lt: 1970}}) // lower than
   db.coll.find({"year": {$lte: 1970}})
   db.coll.find({"year": {$ne: 1970}}) // not equal
   db.coll.find({"year": {$in: [1958, 1959]}})
   db.coll.find({"year": {$nin: [1958, 1959]}})
   ```

5. **Búsqueda con expresiones lógicas**:
   ```js
   db.coll.find({$or: [{year: 1958}, {year: 1959}]})
   db.coll.find({name:{$not: {$eq: "Max"}}})
   db.coll.find({$or: [{"year" : 1958}, {"year" : 1959}]})
   db.coll.find({$nor: [{price: 1.99}, {sale: true}]})
   db.coll.find({
   $and: [
      {$or: [{qty: {$lt :10}}, {qty :{$gt: 50}}]},
      {$or: [{sale: true}, {price: {$lt: 5 }}]}
   ]
   })
   ```

6. **Búsqueda con expresiones regulares**:
   ```js
   db.coll.find({name: /^Max/})   // comienza con "Max"
   db.coll.find({name: /^Max$/i}) // case insensitive
   ```

7. **Búsqueda en arreglos**:
   ```js
   db.coll.find({tags: {$all: ["Realm", "Charts"]}}) // para que la búsqueda no sea literal y no busque el MISMO ORDEN
   db.coll.find({field: {$size: 2}}) // impossible to index - prefer storing the size of the array & update it
   db.coll.find({results: {$elemMatch: {product: "xyz", score: {$gte: 8}}}})
   ```

8. **Buscar con proyección para limitar los campos**:
   ```js
   db.coll.find({x: 1}, {actors: 1})   // solo muestra el campo "actors" y "_id"
   ```

9. **Ordenar, omitir y limitar resultados**:
   ```js
   db.coll.find().sort({year: 1}).skip(10).limit(3)
   ```

10. **Buscar con `readConcern`**:
    ```js
    db.coll.find().readConcern("majority")
    ```

11. **Buscar fechas**:
    ```js
    db.coll.find({date: ISODate("2020-09-25T13:57:17.180Z")})
    ```

12. **Contar Documentos:**
   ```javascript
   db.coll.count({age: 32})          // estimation based on collection metadata
   db.coll.estimatedDocumentCount()  // estimation based on collection metadata
   db.coll.countDocuments({age: 32}) // alias for an aggregation pipeline - accurate count
   ```

13. **Ejecutar una Operación con `explain()` para obtener estadísticas detalladas**

El método `explain()` ayuda a obtener detalles sobre cómo MongoDB ejecuta una consulta.

```js
db.coll.find({name: "Max", age: 32}).explain("executionStats")
```








```js
db.coll.find({"status.description": "description"}).pretty() // To access children
db.coll.find({elements: ["Exact element"]}) // Para sacar un elemento literalmente con ese contenido
db.coll.distinct("name")


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


```





























---

## Actualizar Documentos

1. **Actualizar un solo campo con `updateOne()`**:
   ```js
   db.coll.updateOne({_id: 1}, {$set: {year: 2016}})
   ```

2. **Actualizar múltiples campos con `updateMany()`**:
   ```js
   db.coll.updateMany({year: 1999}, {$set: {decade: "90's"}})
   ```

3. **Operaciones de incremento y multiplicación**:
   ```js
   db.coll.update({_id: 1}, {$inc: {year: 5}})
   db.coll.update({_id: 1}, {$mul: {price: 1.25}})
   ```

4. **Eliminar Campos (unset) o Renombrarlos (rename):**
   ```javascript
   db.coleccion.update({"_id": 1}, {$unset: {"year": 1}})
   db.coleccion.update({"_id": 1}, {$rename: {"year": "date"}})
   ```

4. **Actualizar Elementos en Arrays:**
   - Añadir un elemento:
     ```javascript
     db.coleccion.update({"_id": 1}, {$push: {"array": 1}})
     ```
   - Quitar un elemento:
     ```javascript
     db.coleccion.update({"_id": 1}, {$pull: {"array": 1}})
     ```
   - Añadir sin duplicados:
     ```javascript
     db.coleccion.update({"_id": 1}, {$addToSet: {"array": 2}})
     ```
   
   ```js
   db.coll.update({"_id": 1}, {$pop: {"array": 1}})  // last element
   db.coll.update({"_id": 1}, {$pop: {"array": -1}}) // first element
   db.coll.update({"_id": 1}, {$pullAll: {"array" :[3, 4, 5]}})
   db.coll.update({"_id": 1}, {$push: {scores: {$each: [90, 92, 85]}}})
   db.coll.updateOne({"_id": 1, "grades": 80}, {$set: {"grades.$": 82}})
   db.coll.updateMany({}, {$inc: {"grades.$[]": 10}}) // para que sea en todos los elementos
   db.coll.update({}, {$set: {"grades.$[element]": 100}}, {multi: true, arrayFilters: [{"element": {$gte: 100}}]}) // "element" es un filtro
   ```

5. **Buscar y actualizar con `findOneAndUpdate()`**:
   ```js
   db.coll.findOneAndUpdate({name: "Max"}, {$inc: {points: 5}}, {returnNewDocument: true})
   ```

6. **Usar `upsert` para actualizar o crear si no existe**:
   ```js
   db.coll.updateOne({_id: 1}, {$set: {item: "apple"}, $setOnInsert: {defaultQty: 100}}, {upsert: true})
   ```













```js
db.coll.update({"_id": 1}, {$min: {"imdb": 5}}) // si el valor seleccionado es menor que el que hay en la bdd se cambia
db.coll.update({"_id": 1}, {$max: {"imdb": 8}}) // si el valor seleccionado es mayor que el que hay en la bdd se cambia
db.coll.update({"_id": 1}, {$currentDate: {"lastModified": true}})
db.coll.update({"_id": 1}, {$currentDate: {"lastModified": {$type: "timestamp"}}})


// Update many
db.coll.update({"year": 1999}, {$set: {"decade": "90's"}}, {"multi":true})
db.coll.updateMany({"year": 1999}, {$set: {"decade": "90's"}})

// Replace
db.coll.replaceOne({"name": "Max"}, {"firstname": "Maxime", "surname": "Beugnet"})

// Save
db.coll.save({"item": "book", "qty": 40})

// Write concern
db.coll.update({}, {$set: {"x": 1}}, {"writeConcern": {"w": "majority", "wtimeout": 5000}})

elementMatch se usa para cuando tenemos un array que dentro del mismo están los valores que le pasemos y desperdigados por el resto de elementos
```


























---

## Eliminar Documentos

1. **Eliminar Documentos Específicos**:
   ```js
   db.coll.remove({name: "Max"})
   ```

2. **Eliminar solo el primer documento encontrado**:
   ```js
   db.coll.remove({name: "Max"}, {justOne: true})
   ```

3. **Eliminar todos los documentos de una colección**:
   ```js
   db.coll.remove({})
   ```

   **Nota**: Esto elimina todos los documentos pero no la colección en sí.

4. **Eliminar y devolver el documento eliminado**:
   ```js
   db.coll.findOneAndDelete({name: "Max"})
   ```

---
## Funciones Adicionales y Configuración

1. **Validación de Esquema Avanzada:**
   ```javascript
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
           // más propiedades
         }
       }
     },
     validationAction: 'warn'
   });
   ```

2. **Proyecciones:**
   - Incluir o excluir campos específicos en la consulta:
     ```javascript
     db.coleccion.find({"x": 1}, {"actors": 1})  // Incluye "actors"
     db.coleccion.find({"x": 1}, {"actors": 0})  // Excluye "actors"
     ```

3. **Ordenar, Saltar y Limitar Resultados:**
   ```javascript
   db.coleccion.find({}).sort({"year": 1, "rating": -1}).skip(10).limit(3)
   ```

4. **Read Concern (Nivel de Lectura):**
   ```javascript
   db.coleccion.find().readConcern("majority")
   ```

---

## Restricciones de MongoDB y Tipos de Datos

1. **Límites de Documento:**
   - Tamaño máximo de un documento: 16 MB.
   - Máximo de niveles de anidación en un documento: 100 niveles.

2. **Tipos de Datos Importantes:**
   - **int32**: Rango máximo de ±2,147,483,647.
   - **int64**: Rango máximo de ±9,223,372,036,854,775,807.
   - **Decimal de alta precisión**:
     ```javascript
     db.coleccion.insert({precio: NumberDecimal("12.99")})
     ```



## Tipos de Datos en MongoDB

MongoDB admite varios tipos de datos con ciertos límites:

1. **Enteros**:
   - `int32` (valor máximo: ±2,147,483,647).
   - `int64` (valor máximo: ±9,223,372,036,854,775,807).

2. **Número decimal de alta precisión**:
   - `NumberDecimal("12.99")` es útil para cálculos exactos.

3. **Arreglos y objetos**:
   - Los documentos deben ser <= 16 MB.
   - Solo se permite una profundidad de anidación de hasta 100 niveles.

4. **Convertir tipos de datos en controladores (ejemplo en Node.js)**:
   ```js
   const Long = require('mongodb').Long;
   db.collection('wealth').insert({value: Long.fromString("121949898291")});
   ```

---

## Enlaces útiles

- [Operadores de consulta](https://docs.mongodb.com/manual/reference/operator/query/)
- [Documentación de Insertar](https://docs.mongodb.com/manual/reference/method/db.collection.insertOne/)
- [Documentación de Actualización](https://docs.mongodb.com/manual/tutorial/update-documents/)
- [Documentación de Eliminación](https://docs.mongodb.com/manual/tutorial/remove-documents/)
- [Límites de MongoDB](https://docs.mongodb.com/manual/reference/limits/)
- [Tipos de datos de MongoDB](https://docs.mongodb.com/manual/reference/bson-types/)
