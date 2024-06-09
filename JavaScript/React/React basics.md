# [React](https://es.react.dev/)

React es una biblioteca de JavaScript utilizada para construir interfaces de usuario interactivas y dinámicas. Fue desarrollada por Facebook y lanzada como software de código abierto en 2013. React permite a los desarrolladores crear componentes reutilizables que representan diferentes partes de la interfaz de usuario de una aplicación web. Utiliza un enfoque basado en componentes, lo que significa que las aplicaciones se construyen mediante la composición de estos componentes individuales.

Una de las características principales de React es su capacidad para renderizar de manera eficiente los cambios en la interfaz de usuario. Utiliza un modelo de programación declarativa, donde los desarrolladores definen cómo debería ser la interfaz de usuario en función del estado de la aplicación, y React se encarga de actualizar automáticamente la interfaz de usuario cuando ese estado cambia.

Por otro lado hay que contar con la universalidad de React, ya que es una aplicación que se puede ejecutar tanto en el cliente como en el servidor.

Además, React se integra bien con otras bibliotecas y frameworks de JavaScript, lo que permite a los desarrolladores utilizarlo junto con herramientas como Redux para manejar el estado de la aplicación de manera más avanzada, o con herramientas de enrutamiento como React Router para gestionar la navegación en la aplicación.

## Cómo crear un proyecto en React

Después de instalar Node.js desde [https://nodejs.org/es](https://nodejs.org/es), sigue estos pasos para crear un proyecto en React:

1. **Crear el proyecto:** Ejecuta los siguientes comandos en tu terminal:

```bash
npx create-react-app my-app
cd my-app
npm start
```

También podemos usar el empaquetador [Vite](https://vitejs.dev/guide/)

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

## Recursos

- [Preguntas típicas de React - React Wiki](https://www.reactjs.wiki/)
- [Curso de Midudev de React](https://www.youtube.com/watch?v=7iobxzd_2wY&list=PLUofhDIg_38q4D0xNWp7FEHOTcZhjWJ29&index=1)