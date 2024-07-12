# [React](https://es.react.dev/)

React es una biblioteca de JavaScript utilizada para construir interfaces de usuario interactivas y dinámicas. Fue desarrollada por Facebook y lanzada como software de código abierto en 2013. React permite a los desarrolladores crear componentes reutilizables que representan diferentes partes de la interfaz de usuario de una aplicación web. Utiliza un enfoque basado en componentes, lo que significa que las aplicaciones se construyen mediante la composición de estos componentes individuales.

Una de las características principales de React es su capacidad para renderizar de manera eficiente los cambios en la interfaz de usuario. Utiliza un modelo de programación declarativa, donde los desarrolladores definen cómo debería ser la interfaz de usuario en función del estado de la aplicación, y React se encarga de actualizar automáticamente la interfaz de usuario cuando ese estado cambia.

Por otro lado hay que contar con la universalidad de React, ya que es una aplicación que se puede ejecutar tanto en el cliente como en el servidor.

Además, React se integra bien con otras bibliotecas y frameworks de JavaScript, lo que permite a los desarrolladores utilizarlo junto con herramientas como Redux para manejar el estado de la aplicación de manera más avanzada, o con herramientas de enrutamiento como React Router para gestionar la navegación en la aplicación.

## Cómo crear un proyecto en React

Realmente para usar React no se tiene por que usar un empaquetador (como WebPack o Vite), se puede usar directamente en un archivo poniendo:
```js
import ReactDOM from "https://esm.sh/react-dom@18.2.0/client"

const appDomElement = document.getElementById('app') // Hacemos la refencia de dónde queremos montar la app

const root = ReactDom.createRoot(appDomElement) // Se monta la raíz de la aplicación
root.render('Hola mundo') // Podemos empezar a renderizar texto
```

```html
<div id="app"></div>
```

Con esto podríamos imprimir texto, para empezar a imprimir HTML haría falta la librería de React:

```js
import React from "https://esm.sh/react@18.2.0/client"
import ReactDOM from "https://esm.sh/react-dom@18.2.0/client"

const appDomElement = document.getElementById('app') 

const root = ReactDom.createRoot(appDomElement)
const button = React.createElement('button', {"data-id": 'button-accept'}, 'Aceptar')

root.render(app)
```

**Crear el proyecto con create React APP** 
1. Descarga e instalación: 
Ejecuta los siguientes comandos en tu terminal:

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

3. **Instalar componentes nuevos:** Si necesitas instalar nuevos componentes en tu proyecto, puedes hacerlo utilizando npm. Por ejemplo, para instalar `styled-components`, ejecuta el siguiente comando en el terminal:

```bash
npm install --save styled-components
```

Esto instalará `styled-components` y lo agregará como una dependencia en tu proyecto.


**Crear el proyecto con [Vite](https://vitejs.dev/guide/)** 

1. **Descarga e instalación**

```bash
npm init -y # Inicializa el projecto y crea un package.json
npm create vite@latest # Nos hace una serie de preguntas para configurar el proyecto
npm install
```

2. **Punto de entrada**

Puedes escoger "React" para que te cree una aplicación con el punto de entrada ya montado.
O puedes escoger "Vanilla" para que vengan los archivos por defecto y configurarlos tú.
Para crear el punto de entrada necesitas:

Instala un plugin para poder hacer el punto de entrada:
```bash
npm install @vite/plugin-react -E
```

Ahora si vamos al package.json, no tenemos React. Hay que añadirlo.
```bash
npm install react react-dom -E
```

Configuración de vite.config.js
```js
import { defineConfig } from "vite" 
import react from "@vite/plugin-react"

export default defineConfig({
    plugins: [react()]
})
```

En el index.html tenemos un script que es el que cargamos al inicio en la página web.
El main.js, que es el punto de entrada de la aplicación.

```js
import { createRoot } from 'react-dom/client'

const root = createRoot(document.getElementById('root'))

root.render(<h1>hola mundo</h1>)
```

Si hacemos un ''npm run dev'' dará un error por que en vite los archivos .js no está preparados para soportar el JSX.
Por lo tanto tenemos que cambiar la extensión a .jsx








3. **INSTALAR EL LINTER**

```bash
npm install standard -D
```
Ir al package.json y añadir el linter a la config

```
"eslintConfig": {
    "extends": "./node_modules/standard/eslintrc.json"
}
```













+ extensión en vs code de ESLint
Se puede configurar un editor automático para cuando guarde


## Conceptos básicos de React



## Recursos

- [Preguntas típicas de React - React Wiki](https://www.reactjs.wiki/)
- [Curso de Midudev de React](https://www.youtube.com/watch?v=7iobxzd_2wY&list=PLUofhDIg_38q4D0xNWp7FEHOTcZhjWJ29&index=1)