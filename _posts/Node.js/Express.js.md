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

app.get('/otra-ruta', (req, res, next) => {
    console.log('Esta es la otra ruta')
})

app.use('/', (req, res, next) => {
    console.log('Esto es /')
})

const server = http.createServer(app)
server.listen(3000)
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
// bodyParser.json()
// Como se puede ver, hace una llamada a la función de next() aunque no se lo pidamos

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
const express = require('express')
const router = express.Router()

// Definir las rutas en este archivo
router.get('/', (req, res) => {
    console.log('Root route')
    res.json({ message: 'Root route' })
})

// Exportar el router para que pueda ser usado en otros archivos
module.exports = router
```

#### Paso 2: Importar y usar `routes.js` en `app.js`

```js
const express = require('express')
const app = express()

// Importar las rutas
const routes = require('./routes')
const routesUsers = require('./routes/usersRouters')

// Usar las rutas definidas en routes.js
app.use('/api/users', usersRouters)
app.use(routes)

app.listen(3000, () => {
    console.log('Servidor corriendo en http://localhost:3000')
})
```

#### 3: Rutas más complejas

```js
// Este podría ser la ruta users
const express = require('express')
const router = express.Router()

// Como ya le pusimos la ruta en el app.js no hace falta repetirla aquí
router.get('/:uid', (req, res) => {
    res.json({ user: { name: 'Pepe' } })
})

module.exports = router
```

---

<!-- ### 7. **Adding a 404 Page**

Cuando un usuario visita una ruta no definida en tu aplicación, es una buena práctica mostrar una página 404. Esto se hace definiendo un middleware "catch-all" al final de todas las rutas.

```js
// Todas las rutas van aquí (rutas válidas)

app.use((req, res) => {
    res.status(404).send('404 - Página no encontrada')
})
```

Este middleware se activará si ninguna de las rutas anteriores coincide con la solicitud.

---
-->

### 2. Manejo de Errores

Un buen manejo de errores mejora la experiencia del usuario y ayuda a los desarrolladores a diagnosticar problemas en el backend. Express permite un **middleware de manejo de errores** para capturar cualquier excepción o problema en la aplicación y responder de manera uniforme.

### Ejemplo de manejo simple

```js
// Ejemplo no se encontró un usuario
if (!user) {
    return res.status(404).json({ message: 'User not found' })
}
```

#### Ejemplo de middleware de manejo de errores (`middlewares/errorHandler.js`):

```js
// middlewares/errorHandler.js
module.exports = (error, req, res, next) => {
    // Miramos si ya se establecieron las cabeceras para ver si el error se manejó en otro lado
    if (res.headerSent) {
        return next(error)
    }

    res.status(error.code || 500)
    res.json({ message: error.message || 'An unknown error ocurred!' })
}
```

Si queremos lanzar el error desde uno de los controladores tenemos que pasarle el error. Si es un código síncrono se puede hacer con `next()` pero si es asíncrono se debe hacer con `throw`.

```js
if (!user) {
    const error = new Error('Could not find user for the provided id')
    error.code = 404
    return next(error)
}
```

Este middleware debe agregarse al final de las rutas en `app.js`:

```js
const express = require('express')
const app = express()
const errorHandler = require('./middlewares/errorHandler')

// Otras configuraciones y rutas

// Middleware de manejo de errores
app.use(errorHandler)

app.listen(3000, () => console.log('Servidor corriendo en http://localhost:3000'))
```

---

### 3. Modelo propio de errores

Crear un modelo de error personalizado ayuda a generar mensajes de error específicos y a controlar su estado. Así puedes personalizar mejor las respuestas de error.

#### Ejemplo de un modelo de error (`utils/customError.js`):

```js
// models/http-error.js
class HttpError extends Error {
    constructor(message, errorCode) {
        super(message)
        this.code = errorCode
    }
}

module.exports = HttpError
```

Para usar este modelo, puedes lanzar errores personalizados en los controladores:

```js
const HttpError = require('../model/http-error')

exports.getItemById = async (req, res, next) => {
    if (!user) {
        throw new HttpError('Could not find a user', 404)
    }
}
```

---

### 1. Añadir Controladores

Los **controladores** son funciones que manejan la lógica de cada ruta en la API. Cada controlador generalmente se organiza en función de un modelo o entidad (por ejemplo, `UserController`, `ProductController`). Esto permite separar la lógica de la definición de las rutas, manteniendo el código más modular y fácil de escalar.

#### Ejemplo de controlador básico (`controllers/itemController.js`):

```js
// controllers/itemController.js
const Item = require('../models/Item') // Importa el modelo de la base de datos

// Obtener todos los ítems
exports.getAllItems = async (req, res, next) => {
    try {
        const items = await Item.find()
        res.status(200).json({ success: true, data: items })
    } catch (error) {
        next(error) // Pasa el error al manejador de errores
    }
}

// Crear un nuevo ítem
exports.createItem = async (req, res, next) => {
    try {
        const newItem = await Item.create(req.body)
        res.status(201).json({ success: true, data: newItem })
    } catch (error) {
        next(error)
    }
}
```

Para poder llamarlas desde la ruta tenemos que incluírlas en el archivo de routes

```js
const itemController = require('../controllers/itemController')

router.get('/', itemController.getAllItems)

module.exports = router
```

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

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

### 4. Validar los inputs de la API

La validación es fundamental para asegurar que los datos que recibe la API cumplen con ciertos requisitos antes de ser procesados. Puedes usar paquetes como `express-validator` para validar y sanitizar los datos.

#### Ejemplo de validación con `express-validator`:

1. Instala `express-validator`:

    ```bash
    npm install express-validator
    ```

2. Define las validaciones en el controlador (`controllers/itemController.js`):

    ```js
    const { body, validationResult } = require('express-validator')

    exports.validateItem = [
        body('name').isString().withMessage('El nombre debe ser una cadena'),
        body('price').isFloat({ gt: 0 }).withMessage('El precio debe ser un número mayor a 0'),
        (req, res, next) => {
            const errors = validationResult(req)
            if (!errors.isEmpty()) {
                return res.status(400).json({ errors: errors.array() })
            }
            next()
        },
    ]
    ```

3. Usa esta validación en tus rutas:

    ```js
    const express = require('express')
    const router = express.Router()
    const itemController = require('../controllers/itemController')

    router.post('/items', itemController.validateItem, itemController.createItem)

    module.exports = router
    ```

---

### 5. Conexión con MongoDB

Para conectar una aplicación de Node.js con MongoDB, puedes usar el paquete `mongoose`.

1. Instala Mongoose:

    ```bash
    npm install mongoose
    ```

2. Configura la conexión en tu archivo principal (`app.js`):

    ```js
    const mongoose = require('mongoose')

    mongoose
        .connect('mongodb://localhost:27017/mi_base_datos', {
            useNewUrlParser: true,
            useUnifiedTopology: true,
        })
        .then(() => console.log('Conectado a MongoDB'))
        .catch((error) => console.error('Error de conexión:', error))
    ```

3. Define un modelo de datos, por ejemplo `models/Item.js`:

    ```js
    const mongoose = require('mongoose')

    const itemSchema = new mongoose.Schema({
        name: { type: String, required: true },
        price: { type: Number, required: true },
    })

    module.exports = mongoose.model('Item', itemSchema)
    ```

---

### 6. Petición de ver una entrada y devolverla

En el controlador, define una función para obtener un ítem por su ID:

```js
exports.getItemById = async (req, res, next) => {
    try {
        const item = await Item.findById(req.params.id)
        if (!item) {
            throw new CustomError('Ítem no encontrado', 404)
        }
        res.status(200).json({ success: true, data: item })
    } catch (error) {
        next(error)
    }
}
```

---

### 7. Petición de editar una entrada

Para actualizar una entrada, crea un método `updateItem` en el controlador:

```js
exports.updateItem = async (req, res, next) => {
    // const {name, age, ...} = req.body

    try {
        const updatedItem = await Item.findByIdAndUpdate(req.params.id, req.body, {
            new: true,
            runValidators: true,
        })
        if (!updatedItem) {
            throw new CustomError('Ítem no encontrado', 404)
        }
        res.status(200).json({ success: true, data: updatedItem })
    } catch (error) {
        next(error)
    }
}
```

---

### 8. Petición de eliminar una entrada

Para eliminar una entrada, crea un método `deleteItem` en el controlador:

```js
exports.deleteItem = async (req, res, next) => {
    try {
        const deletedItem = await Item.findByIdAndDelete(req.params.id)
        if (!deletedItem) {
            throw new CustomError('Ítem no encontrado', 404)
        }
        res.status(200).json({ success: true, message: 'Ítem eliminado correctamente' })
    } catch (error) {
        next(error)
    }
}
```
