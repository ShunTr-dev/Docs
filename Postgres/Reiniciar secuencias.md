(Elementos que guardan generalmente el valor del id)

Cuando se vuelca de nuevo una bdd en una nuva el valor de los secuenciadores no se guarda, para resetearlos todos a 10000 se introduce:

```
SELECT  SETVAL(c.oid, 10000)
from pg_class c JOIN pg_namespace n 
on n.oid = c.relnamespace 
where c.relkind = 'S' and n.nspname = 'public' ;
```
Para listar las secuencias:

```
 SELECT c.relname FROM pg_class c WHERE c.relkind = 'S';
```