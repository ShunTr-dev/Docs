---
title: Duplicar BDD
date: 2024-03-09 00:00:00 -100
categories: [Postgres]
tags: [herramientas]
---

# Duplicar Base de Datos en PostgreSQL

Para duplicar una base de datos existente en PostgreSQL:

```sql
CREATE DATABASE nombrebd WITH TEMPLATE bdoriginal OWNER usuario;
```

Sin embargo, antes de realizar cualquier operación en la base de datos, como borrar o copiar, es crucial cerrar todas las sesiones abiertas relacionadas:

```sql
SELECT pg_terminate_backend(pg_stat_activity.pid) FROM pg_stat_activity 
WHERE pg_stat_activity.datname = 'nombrebd' AND pid <> pg_backend_pid();
```

Si prefieres realizar estos pasos desde la consola, aquí hay algunas instrucciones útiles:

Para conectarte a la base de datos PostgreSQL:

```bash
psql -U master_user -h paymeter.cakntrbcq6mw.eu-central-1.rds.amazonaws.com -d postgres
```

Una vez conectado, puedes seleccionar la base de datos recién creada, por ejemplo, your_database:

```bash
psql -U master_user -h server.cakntrbcq6mw.eu-central-1.rds.amazonaws.com -d your_database
```

Para realizar una copia de seguridad de la base de datos, puedes utilizar el comando `pg_dump`:

```bash
pg_dump -U master_user -W -h server.cakntrbcq6mw.eu-central-1.rds.amazonaws.com your_database > your_database.dump
```

Si deseas cargar datos desde un archivo a la base de datos:

```bash
psql -U master_user -h server.cakntrbcq6mw.eu-central-1.rds.amazonaws.com  your_database < your_database.dump
```

Estos comandos te permitirán duplicar fácilmente una base de datos en PostgreSQL, así como realizar operaciones de copia de seguridad y carga de datos desde la consola.