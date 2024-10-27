---
title: Primer commit
date: 2020-01-01 00:00:00 -100
categories: [GIT]
tags: [git, commit]     # TAG names should always be lowercase
---

## Guía para realizar un primer commit en un nuevo repositorio

A continuación se detallan los pasos necesarios para realizar el primer commit en un nuevo repositorio Git:

### 1. Añadir todos los archivos al repositorio:

Antes de realizar el commit, es necesario agregar todos los archivos al repositorio utilizando el siguiente comando:

```bash
git add .
```

Este comando añadirá todos los archivos y cambios al área de preparación para el commit.

### 2. Realizar el commit con un mensaje descriptivo:

Una vez que los archivos han sido añadidos al área de preparación, se debe realizar el commit con un mensaje descriptivo que indique los cambios realizados. Para ello, se utiliza el siguiente comando:

```bash
git commit -m "First commit"
```

Es importante proporcionar un mensaje claro y conciso que describa los cambios realizados en este commit.

### 3. Subir los cambios al repositorio remoto:

Para subir los cambios al repositorio remoto, se utiliza el comando `git push` seguido de la opción `-u` para establecer la rama local como la rama predeterminada del repositorio remoto y `origin master` para indicar que se está subiendo la rama `master` al repositorio remoto llamado `origin`:

```bash
git push -u origin master
```

### 4. Deshacer un commit en caso de error:

En caso de cometer un error al realizar el commit y subir los cambios al repositorio remoto, es posible deshacer el commit utilizando el siguiente comando:

```bash
git revert HEAD
```

Este comando deshace los cambios introducidos por el último commit y crea un nuevo commit con los cambios deshechos. Esto permite corregir errores sin perder el historial de cambios del repositorio.

---

Es importante tener en cuenta que estos pasos son para un nuevo repositorio. Si se está trabajando en un repositorio existente, se deben adaptar los pasos según sea necesario.
