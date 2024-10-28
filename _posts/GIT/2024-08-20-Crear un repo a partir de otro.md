---
title: Crear un repo a partir de otro
date: 2024-08-20 00:00:00 -100
categories: [GIT]
tags: [git, repo, copy]
---

# Crear un repositorio a partir de otro

En esta guía se detallan los pasos necesarios para crear un nuevo repositorio a partir de otro existente.

## Clonar el repositorio original

El primer paso es clonar el repositorio original al que queremos realizar cambios. Utilizamos el siguiente comando:

```bash
git clone https://usuario@bitbucket.org/grupo/proyecto.git
```

## Configurar el nuevo repositorio

Una vez clonado el repositorio original, debemos configurar el nuevo repositorio. Esto incluye cambiar la URL remota del repositorio y asegurarnos de que los archivos de configuración están correctamente ajustados. Utilizamos los siguientes comandos:

```bash
git remote rm origin
git remote add origin git@bitbucket.org:vault/proyecto.git
```

## Inicializar el nuevo repositorio

Después de configurar la URL remota del nuevo repositorio, inicializamos un nuevo repositorio local en el directorio clonado. Utilizamos el siguiente comando:

```bash
git init
```

## Añadir archivos y realizar el primer commit

Una vez inicializado el repositorio, añadimos todos los archivos al área de preparación y realizamos el primer commit con un mensaje descriptivo. Utilizamos los siguientes comandos:

```bash
git add .
git commit -m "initial commit of full repository"
```

## Modificar el archivo de configuración del nuevo repositorio

Para asegurarnos de que la URL remota del nuevo repositorio está correctamente configurada, debemos modificar el archivo de configuración `.git/config` dentro del directorio del repositorio clonado. Buscamos la variable `url` y la editamos con la nueva URL remota del repositorio. Por ejemplo:

```bash
url = git@bitbucket.org:primatehiberica/project.git
```

## Añadir permisos de ejecución a un script

Si hay algún script que necesite permisos de ejecución, podemos añadirlos utilizando el siguiente comando:

```bash
chmod +x ./git.run
```

## Revisar el archivo .gitignore

Es importante revisar y ajustar el archivo `.gitignore` para asegurarnos de que se están ignorando correctamente los archivos y directorios que no deben incluirse en el repositorio. A continuación se muestra un ejemplo de un archivo `.gitignore` común para proyectos CakePHP:

```
# CakePHP specific files #
##########################
/config/app.php
/config/.env
/logs/*
/tmp/*
/vendor/*
*.log
myapp_cake_model_debug_kit_
myapp_cake_model_default_
myapp_cake_core_translations_
/logs/*.log
/tmp/*
/webroot/files/useruploads/*


# OS generated files #
######################
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
Icon?
ehthumbs.db
Thumbs.db


# Tool specific files #
#######################
# vim
*~
*.swp
*.swo
# sublime text & textmate
*.sublime-*
*.stTheme.cache
*.tmlanguage.cache
*.tmPreferences.cache
# Eclipse
.settings/*
# JetBrains, aka PHPStorm, IntelliJ IDEA
.idea/*
# NetBeans
nbproject/*
# Visual Studio Code
.vscode
# Sass preprocessor
.sass-cache/
```

En esta guía se han detallado los pasos necesarios para crear un nuevo repositorio a partir de otro existente, incluyendo clonar el repositorio original, configurar el nuevo repositorio, inicializarlo, añadir archivos y realizar el primer commit, modificar la configuración remota, añadir permisos de ejecución a un script y revisar el archivo .gitignore.
