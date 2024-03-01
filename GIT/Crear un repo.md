```
git init
git add .
git add .gitignore
git remote add origin git@bitbucket.org:primate_vault/moncake.git
git commit -m "First commit"
git push -u origin master
```
Se añaden los remotos:

```
git remote set-url origin https://ShunTr@bitbucket.org/primatehiberica/proyecto.git
```
Si nos da el error de: fatal: remote origin already exists.

Ejecutamos esto para cambiar el origen

```
git remote set-url origin https://ShunTr@bitbucket.org/primatehiberica/beeclock.git
```