# Crear proyecto de Node.js

Para iniciar un proyecto de Node.js, sigue estos pasos:

1. **Crear una carpeta:** En tu sistema de archivos, crea una carpeta donde deseas ubicar tu proyecto de Node.js.

2. **Inicializar el proyecto:** Abre un terminal y navega hasta la ruta de la carpeta del proyecto. Luego, ejecuta el siguiente comando:

```bash
npm init
```

Este comando te guiará a través de la creación de un archivo `package.json` que contendrá la información y configuración de tu proyecto.

3. **Instalación de dependencias:** Instala las dependencias necesarias para tu proyecto. Puedes hacerlo ejecutando los siguientes comandos en tu terminal:

```bash
npm install express
npm install body-parser --save
npm install --save-dev nodemon
```

- El comando `npm install express` instala el framework Express en tu proyecto.
- Con `npm install body-parser --save` instalas el paquete `body-parser`, que se utiliza para analizar la entrada de datos directamente.
- `npm install --save-dev nodemon` instala `nodemon` como una dependencia de desarrollo. Nodemon reiniciará automáticamente el servidor cuando detecte cambios en los archivos.

4. **Inicio del servidor:** Crea un archivo `index.js` en tu proyecto y añade el siguiente código para configurar y arrancar el servidor Express:

```javascript
const express = require('express');

// Crear una aplicación Express
const app = express();

// Configurar el puerto de escucha
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Servidor en funcionamiento en el puerto ${PORT}`);
});
```

5. **Configuración del script de inicio en `package.json`:** En el archivo `package.json`, añade una línea en la sección de scripts para iniciar el servidor utilizando `nodemon`:

```json
"scripts": {
  "start": "nodemon ./index.js"
}
```

6. **Ejecutar el servidor:** Para iniciar el servidor, ejecuta el siguiente comando en tu terminal:

```bash
npm run start
```

Con estos pasos, has creado y configurado un proyecto básico de Node.js con Express, instalado las dependencias necesarias y configurado un script para iniciar el servidor de forma automática. Ahora puedes comenzar a desarrollar tu aplicación Node.js.