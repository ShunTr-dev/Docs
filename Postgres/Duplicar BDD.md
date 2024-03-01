```
CREATE DATABASE nombrebd WITH TEMPLATE bdoriginal OWNER usuario;
```
Para realizar operaciones sobre base de datos tales como: borrar, copiar, etc. Es necesario cerrar todas las sesiones abiertas. Se puede hacer con la siguiente consulta:

```
SELECT pg_terminate_backend(pg_stat_activity.pid) FROM pg_stat_activity 
WHERE pg_stat_activity.datname = 'nombrebd' AND pid <> pg_backend_pid();
```
Lo mismo pero haciendolo por consola:

Conectarse: (si no hay bdd es necesario conectarse a la BDD de mantenimiento)

```
psql -U masterpaymeter -h paymeter.cakntrbcq6mw.eu-central-1.rds.amazonaws.com -d postgres
```
nombre de la base de datos creada: paymeter_production

```
psql -U masterpaymeter -h paymeter.cakntrbcq6mw.eu-central-1.rds.amazonaws.com -d paymeter_production
```
Para hacer una copia de seguridad de la bdd

```
pg_dump -U masterpaymeter -W -h paymeter.cakntrbcq6mw.eu-central-1.rds.amazonaws.com paymeter_production > paymeter_production.dump
```
\ Para hacer un volcado de un archivo a la bdd:

```
psql -U masterpaymeter -h paymeter.cakntrbcq6mw.eu-central-1.rds.amazonaws.com  paymeter_production < paymeter_production.dump
```