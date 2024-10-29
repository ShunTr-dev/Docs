---
title: Deshacer el último commit
date: 2024-08-20 00:00:00 -100
categories: [GIT]
tags: [git, undo, deshacer]
author: <midudev>
---

# Deshacer el Último Commit

## Si aún no has hecho `push`

1. **Para mantener los cambios en el área de staging (index):**
   ```bash
   git reset --soft HEAD~1
   ```
   Este comando deshace el último commit pero deja los cambios en el área de staging, listos para ser modificados y confirmados nuevamente si es necesario.

2. **Para eliminar los cambios completamente:**
   ```bash
   git reset --hard HEAD~1
   ```
   Esto elimina el último commit y los cambios que contenía. ⚠️ **Precaución:** Cualquier cambio en el directorio de trabajo desde el último commit se perderá.

3. **Para modificar el commit (mensaje o archivos):**
   ```bash
   git commit --amend -m "Nuevo mensaje"
   ```
   Este comando permite editar el último commit. Puedes cambiar el mensaje o añadir archivos adicionales antes de confirmar de nuevo.

## Si ya has hecho `push`

1. **Revertir el commit creando un nuevo commit de reversión:**
   ```bash
   git revert <hash_del_commit>
   ```
   Esto crea un nuevo commit que invierte los cambios del commit especificado, sin modificar el historial. Si hay conflictos, deberás resolverlos antes de continuar.

2. **Obtener el hash del commit a revertir:**
   ```bash
   git log
   ```
   Usa `git log` para encontrar el hash del commit que deseas revertir y úsalo en el comando `git revert` de arriba.

## Opciones avanzadas (Nivel experto)

1. **Editar el historial de commits localmente:**
   ```bash
   git rebase -i HEAD~n
   ```
   Con `git rebase -i`, puedes modificar el historial local de commits. Esto permite cambiar el orden, combinar, editar o eliminar commits. Reemplaza `HEAD~n` con el número de commits que deseas editar en el historial.

2. **Forzar el push tras modificar el historial:**
   ```bash
   git push --force-with-lease
   ```
   ⚠️ **Precaución:** Solo usa `rebase` y `push --force-with-lease` en ramas donde trabajas solo o en casos donde todos los colaboradores estén informados y de acuerdo en reescribir el historial.

## Explicación de los comandos y parámetros clave

- **`git reset`**: Restaura el índice y el directorio de trabajo a un commit específico.
   - `--soft`: Deshace el commit sin modificar el índice ni el directorio de trabajo, dejando los cambios en el área de staging.
   - `--hard`: Restaura el índice y el directorio de trabajo al commit especificado, eliminando cualquier cambio realizado desde ese commit.
   
- **`HEAD~1`**: Representa el commit anterior al último. `HEAD` es un puntero al último commit en la rama actual; `~1` mueve ese puntero un commit atrás.

- **`--force-with-lease`**: Es una alternativa más segura a `--force` al hacer `push`. Este comando solo forzará el `push` si tu copia local está al día respecto a la versión en el remoto, previniendo sobrescribir cambios de otros colaboradores por error.


