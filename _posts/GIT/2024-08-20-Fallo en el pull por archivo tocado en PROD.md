---
title: Fallo en el pull por archivo tocado en PROD
date: 2024-08-20 00:00:00 -100
categories: [GIT]
tags: [herramientas]
---

# Solución para el fallo en el pull por archivo tocado en PROD

Si has tenido un fallo al intentar hacer un pull debido a un archivo modificado en el entorno de producción, puedes seguir estos pasos para resolverlo:

1. Volver al commit anterior al último en el que se modificó el archivo en cuestión en el entorno de producción. Esto se puede hacer con el siguiente comando:

```bash
git checkout HEAD^ file/to/overwrite
```

Este comando deshace los cambios en el archivo `file/to/overwrite` y lo vuelve al estado en el commit anterior al último.

2. Una vez que el archivo ha sido revertido al estado anterior, intenta hacer el pull nuevamente para obtener los últimos cambios del repositorio remoto:

```bash
git pull
```

Con estos pasos, deberías poder hacer el pull sin problemas y tener el archivo en el estado deseado en tu entorno de desarrollo.
