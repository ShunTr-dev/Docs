---
title: Manual básico
date: 2024-08-20 00:00:00 -100
categories: [GIT]
tags: [herramientas]
---

````markdown
# Guía Básica de Git

Git es un sistema de control de versiones distribuido ampliamente utilizado para el seguimiento de cambios en archivos de código fuente durante el desarrollo de software. Permite a los desarrolladores trabajar en colaboración, mantener un historial de cambios, crear ramas para el desarrollo paralelo y fusionar cambios de manera eficiente. Git es conocido por su velocidad, flexibilidad y robustez, y es fundamental en el desarrollo de software moderno.

## Herramientas Gráficas para Utilizar Git

-   Sourcetree
-   GitKraken
-   GitHub Desktop

Para comenzar, es necesario instalar Git desde [git-scm.com/downloads](https://git-scm.com/downloads). Si estás utilizando Windows, es imprescindible instalar Git BASH en lugar de utilizar la terminal de Windows.

## Configuración Inicial

```bash
git --version
git config --global user.name "Tu Nombre"
git config --global user.email tuemail@gmail.com
git config --global color.ui auto # Habilita la colorización de la salida de Git
git config --global core.editor "code --wait" # Configura VSCode como el editor por defecto
git config --global -e # Abre el archivo de configuración global en el editor
```
````

### Configuración de core.autocrlf

En entornos Windows, se utilizan los caracteres CR y LF para los saltos de línea, mientras que en Linux/Mac se utiliza solo LF. Por lo tanto, los usuarios de Windows deben configurar esto en TRUE, mientras que los usuarios de Linux/Mac deben configurarlo en INPUT.

```bash
git config --global core.autocrlf true
```

Para ver las opciones de configuración global disponibles:

```bash
git config -h
```

## Comandos Útiles

```bash
ls # Lista archivos y carpetas
pwd # Muestra la ruta actual
cd <ruta> # Cambia de directorio
mkdir # Crea un nuevo directorio
```

La opción de `git remote --verbose`, se utiliza para mostrar información detallada sobre los repositorios remotos asociados con un proyecto de Git. Esta orden mostrará tanto la URL del repositorio remoto como su nombre (por defecto, "origin") y permitirá al usuario ver qué operaciones (como push o fetch) están configuradas para cada repositorio remoto. La opción `--verbose` o `-v` muestra una salida más detallada que simplemente `git remote`.

## Iniciar un Repositorio

```bash
# En la ruta del repositorio
git init [nombre del proyecto]
git clone [URL del proyecto] # Descarga un proyecto con todo su historial desde el repositorio remoto
```

## Añadir Archivos a un Repositorio

```bash
git add archivo.txt
git add *.txt # Añade todos los archivos .txt
git add . # Añade todos los archivos (no recomendado)
```

```bash
git status # Muestra el estado del directorio de trabajo
git status -s
```

## Realizar un COMMIT

```bash
git commit -m "Propósito del commit"
git commit # Abre el editor para ingresar un mensaje de commit
```

## Uso Habitual

```bash
git add [archivo] # Añade un archivo al área de preparación
git diff [archivo] # Muestra los cambios entre el directorio de trabajo y el área de preparación
git diff --staged [archivo] # Muestra los cambios entre el área de preparación y el repositorio
git checkout -- [archivo] # Descarta los cambios en el directorio de trabajo (operación irreversible)
git reset [archivo] # Revierte el repositorio a un estado previamente conocido
git commit # Crea un nuevo commit con los cambios añadidos al área de preparación
git rm [archivo] # Elimina un archivo del directorio de trabajo y del área de preparación
git stash # Guarda los cambios actuales en un almacén temporal para usarlos más tarde
git stash pop # Aplica los cambios almacenados en el directorio de trabajo y los elimina del almacén
git stash drop # Elimina un almacén específico
git restore --staged archivo.txt # Quita un archivo del área de preparación
git restore archivo.txt # Recupera un archivo del repositorio
```

## Ramificación en Git

```bash
git branch [-a] # Lista todas las ramas locales del repositorio
git branch [nombre_rama] # Crea una nueva rama, referenciando la rama actual
git checkout [-b] [nombre_rama] # Cambia al directorio de trabajo a la rama especificada
git merge [nombre_rama] # Fusiona la rama especificada con la rama actual
git branch -d [nombre_rama] # Elimina la rama seleccionada, si ya ha sido fusionada
```

## Actualizar los cambios de la rama principal (upstream) al fork (main)

```bash
git upstream main
```

## Revisar tu Trabajo

```bash
git log [-n cantidad] # Muestra el historial de commits de la rama actual
git log --oneline --graph --decorate # Ofrece una visión general del historial con etiquetas de referencia y gráfico de historia
git log ref.. # Lista los commits que están presentes en la rama actual pero no fusionados en la referencia
git log ..ref # Lista los commits que están presentes en la referencia pero no fusionados en la rama actual
git reflog # Lista las operaciones realizadas en el repositorio local
```

## Revertir Cambios

```bash
git reset [--hard] [referencia_objetivo] # Cambia la rama actual a la referencia objetivo, dejando una diferencia como un cambio no confirmado
git revert [hash_commit] # Crea un nuevo commit revirtiendo los cambios del commit especificado
```

## Sincronizar Repositorios

```bash
git remote add origin [URL_repositorio_remoto]
git fetch [remoto] # Descarga los cambios del remoto, pero no actualiza las ramas de seguimiento
git fetch --prune [remoto] # Elimina las referencias remotas que fueron eliminadas del repositorio remoto
git pull [remoto] # Descarga los cambios del remoto y fusiona la rama actual con su rama ascendente
git push [--tags] [remoto] # Envía los cambios locales al remoto. Usa --tags para enviar las etiquetas
git push -u [remoto] [rama] # Envía una rama local al repositorio remoto y establece su copia como ascendente
git push -u origin main
```

En el archivo `.gitignore`, se pueden añadir los archivos o rutas que no deseas que sean incluidos en el repositorio.

```
# Ejemplo de .gitignore para varios lenguajes
# Enlace: https://github.com/github/gitignore
```

[ejemplos para varios lenguajes](https://github.com/github/gitignore)
[Aprende git con ejemplos interactivos](https://antonz.org/git-by-example/)

## Listado de comandos a tener en cuenta

1. Core:

```bash
git init  # Inicializa un nuevo repositorio Git en el directorio actual.
git clone  # Clona un repositorio Git existente en un nuevo directorio.
git add  # Añade cambios al área de preparación (staging area) para ser incluidos en el próximo commit.
git commit  # Guarda los cambios realizados en el repositorio. Se le puede añadir un mensaje descriptivo.
git status  # Muestra el estado actual del repositorio, incluyendo archivos modificados, añadidos o eliminados.
git diff  # Muestra las diferencias entre los cambios realizados y los archivos en el área de preparación (staging area).
git checkout  # Permite cambiar entre ramas o deshacer cambios en archivos específicos.
git reset  # Permite deshacer cambios en el repositorio. Puede utilizarse para deshacer commits, mover archivos del área de preparación al directorio de trabajo, entre otros usos.
git log  # Muestra un registro de los commits realizados en el repositorio, incluyendo autor, fecha y mensaje del commit.
git show  # Muestra información detallada sobre un commit específico, incluyendo los cambios realizados en ese commit.
git tag  # Permite crear, listar o eliminar etiquetas (tags) que señalan puntos específicos en la historia del repositorio, como versiones.
git push  # Sube los commits locales a un repositorio remoto.
git pull  # Descarga los cambios desde un repositorio remoto y los integra con el repositorio local.
```

2. Branching:

```bash
git branch  # Lista todas las ramas en el repositorio. También se puede utilizar para crear, renombrar o eliminar ramas.
git checkout -b <nombre_rama>  # Crea una nueva rama y se cambia a ella en un solo paso.
git merge <nombre_rama>  # Fusiona los cambios de una rama específica en la rama actual.
git rebase <nombre_rama>  # Reorganiza la historia del commit, moviendo los cambios de la rama actual al final de la rama especificada.
git branch --set-upstream-to=<nombre_rama_remota>  # Establece una conexión entre una rama local y una rama remota, permitiendo así que el comando git pull funcione sin especificar la rama remota.
git branch --unset-upstream  # Elimina la conexión entre la rama local y la rama remota.
git cherry-pick <commit>  # Aplica los cambios de un commit específico en la rama actual, sin fusionar la historia completa de la rama del commit.
```

3. Merging:

```bash
git merge <nombre_rama>  # Fusiona los cambios de una rama específica en la rama actual. Crea un nuevo commit de fusión que integra los cambios de ambas ramas.
git rebase <nombre_rama>  # Reorganiza la historia del commit, moviendo los cambios de la rama actual al final de la rama especificada. A diferencia de merge, no crea un commit de fusión adicional, sino que reescribe la historia del commit.
```

4. Stashing:

```bash
git stash  # Guarda temporalmente los cambios locales que no se han confirmado en un área de almacenamiento temporal (stash).
git stash pop  # Aplica el último stash guardado y lo elimina del stash. Los cambios guardados se aplican al directorio de trabajo.
git stash list  # Muestra una lista de todos los stashes guardados en el repositorio.
git stash apply  # Aplica el último stash guardado, pero no lo elimina del stash. Los cambios guardados se aplican al directorio de trabajo.
git stash drop  # Elimina el último stash guardado de la lista de stashes. Los cambios guardados se pierden definitivamente.
```

5. Remotes:

```bash
git remote  # Muestra una lista de los repositorios remotos configurados actualmente.
git remote add <nombre_remoto> <url_remoto>  # Añade un nuevo repositorio remoto con el nombre especificado y la URL proporcionada.
git remote remove <nombre_remoto>  # Elimina un repositorio remoto del listado de repositorios remotos configurados.
git fetch <nombre_remoto>  # Descarga todos los cambios del repositorio remoto especificado, pero no los integra en el repositorio local.
git pull <nombre_remoto> <rama_remota>  # Descarga los cambios desde el repositorio remoto especificado y los integra en la rama local actual.
git push <nombre_remoto> <rama_local>:<rama_remota>  # Sube los cambios de la rama local especificada al repositorio remoto y la rama remota especificada.
git clone --mirror <url_repositorio>  # Clona un repositorio remoto, incluyendo todas las referencias remotas y las referencias locales, creando un espejo exacto del repositorio original.
```

6. Configuration:

```bash
git config  # Muestra la configuración de Git. Puede ser utilizado para ver, establecer y modificar la configuración a nivel local.
git config --global  # Permite establecer opciones de configuración a nivel global, que se aplicarán a todos los repositorios de Git en tu sistema.
git config --unset <clave>  # Elimina la configuración de Git asociada con una clave específica, tanto a nivel local como global.
```

7. Plumbing:

```bash
git cat-file  # Proporciona contenido y tipo de objeto de un objeto Git en la base de datos.
git checkout-index  # Copia los archivos de Git al área de trabajo.
git commit-tree  # Crea un nuevo commit objeto a partir de un árbol y una lista de padres.
git diff-tree  # Compara el contenido y la estructura de los árboles de árbol entre dos árboles de árbol.
git for-each-ref  # Proporciona una forma de iterar sobre referencias.
git hash-object  # Calcula el hash SHA-1 de un archivo.
git ls-files  # Muestra información sobre archivos en el índice y el directorio de trabajo.
git ls-remote  # Muestra referencias de un repositorio remoto.
git merge-tree  # Muestra el resultado de tres vías de fusión de dos árboles de árbol.
git read-tree  # Lee árboles recursivamente y los convierte en contenido en el área de preparación.
git rev-parse  # Transforma un nombre de referencia en un identificador de objeto.
git show-branch  # Muestra las ramas y sus commits junto con los mensajes de confirmación.
git show-ref  # Muestra referencias (etiquetas, ramas, etc.) junto con los identificadores de objeto.
git symbolic-ref  # Lee y modifica referencias simbólicas.
git tag --list  # Lista etiquetas con coincidencias de patrones opcionales.
git update-ref  # Actualiza el valor de una referencia a un nuevo valor SHA-1.
```

8. Porcelain:

```bash
git blame <archivo>  # Muestra quién modificó por última vez cada línea de un archivo y quién lo hizo.
git bisect  # Ayuda a encontrar el commit que introdujo un problema, utilizando una búsqueda binaria.
git checkout <rama/archivo>  # Cambia a una rama específica o restaura archivos a un estado anterior.
git commit  # Guarda los cambios en el repositorio, creando un nuevo commit.
git diff  # Muestra las diferencias entre los cambios realizados y los archivos en el área de preparación o el repositorio.
git fetch  # Descarga objetos y referencias desde otro repositorio.
git grep <patrón>  # Busca en los archivos del árbol de trabajo cualquier ocurrencia de un patrón.
git log  # Muestra un registro de los commits realizados en el repositorio.
git merge <rama>  # Fusiona cambios de una rama a otra.
git push  # Sube los commits locales a un repositorio remoto.
git rebase <rama>  # Reorganiza la historia del commit, aplicando cambios de una rama a otra.
git reset <archivo>  # Quita archivos del área de preparación y restaura archivos a un estado anterior.
git show <commit>  # Muestra información sobre un commit específico.
git tag <nombre>  # Crea, lista o borra etiquetas (tags) para marcar puntos específicos en la historia del repositorio.
```

9. Alias:

```bash
git config --global alias.<alias> <command>  # Crea un alias global para un comando de Git. Esto permite crear abreviaciones personalizadas para comandos Git frecuentemente utilizados, lo que facilita su uso.
```

10. Hook:

```bash
git config --local core.hooksPath <path>  # Establece la ruta local del directorio donde se encuentran los ganchos (hooks) de Git. Los ganchos son scripts que se ejecutan automáticamente en ciertos eventos de Git, como pre-commit, post-commit, pre-push, etc. Esta opción permite personalizar la ubicación de estos ganchos para un repositorio específico.
```

11. Experimental:

```bash
git annex  # Permite gestionar archivos grandes y binarios de manera eficiente, manteniendo el control de versiones con Git.
git am  # Aplica los cambios en forma de parche generados por git format-patch.
git cherry-pick --upstream  # Extrae un cambio específico de otra rama remota y lo aplica en la rama actual.
git describe  # Proporciona una descripción legible del estado actual del repositorio en relación con los tags más cercanos.
git format-patch  # Genera parches de cambios entre commits específicos.
git fsck  # Verifica la integridad del sistema de archivos del repositorio Git.
git gc  # Recolecta basura en el repositorio Git, comprimiendo y optimizando los objetos no referenciados.
git help  # Muestra ayuda sobre un comando específico de Git.
git log --merges  # Muestra solo los commits que son fusiones.
git log --oneline  # Muestra cada commit en una línea, con el resumen del mensaje.
git log --pretty=  # Controla el formato de salida del registro de commits.
git log --short-commit  # Muestra solo los primeros caracteres del hash SHA-1 de cada commit.
git log --stat  # Muestra estadísticas resumidas de los cambios en cada commit.
git log --topo-order  # Muestra los commits en orden topológico, sin tener en cuenta la fecha del commit.
git merge-ours  # Realiza una fusión y resuelve automáticamente cualquier conflicto utilizando los cambios de la rama actual.
git merge-recursive  # Realiza una fusión recursiva de varios árboles de cambios.
git merge-subtree  # Realiza una fusión de un subárbol en la rama actual.
git mergetool  # Inicia una herramienta de resolución de conflictos para fusiones.
git mktag  # Crea un tag a partir de un objeto existente en la base de datos.
git mv  # Mueve o renombra archivos y registra el cambio en el área de preparación.
git patch-id  # Calcula el identificador único para un parche.
git p4  # Permite interactuar con un servidor Perforce.
git prune  # Elimina objetos inaccesibles de la base de datos de Git.
git pull --rebase  # Descarga los cambios desde el repositorio remoto y los aplica mediante un rebase en lugar de un merge.
git push --mirror  # Sube todos los refs al repositorio remoto, sobrescribiendo cualquier ref existente.
git push --tags  # Sube todos los tags al repositorio remoto.
git reflog  # Muestra un registro de cambios en las referencias del repositorio, útil para recuperar commits perdidos.
git replace  # Permite reemplazar objetos Git (como commits) por otros.
git reset --hard  # Restablece el HEAD y el árbol de trabajo al estado de un commit específico, descartando todos los cambios no confirmados.
git reset --mixed  # Restablece el HEAD al estado de un commit específico, pero conserva los cambios en el área de preparación.
git revert  # Crea un nuevo commit que deshace los cambios de un commit existente.
git rm  # Elimina archivos del árbol de trabajo y del índice de Git.
git show-branch  # Muestra un gráfico de la relación entre ramas.
git show-ref  # Muestra referencias junto con sus hash SHA-1.
git show-ref --heads  # Muestra solo las referencias de las ramas.
git show-ref --tags  # Muestra solo las referencias de los tags.
git stash save  # Guarda temporalmente cambios no terminados para su uso posterior.
git subtree  # Permite trabajar con subproyectos dentro de un repositorio como si fueran repositorios independientes.
git tag --delete  # Elimina tags existentes.
git tag --force  # Sobrescribe un tag existente.
git tag --sign  # Crea tags firmados digitalmente.
git tag -f  # Sinónimo de git tag --force.
git tag -l  # Lista todos los tags.
git tag --verify  # Verifica la firma GPG de un tag.
git unpack-file  # Extrae un archivo Git en su forma original.
git update-index  # Actualiza el índice utilizando el contenido del árbol actual.
git verify-pack  # Verifica la consistencia y la información de un archivo de pack.
git worktree  # Permite trabajar con múltiples árboles de trabajo independientes asociados con un mismo repositorio.
```
