Aggregation Framework - RETRIEVING DATA EFFICIENTLY AND IN A STRUCTURED WAY

https://www.mongodb.com/docs/manual/aggregation/

```
db.orders.aggregate( [{
   // Stage 1: FILTER
   $match: { size: "medium" }
},{
   // Stage 2: GROUP remaining documents by pizza name and calculate total quantity
   $group: { _id: "$name", totalQuantity: { $sum: "$quantity" } }
}] )
```

The $match stage:

-   Filters the pizza order documents to pizzas with a size of medium.
-   Passes the remaining documents to the $group stage.
    The $group stage:
-   Groups the remaining documents by pizza name.
-   Uses $sum to calculate the total order quantity for each pizza name. The total is stored in the totalQuantity field returned by the aggregation pipeline.

```
//Sacar las personas female agrupadas por estado
db.persons.aggregate([
    { $match: { gender: 'female' } },
    { $group: { _id: { state: "$location.state" }, totalPersons: { $sum: 1 } } },
        // Le asignamos un DOCUMENT al ID,
        // esto se interpretará de una manera especial que permitira agrupar los campos
        // totalPersons es una key
        // sumamos 1 por cada uno que encuentre
    { $sort: { totalPersons: -1 } }
        // solo podemos ordernar TRAS tener totalPersons
]).pretty();
```

```
db.persons.aggregate([{
  $project: {
    _id: 0,
    name: 1, // le tenemos que pasar los elementos que van a ser usados en el siguiente STAGE (project)
    email: 1,
    //birthdate: { $convert: { input: '$dob.date', to: 'date' } },
    birthdate: { $toDate: '$dob.date' },
    age: "$dob.age",
    location: {
      type: 'Point',
      coordinates: [
        {
          $convert: { // Parsing de datos ya que si no se pasan como string
            input: '$location.coordinates.longitude',
            to: 'double',
            onError: 0.0,
            onNull: 0.0
          }
        },
        {
          $convert: {
            input: '$location.coordinates.latitude',
            to: 'double',
            onError: 0.0,
            onNull: 0.0
          }
        }
      ]
    }
  }
},{
  $project: {
    gender: 1,
    email: 1,
    location: 1, // este es el valor de la localización de arriba
    birthdate: 1,
    age: 1,
    fullName: {
      $concat: [
        { $toUpper: { $substrCP: ['$name.first', 0, 1] } },
        {
          $substrCP: [
            '$name.first',
            1,
            { $subtract: [{ $strLenCP: '$name.first' }, 1] }
          ]
        },
        ' ',
        { $toUpper: { $substrCP: ['$name.last', 0, 1] } },
        {
          $substrCP: [
            '$name.last',
            1,
            { $subtract: [{ $strLenCP: '$name.last' }, 1] }
          ]
        }
      ]
    }
  }
},
{ $group: { _id: { birthYear: { $isoWeekYear: "$birthdate" } }, numPersons: { $sum: 1 } } },
{ $sort: { numPersons: -1 } }
]).pretty();
```

```
db.friends.aggregate([
    { $unwind: "$hobbies" }, // divide las colecciones padre del array y si tiene dos elementos
    // crea dos elementos cada uno con un atriburo diferente
    //{ $group: { _id: { age: "$age" }, allHobbies: { $push: "$hobbies" } } }
    // introduce un elemento nuevo para cada entrada de elemento, pero como elementos en conjunto, no por separado
    { $group: { _id: { age: "$age" }, allHobbies: { $addToSet: "$hobbies" } } }
    // mete los valores pero evita valores repetidos
  ]).pretty();
```

```
db.friends.aggregate([
    { $project: { _id: 0, examScore: { $slice: ["$examScores", 2, 1] } } }
  ]).pretty();
```

```
// length of array (numero de exámenes)
db.friends.aggregate([
    { $project: { _id: 0, numScores: { $size: "$examScores" } } }
  ]).pretty();
```

```
// Exámenes con nota má sde 60
db.friends.aggregate([
    {
      $project: {
        _id: 0,
        scores: { $filter: { input: '$examScores', as: 'sc', cond: { $gt: ["$$sc.score", 60] } } }
        // tiene $$ por que filter necesita la variable temporal para realizar la itenrancia, y se escribe así
      }
    }
  ]).pretty();
```

```
// La mayor puntuación para cada persona
db.friends.aggregate([
    { $unwind: "$examScores" },
    { $project: { _id: 1, name: 1, age: 1, score: "$examScores.score" } },
    { $sort: { score: -1 } },
    { $group: { _id: "$_id", name: { $first: "$name" }, maxScore: { $max: "$score" } } },
    { $sort: { maxScore: -1 } }
  ]).pretty();
```

```
// Agrupar personas por edad

db.persons
  .aggregate([
    {
      $bucket: { // Agrupar los datos en bloques para hacer cosas con los datos
        groupBy: '$dob.age',
        boundaries: [18, 30, 40, 50, 60, 120], // Categorías
        output: {
          numPersons: { $sum: 1 },
          averageAge: { $avg: '$dob.age' }
        }
      }
    }
  ])
  .pretty();

db.persons.aggregate([
    {
      $bucketAuto: { // De manera automática, devuelve un array con los tramos
        groupBy: '$dob.age',
        buckets: 5,
        output: {
          numPersons: { $sum: 1 },
          averageAge: { $avg: '$dob.age' }
        }
      }
    }
  ]).pretty();
```

```
// Pagination
db.persons.aggregate([
    { $match: { gender: "male" } },
    { $project: { _id: 0, gender: 1, name: { $concat: ["$name.first", " ", "$name.last"] }, birthdate: { $toDate: "$dob.date" } } },
    { $sort: { birthdate: 1 } },
    { $skip: 10 },
    { $limit: 10 } // limita el número de entradas que queremos ver
  ]).pretty();
```

MongoDB actually tries its best to optimize your Aggregation Pipelines without interfering with your logic.
Learn more about the default optimizations MongoDB performs in this article: https://docs.mongodb.com/manual/core/aggregation-pipeline-optimization/

```
{ $out: "transformedPersons" } // Puedes añadirlo al final de un aggregate para crear una colección nueva con la respuesta

// creamos el indice para poder hacer los cálculos
db.transformedPersons.createIndex({location: "2dsphere"})

//
db.transformedPersons.aggregate([
    {
      $geoNear: { // Encuenta elementos en la coleccion que están cerca de nuestro punto
        near: {
          type: 'Point',
          coordinates: [-18.4, -42.8]
        },
        maxDistance: 1000000,
        num: 10,
        query: { age: { $gt: 30 } },
        distanceField: "distance"
      }
    }
  ]).pretty();
```

Helpful Articles/ Docs:

-   Official Aggregation Framework Docs: https://docs.mongodb.com/manual/core/aggregation-pipeline/
-   Learn more about $cond: https://docs.mongodb.com/manual/reference/operator/aggregation/cond/
