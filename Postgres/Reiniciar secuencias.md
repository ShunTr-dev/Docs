# Reiniciar secuencias en PostgreSQL

En ocasiones, al volcar nuevamente una base de datos en un nuevo entorno, los valores de los secuenciadores no se conservan. Para restablecer todos los valores de las secuencias a 10000, se puede utilizar la siguiente consulta SQL:

```sql
SELECT SETVAL(c.oid, 10000)
FROM pg_class c JOIN pg_namespace n 
ON n.oid = c.relnamespace 
WHERE c.relkind = 'S' AND n.nspname = 'public';
```

Para listar las secuencias existentes en la base de datos, se puede ejecutar la siguiente consulta:

```sql
SELECT c.relname FROM pg_class c WHERE c.relkind = 'S';
```

Estos comandos pueden resultar útiles al administrar secuencias en PostgreSQL y garantizar que estén correctamente configuradas para su uso en la base de datos.