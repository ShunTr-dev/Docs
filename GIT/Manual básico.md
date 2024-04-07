```markdown
# Guía Básica de Git

Git es un sistema de control de versiones distribuido ampliamente utilizado para el seguimiento de cambios en archivos de código fuente durante el desarrollo de software. Permite a los desarrolladores trabajar en colaboración, mantener un historial de cambios, crear ramas para el desarrollo paralelo y fusionar cambios de manera eficiente. Git es conocido por su velocidad, flexibilidad y robustez, y es fundamental en el desarrollo de software moderno.

## Herramientas Gráficas para Utilizar Git

- Sourcetree
- GitKraken
- GitHub Desktop

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










Buscar el archivo contributing.md





1. Core:
•  git init
•  git clone
•  git add
•  git commit
•  git status
•  git diff
•  git checkout
•  git reset
•  git log
•  git show
•  git tag
•  git push
•  git pull

2.Branching:
•  git branch
•  git checkout -b
•  git merge
•  git rebase
•  git branch --set-upstream-to
•  git branch --unset-upstream
•  git cherry-pick

3.Merging:
•  git merge
•  git rebase

4.Stashing:
•  git stash
•  git stash pop
•  git stash list
•  git stash apply
•  git stash drop

5.Remotes:
•  git remote
•  git remote add
•  git remote remove
•  git fetch
•  git pull
•  git push
•  git clone --mirror

6.Configuration:
•  git config
•  git global config
•  git reset config

7. Plumbing:
•  git cat-file
•  git checkout-index
•  git commit-tree
•  git diff-tree
•  git for-each-ref
•  git hash-object
•  git ls-files
•  git ls-remote
•  git merge-tree
•  git read-tree
•  git rev-parse
•  git show-branch
•  git show-ref
•  git symbolic-ref
•  git tag --list
•  git update-ref

8.Porcelain:
•  git blame
•  git bisect
•  git checkout
•  git commit
•  git diff
•  git fetch
•  git grep
•  git log
•  git merge
•  git push
•  git rebase
•  git reset
•  git show
•  git tag

9.Alias:
•  git config --global alias.<alias> <command>

10.Hook:
•  git config --local core.hooksPath <path>

11.Experimental: (May not be fully Supported)
•  git annex
•  git am
•  git cherry-pick --upstream
•  git describe
•  git format-patch
•  git fsck
•  git gc
•  git help
•  git log --merges
•  git log --oneline
•  git log --pretty=
•  git log --short-commit
•  git log --stat
•  git log --topo-order
•  git merge-ours
•  git merge-recursive
•  git merge-subtree
•  git mergetool
•  git mktag
•  git mv
•  git patch-id
•  git p4
•  git prune
•  git pull --rebase
•  git push --mirror
•  git push --tags
•  git reflog
•  git replace
•  git reset --hard
•  git reset --mixed
•  git revert
•  git rm
•  git show-branch
•  git show-ref
•  git show-ref --heads
•  git show-ref --tags
•  git stash save
•  git subtree
•  git tag --delete
•  git tag --force
•  git tag --sign
•  git tag -f
•  git tag -l
•  git tag --verify
•  git unpack-file
•  git update-index
•  git verify-pack
•  git worktree