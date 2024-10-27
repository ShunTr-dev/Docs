---
title: Crear un repo
date: 2020-01-01 00:00:00 -100
categories: [GIT]
tags: [git]     # TAG names should always be lowercase
---

# Crear un repositorio

En esta guía se detallan los pasos necesarios para crear un nuevo repositorio desde cero y añadirlo a un servidor remoto.

## Inicializar el repositorio local

El primer paso es inicializar un nuevo repositorio local en el directorio del proyecto. Utilizamos el siguiente comando:

```bash
git init
```

## Añadir archivos al repositorio

Una vez inicializado el repositorio, añadimos todos los archivos al área de preparación utilizando el siguiente comando:

```bash
git add .
```

También añadimos el archivo `.gitignore` si es necesario, para especificar qué archivos y directorios queremos ignorar en el repositorio:

```bash
git add .gitignore
```

## Asociar un repositorio remoto

Después de añadir los archivos al repositorio local, asociamos un repositorio remoto utilizando el siguiente comando:

```bash
git remote add origin git@bitbucket.org:primate_vault/moncake.git
```

## Realizar el primer commit

Una vez que los archivos están en el área de preparación, realizamos el primer commit con un mensaje descriptivo:

```bash
git commit -m "First commit"
```

## Subir los cambios al repositorio remoto

Finalmente, subimos los cambios al repositorio remoto utilizando el siguiente comando:

```bash
git push -u origin master
```

## Cambiar la URL del repositorio remoto (en caso de error)

En caso de que se produzca un error debido a que el origen remoto ya existe, podemos cambiar la URL del repositorio remoto utilizando el siguiente comando:

```bash
git remote set-url origin https://ShunTr@bitbucket.org/primatehiberica/beeclock.git
```

Este comando nos permite cambiar la URL del origen remoto y resolver el error.

Con estos pasos, habremos creado un nuevo repositorio local, asociado un repositorio remoto y subido los cambios al servidor remoto.
