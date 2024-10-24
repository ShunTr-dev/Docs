### 1. ¿Qué es **Express.js**?

**Express.js** es un framework de Node.js que facilita la creación de aplicaciones web y APIs al proporcionar una serie de herramientas y utilidades que hacen el proceso más simple. Es minimalista y flexible, permitiéndote manejar rutas, middleware, y gestionar peticiones HTTP con facilidad. Es uno de los frameworks más populares para construir aplicaciones del lado del servidor en Node.js.

---

### 2. **Instalando Express.js**

Para empezar a usar Express.js, primero necesitas tener Node.js instalado. Luego, puedes instalar Express.js en tu proyecto mediante npm.

1. Crea un directorio para tu proyecto y navega a él:

```bash
mkdir mi-proyecto
cd mi-proyecto
```

2. Inicializa un proyecto de Node.js:

```bash
npm init -y
```

3. Instala **Express** como dependencia:

```bash
npm install express
```

4. El código inicial para levantar servidor es muy parecido al normal, simplemente con la función de `express()`

```js
const http = require('http')

const express = require('express')

const app = express()
const server = http.createServer(app)

server.listen(3000)
```

---

### 3. **Middleware**

En `Express.js`, los _middlewares_ son funciones que tienen acceso al objeto de solicitud (`req`), el objeto de respuesta (`res`), y la función `next()`, que se invoca para pasar el control al siguiente middleware. Los middlewares son útiles para manipular las peticiones antes de que lleguen a las rutas.

```js
const express = require('express')
const app = express()

// Middleware personalizado para registrar cada solicitud
app.use((req, res, next) => {
    console.log('Primer middleware')
    next() // Pasa el control al siguiente middleware o ruta si no se llama para la ejecución
})

app.use((req, res, next) => {
    //Si no se pone next() en la función anterior esto no se ejecuta
    console.log('Segundo middleware')
    res.send('<h1>Hola mundo</h1>') // Nos permite enviar una respuesta e incluye los headers automáticamente
    //Con esto no necesitamos volver a poner next() ya que envía una respuesta.
})

const server = http.createServer(app)
server.listen(3000)
```

---

### 4. **Manejo de Routes**

Las rutas en Express.js son puntos de entrada a través de los cuales los clientes pueden interactuar con tu aplicación. Cada ruta está asociada con un método HTTP (GET, POST, PUT, DELETE, etc.) y una URL.

Los accesos a la URL se hacen de arriba abajo según se leen. Por lo tanto si tenemos declaradas las rutas de `/` y `/otra-ruta` y ponemos en el navegador `/otra-ruta` se activará la funcion de `/` por que `/otra-ruta` contiene `/`. Para que esto funcione correctamente, se deberían de poner las rutas al revés (de arriba a abajo): `/otra-ruta` y `/`

```js
const express = require('express')
const app = express()

app.use('/otra-ruta', (req, res, next) => {
    console.log('Esta es la otra ruta')
})

app.use('/', (req, res, next) => {
    console.log('Esto es /')
})

const server = http.createServer(app)
server.listen(3000)

// app.get('/', (req, res) => {
//     res.send('Home Page')
// })

// app.get('/about', (req, res) => {
//     res.send('About Page')
// })
```

---

### 5. **Parsing incoming requests**

Express.js ofrece varias formas de analizar (parsear) las solicitudes entrantes, como el análisis de datos JSON, datos URL codificados (formularios), o archivos binarios.
Para el parseo del request se puede usar `body-parser`

```js
const express = require('express')
const bodyParser = require('body-parser')

const app = express()

app.use(bodyParser.urlencoded({ extended: false })) // Parsea el request para que sea legible, pero no parsea todas las entradas (Como imágenes)

app.get('/add-product', (req, res, next) => {
    res.send(
        '<form action="/product" method="POST"><input type="text" name="title" /><button type="submit"></button></form>'
    )
})

app.post('/', (req, res, next) => {
    console.log(req.body)
    res.redirect('/')
})

const server = http.createServer(app)
server.listen(3000)
```

---

### 6. **Usando `express.Router()`**

Para mantener el código organizado, especialmente en aplicaciones grandes, Express tiene la clase `Router`, que permite definir rutas en archivos separados. Veamos cómo podemos mover las rutas a un archivo externo (`routes.js`).

#### Paso 1: Crear `routes.js`

```js
// routes.js
const express = require('express')
const router = express.Router()

// Definir las rutas en este archivo
router.get('/', (req, res) => {
    res.send('Home Page')
})

router.get('/about', (req, res) => {
    res.send('About Page')
})

// Exportar el router para que pueda ser usado en otros archivos
module.exports = router
```

#### Paso 2: Importar y usar `routes.js` en `app.js`

```js
// app.js
const express = require('express')
const app = express()

// Importar las rutas
const routes = require('./routes')

// Usar las rutas definidas en routes.js
app.use('/', routes)

app.listen(3000, () => {
    console.log('Servidor corriendo en http://localhost:3000')
})
```

Ahora, todas las rutas definidas en `routes.js` estarán disponibles en la aplicación principal.

---

### 7. **Adding a 404 Page**

Cuando un usuario visita una ruta no definida en tu aplicación, es una buena práctica mostrar una página 404. Esto se hace definiendo un middleware "catch-all" al final de todas las rutas.

```js
// Todas las rutas van aquí (rutas válidas)

app.use((req, res) => {
    res.status(404).send('404 - Página no encontrada')
})
```

Este middleware se activará si ninguna de las rutas anteriores coincide con la solicitud.

---

### 8. **Filtro de Paths**

A veces, es útil filtrar o restringir el acceso a ciertas rutas dependiendo de condiciones específicas, como autenticación, verificación de roles, etc.

Por ejemplo, aquí tienes un middleware que solo permite acceso a rutas específicas si el usuario está autenticado:

```js
// Middleware para verificar autenticación
function isAuthenticated(req, res, next) {
    const loggedIn = true // Simulación de autenticación
    if (loggedIn) {
        next() // Continuar si está autenticado
    } else {
        res.status(401).send('No autorizado')
    }
}

// Usamos el middleware solo en ciertas rutas
app.get('/dashboard', isAuthenticated, (req, res) => {
    res.send('Dashboard - Solo para usuarios autenticados')
})
```

Con este middleware, la ruta `/dashboard` solo estará disponible para usuarios autenticados. Puedes personalizar esta lógica según tus necesidades.

---

### Resumen

1. **Express.js** es un framework minimalista para Node.js que facilita la creación de aplicaciones web y APIs.
2. **Instalación**: Se puede instalar fácilmente usando npm.
3. **Middlewares** permiten modificar solicitudes y respuestas en tránsito, ya sea para parsear el cuerpo de las peticiones o para manejar seguridad, autenticación, etc.
4. **Rutas** se usan para definir cómo la aplicación responde a diferentes URL y métodos HTTP.
5. **Parsing**: Express ofrece varias utilidades para parsear datos entrantes.
6. **Express Router** permite separar y organizar rutas en módulos para mayor claridad.
7. **Página 404**: Es importante manejar rutas no encontradas de manera apropiada.
8. **Filtro de Paths**: Puedes restringir el acceso a rutas basándote en condiciones como autenticación.
