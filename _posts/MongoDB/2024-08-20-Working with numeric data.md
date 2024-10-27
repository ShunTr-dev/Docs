---
title: Working with numeric data
date: 2024-08-20 00:00:00 -100
categories: [MongoDB]
tags: [herramientas]
---

There's one important thing you have to keep in mind about the MongoDB Shell (which we're using via the mongo command): It is based on JavaScript, it's running on JavaScript.
Hence you can use JavaScript syntax in there and hence the default data types are the default JavaScript data types.
That matters especially for the numbers. JavaScript does NOT differentiate between integers and floating point numbers => Every number is a 64bit float instead.
So 12 and 12.0 are exactly the same number in JavaScript and therefore also in the Shell.

Useful Articles/ Docs:

-   Float vs Double vs Decimal - A Discussion on Precision: https://stackoverflow.com/questions/618535/difference-between-decimal-float-and-double-in-net
-   Number Ranges: https://social.msdn.microsoft.com/Forums/vstudio/en-US/d2f723c7-f00a-4600-945a-72da23cbc53d/can-anyone-explain-clearly-about-float-vs-decimal-vs-double-?forum=csharpgeneral
-   Modelling Number/ Monetary Data in MongoDB: https://docs.mongodb.com/manual/tutorial/model-monetary-data/
