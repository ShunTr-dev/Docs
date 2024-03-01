- Crear una carpeta
- Desde un terminal a la ruta de la carpeta del proyecto poner
```
npm init

```
Esto sirve para crear las dependencias del proyecto.

Instalación de dependencias:

```
npm install express


npm i express


npm install --save express
npm install --save body-parser
//Para hacer los parseos de la entrada de datos directamente
//Estuvo en varias versiones de express y lo quitaron y lo volvieron a poner, y a quitar...

npm install --save--dev nodemon

```
El --save hace que guarde las instalaciones en el package.json con la info del proyecto. Con --save--dev se instala una dependencia para producción, por ejemplo nodemon detectará los cambios en los archivos y reiniciará el servidor cuando lo vea necesario.

Para hacer una instalación completa de las dependencias en el package.json se ejecuta

```
nmp install

```
Para el inicio del servidor crea un archivo index.js e importa las librerías

```
const express = require('express');


//crear una app de expres
const app = express();
//Le decimos el puerto de escucha
app.listen(3000);

```
En el package.json puedes poner una línea para que ejecute algo al inicio en el apartado de scripts. (Admite varios tipos)

```
"start" : "nodemon ./index.js"

```
Para poder ejecutar este script deberíamos escribir en el shell

```
npm run start
```