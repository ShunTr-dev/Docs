```markdown
# Guía Básica de Git

## Herramientas Gráficas para Utilizar Git

- Sourcetree
- GitKraken
- GitHub Desktop

Para comenzar, es necesario instalar Git desde [git-scm.com/downloads](https://git-scm.com/downloads). Si estás utilizando Windows, es imprescindible instalar Git BASH en lugar de utilizar la terminal de Windows.

## Configuración Inicial

```bash
git --version
git config --global user.name "Pablo Martínez"
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