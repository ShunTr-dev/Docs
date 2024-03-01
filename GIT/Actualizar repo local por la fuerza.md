Realizar con cuidado, esto se carga la versión local del repo:

(Tener en cuenta Imágenes o archivos especiales de los locales)

```
git fetch origin
git reset --hard origin/master
chown -R www-data:www-data ./
```
git - la guía sencilla

Actualizar en vexeta moncake

```
moncakedev
git status
git add app/plugins/centralreservas/models/paciente_resultado_adjunto.php
git commit -m "Seaslab: multiples adjuntos" app/plugins/centralreservas/models/paciente_resultado_adjunto.php
git push
moncake
git pull
```