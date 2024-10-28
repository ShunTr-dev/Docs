---
title: Performance, Fault Tolerance & Deployment
date: 2024-08-20 00:00:00 -100
categories: [MongoDB]
tags: [mongodb]
---

Capped collections
Colecciones que limitas el tamaño y cuando llegas a un tamaño las entradas más viejas son eliminadas

```js
db.createCollection("log", { capped : true, size : 5242880, max : 5000 } )
```

Useful Articles/ Docs:

-   Official Docs on Replica Sets: https://docs.mongodb.com/manual/replication/
-   Official Docs on Sharding: https://docs.mongodb.com/manual/sharding/
