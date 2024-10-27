---
title: React basics
date: 2024-08-20 00:00:00 -100
categories: [React]
tags: [herramientas]
---

# [React](https://es.react.dev/)

React es una biblioteca de JavaScript utilizada para construir interfaces de usuario interactivas y dinámicas. Fue desarrollada por Facebook y lanzada como software de código abierto en 2013. React permite a los desarrolladores crear componentes reutilizables que representan diferentes partes de la interfaz de usuario de una aplicación web. Utiliza un enfoque basado en componentes, lo que significa que las aplicaciones se construyen mediante la composición de estos componentes individuales.

Una de las características principales de React es su capacidad para renderizar de manera eficiente los cambios en la interfaz de usuario. Utiliza un modelo de programación declarativa, donde los desarrolladores definen cómo debería ser la interfaz de usuario en función del estado de la aplicación, y React se encarga de actualizar automáticamente la interfaz de usuario cuando ese estado cambia.

Por otro lado hay que contar con la universalidad de React, ya que es una aplicación que se puede ejecutar tanto en el cliente como en el servidor.

Además, React se integra bien con otras bibliotecas y frameworks de JavaScript, lo que permite a los desarrolladores utilizarlo junto con herramientas como Redux para manejar el estado de la aplicación de manera más avanzada, o con herramientas de enrutamiento como React Router para gestionar la navegación en la aplicación.

## Cómo crear un proyecto en React

Realmente para usar React no se tiene por que usar un empaquetador (como WebPack o Vite), se puede usar directamente en un archivo poniendo:

```js
import ReactDOM from 'https://esm.sh/react-dom@18.2.0/client'

const appDomElement = document.getElementById('app') // Hacemos la refencia de dónde queremos montar la app

const root = ReactDom.createRoot(appDomElement) // Se monta la raíz de la aplicación
root.render('Hola mundo') // Podemos empezar a renderizar texto
```

```html
<div id="app"></div>
```

Con esto podríamos imprimir texto, para empezar a imprimir HTML haría falta la librería de React:

```js
import React from 'https://esm.sh/react@18.2.0/client'
import ReactDOM from 'https://esm.sh/react-dom@18.2.0/client'

const appDomElement = document.getElementById('app')

const root = ReactDom.createRoot(appDomElement)
const button = React.createElement('button', { 'data-id': 'button-accept' }, 'Aceptar')

root.render(app)
```

### **Crear el proyecto con create React APP**

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

### **Crear el proyecto con [Vite](https://vitejs.dev/guide/)**

1. **Descarga e instalación**

```bash
npm init -y # Inicializa el projecto y crea un package.json
npm create vite@latest # Nos hace una serie de preguntas para configurar el proyecto
npm install
```

2. **Punto de entrada**

Puedes escoger `React` para que te cree una aplicación con el punto de entrada ya montado.
O puedes escoger `Vanilla` para que vengan los archivos por defecto y configurarlos tú.
Para crear el punto de entrada necesitas:

Instala un plugin para poder hacer el punto de entrada:

```bash
npm install @vite/plugin-react -E
```

Ahora si vamos al `package.json`, no tenemos React. Hay que añadirlo.

```bash
npm install react react-dom -E
```

Configuración de vite.config.js

```js
import { defineConfig } from 'vite'
import react from '@vite/plugin-react'

export default defineConfig({
    plugins: [react()],
})
```

En el `index.html` tenemos un script que es el que cargamos al inicio en la página web.
El `main.js`, que es el punto de entrada de la aplicación.

```js
import { createRoot } from 'react-dom/client'

const root = createRoot(document.getElementById('root'))

root.render(<h1>hola mundo</h1>)
```

Si hacemos un `npm run dev` dará un error por que en vite los archivos .js no está preparados para soportar el JSX.
Por lo tanto tenemos que cambiar la extensión a .jsx

### **Instalar el linter y el prettier**

```bash
npm i -D eslint #Lo instalamos sólo como dependencia de desarrollo
npx eslint --init #npm init @eslint/config
```

Esto instalará eslint y el segundo comando nos irá preguntando por la configuración del mismo.
Tras esto tendremos un archivo `.eslintrc.js` en la raíz.
Añadimos la versión de react:

```
settings: {
    react: {
        version: 'detect'
    },
},
```

```bash
npx eslint src/main.jsx # Se puede ver el estado del archivo
```

Para poder tener una salida en el editor hay que instalar la extensión de ESLint

```bash
npm i -D prettier
npx prettier src/main.jsx --write # Hace lo mismo que el otro, pero formateando el archivo
```

El problema que tiene esto es que Prettier y ESLint tienen diferentes opiniones de como hacer las cosas.
Donde uno te pedirá hacer comillas simples otro te pedirá comillas dobles.
Entonces, para evitar esto necesitamos crear un documento en el root `.prettierrc`.
En la web de Prettier se pueden ver las confs por defecto.

```js
{
    "printWidth": 120,
    "tabWidth": 4,
    "trailingComma": "es5",
    "singleQuote": true,
    "useTabs": false,
    "semi": true,
    "quoteProps": "as-needed",
    "jsxSingleQuote": false,
    "bracketSpacing": true,
    "bracketSameLine": false,
    "arrowParens": "always",
    "endOfLine": "lf"
}
```

Es necesario instalar la extensión de Prettier para usarlo con VSCode.
En la configuración `pulsando ctrl + ,` se puede poner el `format on save`, para que se formatee al guardar.

Para que estas dos cosas puedan coexistir hay que instalar un paquete.

```bash
npm i -D eslint-config-prettier
```

Tras esto tenemos que ir al archivo de configuración del linter `.eslintrc.js` y en el apartado de `extends` tenemos que añadir `eslint-config-prettier`.
Con esto lo que conseguimos es que para determinar quién gana en un conflicto entre el linter y el prettier, ponemos esto, para que se determine por defecto el ganador prettier.

Añadimos un archivo `.prettierignore` para decir que rutas/archivos no queremos que se formateen.

```js
# Ignore artifacts:
build
coverage

# Ignore all HTML files:
**/*.html

**/.git
**/.svn
**/.hg
**/node_modules
```

Hacemos lo mismo para el linter `.eslintignore`, en este caso no hace falta meterse en todos los archivos ya que ESLint es sólo un linter para `.js` y `.jsx`

```
dist
```

Para automatizar esto, tenemos que añadir dos scripts en el `package.json`.

```js
"format": "prettier --write .",
"lint": "eslint --fix . --ext .js,.jsx,.ts,.tsx",
```

## Conceptos Básicos en React

1. **Components (Componentes)**

-   Son las unidades básicas y reutilizables en React. Forman las partes visibles de nuestra aplicación, como pueden ser botones, inputs o páginas enteras.
    Su parte más interesante es la reutilización. Todos ellos devuelven código al ser ejecutados y pese a que se puede usar sin JSX, lo normal es usarlo gracias a la comodidad que ofrece.
    Pueden ser clases o funciones.

```js
function Welcome(props) {
    return <h1>Hello, {props.name}</h1>
}
```

2. **JSX**

-   Es una extensión de JavaScript que permite escribir HTML dentro de JavaScript.
    Es necesario una notación en concreto y se escribe en [camelCase](https://es.wikipedia.org/wiki/Camel_case)

```js
const element = <h1 className="tittle">Hello, world!</h1>
```

3. **Curly braces (Llaves)**

-   Se usan para incluir expresiones de JavaScript dentro de JSX y así poder tener contenido dinámico.

```js
const name = 'React'
const element = <h1>Hello, {name}!</h1>
```

4. **Fragments**

-   Permiten agrupar una lista de hijos sin añadir nodos extra al DOM.

```js
function FragmentDemo() {
    return (
        <React.Fragment>
            <h1>Title</h1>
            <p>Description</p>
        </React.Fragment>
    )
}

// O también podríamos usar:

function FragmentDemo() {
    return (
        <>
            <h1>Title</h1>
            <p>Description</p>
        </>
    )
}
```

5. **Props**

-   Son los datos que se pasan a los componentes para configurar cómo se deben comportar o qué deben mostrar.
    Se puede pasar como prop cualquier cosa, desde datos, otros componentes, o funciones.

```js
function Greeting(props) {
    return <h1>Hello, {props.name}</h1>
}
```

6. **Children**

-   Prop especial que permite pasar componentes o elementos secundarios a un componente.

```js
function Wrapper({ children }) {
    return <div className="wrapper">{children}</div>
}

function App() {
    return (
        <Wrapper>
            <h1>Title</h1>
            <p>Description</p>
        </Wrapper>
    )
}
```

7. **Keys**

-   Es lo que usa React para identificar un componente de otro, al final la Key es un identificador único para ese componente.
-   Son necesarias para ayudar a React a identificar qué ítems han cambiado, agregado o eliminado en las listas.
-   Si no puedes usar una key siempre puedes usar el index para usarlo como identificador.

```js
const items = ['Apple', 'Banana', 'Cherry']
const listItems = items.map((item, index) => <li key={index}>{item}</li>)
```

8. **Rendering (Renderizado)**
   Lo que usa react para renderizar/dibujar los componentes es el `Virtual DOM` (Document Object Model), que es lo que usan todos los navegadores usan para mostrar los elementos en las páginas web. El proceso de dibujado es tal que así:

-   Si cambia el estado de la aplicación, React actualiza el `VDOM`, que es más rápido que actualizar todo el `DOM`.
-   React usa un proceso en el que encuentra las diferencias entre los diferentes estados en el `VDOM`.
-   React lanza un proceso llamado `reconciliation` por el cual actualiza solo las partes que tuvieron cambios.

Es decir, sólo actualiza la parte que cambió en la página.

```js
ReactDOM.render(<Welcome name="Sara" />, document.getElementById('root'))
```

9. **Event Handling (Manejo de eventos)**

-   React maneja los eventos de una forma muy similar a como se manejan en HTML, pero con sintaxis de JSX.

```js
function Button() {
    function handleClick() {
        alert('Button clicked')
    }

    return <button onClick={handleClick}>Click me</button>
}
```

10. **State**

-   Es una forma de hacer que los componentes respondan a la entrada del usuario y cambien su representación.
-   El estado es como una fotografía de un elemento. No son simplemente variables, si no que son funciones de propio React como `useState()`

```js
import { useState } from 'react'

const [likes, setlikes] = useState(0)

const handleClick = () => {
    setClicks(likes + 1)
}

return <button onClick={handleClisk}>Likes: {likes}</button>
```

11. **Controlled Components (Componentes controlados)**

-   Son componentes donde React controla el estado de los inputs de formularios.

```js
function ControlledInput() {
    const [value, setValue] = useState('')

    return <input value={value} onChange={(e) => setValue(e.target.value)} />
}
```

12. **(Hooks)[https://github.com/ShunTr-dev/Docs/tree/main/JavaScript/React/Hooks.md]**

Permiten usar estado y otras características de React sin escribir una clase. Hay principalmente 5 tipos:

-   Hooks de estado: `useState()`, `useReducer()`. (Para manejar el estado)
-   Hooks de contexto: `useContext()`, para pasar datos a través del contexto.
-   Hooks de referencia: `useRef()`.
-   Hooks de Efectos: `useEffect()`, perfecto para conectar con sistemas externos.
-   Hooks de Rendimiento: `useMemo()`, `useCallback()`. Mejoran el rendimiento evitando el trabajo extra.

Pero los que más se usan son: `useState()`, `useEffect()` y `useRef()`.

13. **Purity (Pureza)**

-   La pureza en React dice que un componente puro, siempre al tener un mismo input deba sacar siempre el mismo output.
-   Los componentes deben ser funciones puras, lo que significa que no deben modificar sus props ni tener efectos secundarios y devolver sólo JSX.

```js
function PureComponent(props) {
    return <div>{props.value}</div>
}
```

14. **Strict Mode (Modo estricto)**

-   Ayuda a identificar componentes con posibles problemas al hacer que ciertos errores sean más obvios a la hora de desarrollar los componentes.
-   Se monta alrededor de el módulo de APP de la aplicación. Entre otras cosas lo que hace, a la hora de montar un componente, es montarlo, destruirlo, y volverlo a montar, para comprobar que todo está correcto.

```js
const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(
    <React.StrictMode>
        <App />
    </React.StrictMode>
)
```

15. **Effects**

-   Con el hook `useEffect()`, puedes realizar efectos secundarios en componentes funcionales.
-   Si quieres hacer peticiones a elementos externos esta es una forma muy buena de hacerlo. Ya que se ejecuta en funcion del cambio de estado de los estados que le pasemos.

```js
import React, { useEffect } from 'react'

function MyComponent() {
    useEffect(() => {
        console.log('Component mounted')
    }, [])

    return <div>Hello</div>
}
```

16. **Refs**

-   Son una forma de acceder directamente a un DOM node o a una instancia de un componente.

```js
<Button ref={ref}>
```

17. **Context**

-   Proporciona una forma de pasar datos a través del árbol de componentes sin tener que pasar props manualmente en cada nivel.

```js
function App() {
    return (
        <>
            <AuthContext.Provider
                value={{
                    isLoggedIn: !!token,
                    token: token,
                    userId: userId,
                    userEmail: userEmail,
                    isAdmin: isAdmin,
                    login: login,
                    logout: logout,
                }}>
                <RouterProvider router={router} />
            </AuthContext.Provider>
        </>
    )
}

const ProductSingle = (props) => {
    const productId = useParams().productId
    const auth = useContext(AuthContext)

    return (
        <>
            <ProductDetail id={productId} />
            {auth.isLoggedIn && auth.isAdmin && (
                <>
                    <ProductSellsStatisticsChart id={productId} />
                    <ProductViewsStatisticsChart id={productId} />
                </>
            )}

            <RelatedProducts id={productId} />
        </>
    )
}
```

18. **Portals**

-   Permiten renderizar componentes fuera de su jerarquía padre, pero manteniendo su contexto. Son perfectos para modales, dropdowns y tooltips.

19. **Suspense**

-   Permite mostrar un fallback mientras se espera a que algo se cargue, como componentes dinámicos o datos asíncronos.

```js
const OtherComponent = React.lazy(() => import('./OtherComponent'))

function MyComponent() {
    return (
        <React.Suspense fallback={<div>Loading...</div>}>
            <OtherComponent />
        </React.Suspense>
    )
}
```

20. **Error Boundaries (Límites de error)**

-   Son componentes que capturan errores en el árbol de componentes hijo y muestran una interfaz de error en lugar de que la aplicación se bloquee.
-   Se refiere a la separación de responsabilidades entre componentes, donde cada componente tiene una responsabilidad clara y no debe hacer demasiado.

```js
import { ErrorBoundary } from 'react-error-boundary'

function Fallback({ error }) {
    return (
        <div role="alert">
            <p>No user provided: </p>
            <pre>{error.message}</pre>
        </div>
    )
}

;<ErrorBoundary FallbackComponent={Fallback}>
    <App />
</ErrorBoundary>
```

21. **Code Splitting**

-   Dividir el código en varios archivos para cargar solo lo necesario.

```jsx
import { Suspense, lazy } from 'react'

const OtherComponent = lazy(() => import('./OtherComponent'))

function MyComponent() {
    return (
        <Suspense fallback={<div>Loading...</div>}>
            <OtherComponent />
        </Suspense>
    )
}
```

## Recursos

-   [Preguntas típicas de React - React Wiki](https://www.reactjs.wiki/)
-   [Every React Concept Explained in 12 Minutes](https://www.youtube.com/watch?v=wIyHSOugGGw)
-   [Curso de Midudev de React](https://www.youtube.com/watch?v=7iobxzd_2wY&list=PLUofhDIg_38q4D0xNWp7FEHOTcZhjWJ29&index=1)
