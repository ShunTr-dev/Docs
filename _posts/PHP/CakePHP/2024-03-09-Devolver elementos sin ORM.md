---
title: Devolver elementos sin ORM
date: 2024-03-09 00:00:00 -100
categories: [PHP, CakePHP]
tags: [herramientas]
---

# Devolver elementos sin ORM

Para recuperar elementos sin utilizar el ORM (Object-Relational Mapping) en CakePHP, puedes realizar consultas directas a la base de datos y obtener resultados como matrices en lugar de entidades. Aquí tienes un ejemplo de cómo hacerlo:

```php
$query = $articles->find();

$query->hydrate(false); // Obtener resultados como matrices en lugar de entidades

$result = $query->toList(); // Ejecutar la consulta y devolver la matriz de resultados
```

Este código crea una consulta utilizando el objeto `$articles`, luego se establece `hydrate(false)` para obtener los resultados como matrices en lugar de entidades. Finalmente, se ejecuta la consulta y se devuelve la matriz de resultados utilizando `toList()`. Esto te proporcionará los resultados directamente como matrices sin procesar, lo que puede ser útil en algunos casos donde no necesitas trabajar con entidades ORM.