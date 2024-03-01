Añadimos el la ruta del proyecto

```
git add .
```
Añadimos un motivo del commit

```
git commit -m "First commit"
```
Lanzamos el Push

```
git push -u origin master
```
Si al hacer el push, la cagaste con el commit, esto deshace los cambios en local y en remoto:

```
git revert HEAD
```