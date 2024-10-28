---
title: Geospatial Queries
date: 2024-08-20 00:00:00 -100
categories: [MongoDB]
tags: [mongodb]
---

```js
location: {
      type: "Point",
      coordinates: [-73.856077, 40.848447]
}

db.coll.find({location: {$near: {$geometry: { type: "Point", coordinates: {-73.84, 40.22}}}}}) // Buscar elementos cercanos al elemento dado
                                                                                               // Falla por que se necesitan índices

db.coll.createIndex({location: "2dsphere"})
db.coll.find({location: {$near: {$geometry: { type: "Point", coordinates: [-73.84, 40.22]}, $maxDistance: 30, $minDistance: 10}}})
// Le pasamos las distancias mínimas y máximas que se le pueden dar a la consulta. EN METROS



const p1 = [-122.4547, 37.77473]
const p2 = [-122.45303, 37.76641]
const p3 = [-122.51026, 37.76411]
const p4 = [-122.51088, 37.77131]

db.coll.find({location: {$geoWithin: {$geometry: {type: "Polygon", coordinates: [[p1, p2, p3, p4, p1]]}}}})
// Traer los elementos dentro de los puntos
// Se tiene que volver a añadir el punto inicial para marcar que se terminó

```

```
Mirar si el usuario está dentro del área
geointersects: Muestra si un punto está dentro de un área
```

```
Devuelve el area con el que corta
```

```
saber los elementos que están en un radio. Los valores se tienen que convertir que están en radianes
```
