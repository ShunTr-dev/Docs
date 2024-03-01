Herramientas para poder utilizar GIT de manera GRÁFICA
- Sourcetree
- GitKraken
- GitHub Desktop

Para poder usarlo debemos instalarlo desde git-scm.com/downloads
En caso de hacerlo desde windows es necesario instalar el Git BASH -TOTALMENTE NECESARIO, NO USES LA TERMINAL DE WINDOWS-

Configuración Inicial
```
git --version
git config --global user.name "Pablo Martínez"
git config --global user.email repaco9@gmail.com
git config --global color.ui auto //Enable some colorization of Git output
git config --global core.editor "code --wait" //para usar el vscode como editor
git config --global -e //para ver el archivo de configuración
```

Configuración de core.autocrlf
(Por probar) Windows usa para los saltos de línea CR y LF y Linux/Mac usa LF, por lo tanto los usuarios de WINDOWS deben tener la config a TRUE y los usuarios de Linux/MAC lo deben tener a con el valor de INPUT
```
git config --global core.autocrlf true
```

Para ver las cosas que se pueden configurar en el global
```
git config -h
```

Comandos
```
ls //Listado de archivos y carpetas
pwd //Ruta en la que se encuentra la terminal
cd <ruta> //Moverse entre carpetas
mkdir //crear una carpeta
```

Iniciar un Repositorio
```
(En la ruta del repo)
git init [project name]
git clone [project url] //Downloads a project with the entire history from the remote repository.
```

Añadir un archivo a un repo
```
git add archivo.txt
git add .txt //añade todos los archivos txt
git add . //Añade todos los archivos (No recomendado)
```

```
git status //Displays the status of your working directory. Options include new, staged, and modified files. It will retrieve branch name, current commit identifier, and changes pending commit.
git status -s
```

Para hacer el COMMIT
```
git commit -m "Propósito del commit"
git commit //abre el editor para configurar el commit
```

Uso habitual
```
git add [file] //Add a file to the staging area. Use in place of the full file path to add all changed files from the current directory down into the directory tree.
git diff [file] //Show changes between working directory and staging area.
git diff --staged [file] //Shows any changes between the staging area and the repository.
git checkout -- [file] //Discard changes in working directory. This operation is unrecoverable.
git reset [file] //Revert your repository to a previous known working state.
git commit //Create a new commit from changes added to the staging area. The commit must have a message!
git rm [file] //Remove file from working directory and staging area.
git stash //Put current changes in your working directory into stash for later use.
git stash pop //Apply stored stash content into working directory, and clear stash.
git stash drop //Delete a specific stash from all your previous stashes.

git restore --staged archivo.txt //Para quitar un archivo del estado staged
git restore archivo.txt //Para recuperar un archivo del repo
```

Git branching
```
git branch [-a] //List all local branches in repository. With -a: show all branches (with remote).
git branch [branch_name] //Create new branch, referencing the current HEAD.
git checkout [-b][branch_name] //Switch working directory to the specified branch. With -b: Git will create the specified branch if it does not exist.
git merge [from name] //Join specified [from name] branch into your current branch (the one you are on currently).
git branch -d [name] //Remove selected branch, if it is already merged into any other. -D instead of -d forces deletion.
```

Review your work
```
git log [-n count] //List commit history of current branch. -n count limits list to last n commits.
git log --oneline --graph --decorate //An overview with reference labels and history graph. One commit per line.
git log ref.. //List commits that are present on the current branch and not merged into ref. A ref can be a branch name or a tag name.
git log ..ref //List commit that are present on ref and not merged into current branch.
git reflog //List operations (e.g. checkouts or commits) made on local repository
git log --oneline
```

Reverting changes
```
git reset [--hard] [target reference] //Switches the current branch to the target reference, leaving a difference as an uncommitted change. When --hard is used, all changes are discarded.
git revert [commit sha] //Create a new commit, reverting changes from the specified commit. It generates an inversion of changes.
```

Synchronizing repositories
```
*
git remote add origin https://github.com akgufdkaufgdks
*
git fetch [remote] //Fetch changes from the remote, but not update tracking branches.
git fetch --prune [remote] //Delete remote Refs that were removed from the remote repository.
git pull [remote] //Fetch changes from the remote and merge current branch with its upstream.
git push [--tags] [remote] //Push local changes to the remote. Use --tags to push tags.
git push -u [remote] [branch] //Push local branch to remote repository. Set its copy as an upstream.
git push -u origin main
```

En el archivo .gitignore añadimos los archivos o rutas que no queremos que acaben en el repo (ejemplos para varios lenguajes https://github.com/github/gitignore )
```
# CakePHP 3

/vendor/*
/config/app.php

/tmp/cache/models/*
!/tmp/cache/models/empty
/tmp/cache/persistent/*
!/tmp/cache/persistent/empty
/tmp/cache/views/*
!/tmp/cache/views/empty
/tmp/sessions/*
!/tmp/sessions/empty
/tmp/tests/*
!/tmp/tests/empty

/logs/*
!/logs/empty

# CakePHP 2

/app/tmp/*
/app/Config/core.php
/app/Config/database.php
/vendors/*
```