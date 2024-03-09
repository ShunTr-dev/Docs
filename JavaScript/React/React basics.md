# Crear un proyecto en React

Después de instalar Node.js desde [https://nodejs.org/es](https://nodejs.org/es), sigue estos pasos para crear un proyecto en React:

1. **Crear el proyecto:** Ejecuta los siguientes comandos en tu terminal:

```bash
npx create-react-app my-app
cd my-app
npm start
```

Esto creará un nuevo proyecto de React llamado `my-app`, cambiará al directorio del proyecto y comenzará el servidor de desarrollo.

2. **Instalar dependencias:** Una vez que el proyecto esté creado, instala las dependencias necesarias ejecutando el siguiente comando en el terminal:

```bash
npm install
```

Esto instalará todas las dependencias listadas en el archivo `package.json`.

3. **Agregar carpetas al VSCode:** Abre Visual Studio Code (VSCode) y añade la carpeta del proyecto. Para hacerlo, ve a `Archivo` > `Abrir carpeta...` y selecciona la carpeta de tu proyecto `my-app`.

4. **Instalar componentes nuevos:** Si necesitas instalar nuevos componentes en tu proyecto, puedes hacerlo utilizando npm. Por ejemplo, para instalar `styled-components`, ejecuta el siguiente comando en el terminal:

```bash
npm install --save styled-components
```

Esto instalará `styled-components` y lo agregará como una dependencia en tu proyecto.