```
git remote rm origin
git remote add origin git@bitbucket.org:primate_vault/moncake.git
git init
git add .
git commit -m "initial commit of full repository"
```
Acordarse cambiar los elementos de .git e incluirlo en el script del bitbicket

Ir dentro del webroot a .git e editar el archivo config y editar la var URL (por el usuario)

```
url = git@bitbucket.org:primatehiberica/project.git
```

```
git clone https://usuario@bitbucket.org/grupo/proyecto.git
chmod +x ./git.run
```
Mirar el ignore

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