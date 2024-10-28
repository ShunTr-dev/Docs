---
title: Relations
date: 2024-08-20 00:00:00 -100
categories: [MongoDB]
tags: [mongodb]
---

Relations
```js
db.books.aggregate([{$lookup: {
from: "authors", // from what other collection
localField: "authors",
foreignField: "_id",
as: "creators"
}}])

```

```
