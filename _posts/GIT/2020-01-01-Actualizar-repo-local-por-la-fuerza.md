---
title: Actualizar repo local por la fuerza
date: 2020-01-01 00:00:00 -100
categories: [GIT]
tags: [git]     # TAG names should always be lowercase
---

## Actualizar repo local por la fuerza

Realizar con cuidado, ya que esto sobrescribirá la versión local del repositorio:

**Nota:** Tener en cuenta imágenes o archivos especiales locales.

```bash
git fetch origin
git reset --hard origin/master
chown -R www-data:www-data ./
```

### Actualizar y descargar un repo

```bash
cd ./carpeta_dev
git status
git add ./archivo_modificado.txt
git commit -m "Archivo modificado" ./archivo_modificado.txt
git push
cd ./carpeta_prod
git pull
```
