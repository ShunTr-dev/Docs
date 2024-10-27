---
title: Node basics
date: 2024-10-24 00:00:00 -100
categories: [Node.js]
tags: [herramientas]
---

### 1. **Enviar respuestas**

Para enviar respuestas en Node.js, normalmente se utiliza el objeto `response` proporcionado por el módulo `http`. El método más común es `response.write()` para escribir en el cuerpo de la respuesta y `response.end()` para terminar la respuesta.

```js
const http = require('http')

const server = http.createServer((req, res) => {
    res.setHeader('Content-Type': 'text/plain')
    res.write('Hello, World!')
    res.end()
})

server.listen(3000, () => {
    console.log('Server running at http://localhost:3000/')
})
```

---

### 2. **[Cabeceras](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers) de peticiones y respuestas**

#### _Request_:

Para acceder a las cabeceras de una petición, se utiliza el objeto `req`:

```js
const server = http.createServer((req, res) => {
    console.log(req.headers) // Muestra todas las cabeceras
    res.end('Check console for headers')
})
```

#### _Response_:

Para configurar las cabeceras de la respuesta, se puede usar `res.setHeader()` o `res.writeHead()`.

```js
res.setHeader('Content-Type', 'application/json')
res.writeHead(200, { 'X-Custom-Header': 'MyValue' })
```

---

### 3. **Routing de peticiones**

El "routing" es el manejo diferentes URL dentro del servidor. Aunque Node.js no tiene un sistema de rutas incorporado, se puede implementar una lógica básica o utilizar librerías como `express`.

**Routing básico con Node.js:**

```js
const http = require('http')

const server = http.createServer((req, res) => {
    if (req.url === '/' && req.method === 'GET') {
        res.writeHead(200, { 'Content-Type': 'text/plain' })
        res.write('Home Page')
        return res.end()
    } else if (req.url === '/about' && req.method === 'GET') {
        res.writeHead(200, { 'Content-Type': 'text/plain' })
        res.write('About Page')
        return res.end()
    } else {
        res.writeHead(404, { 'Content-Type': 'text/plain' })
        res.write('Not Found')
        return res.end()
    }
})

server.listen(3000)
```

---

### 4. **Redirección de peticiones**

Para redirigir una petición, se usa la cabecera `Location` junto con el código de estado `301` o `302`:

```js
const http = require('http')

const server = http.createServer((req, res) => {
    if (req.url === '/old-route') {
        res.writeHead(301, { Location: '/new-route' })
        res.end()
    } else if (req.url === '/new-route') {
        res.writeHead(200, { 'Content-Type': 'text/plain' })
        res.end('You have been redirected')
    } else {
        res.writeHead(404)
        res.end('Not Found')
    }
})

server.listen(3000)
```

---

### 5. **Parseo del cuerpo de peticiones**

Node.js no parsea el cuerpo de la petición por defecto, es necesario manejar esto manualmente o usar un middleware como `body-parser`.

#### Parseo manual de JSON:

```js
const http = require('http')

const server = http.createServer((req, res) => {
    if (req.method === 'POST') {
        let body = []
        req.on('data', (chunk) => {
            // Permite escuchar eventos, disparándose cada vez que un bloque de texto está listo para ser leído
            // body += chunk.toString() // Agregar cada trozo de datos
            body.push(chunk)
        })
        req.on('end', () => {
            // Se dispara al terminar de leer los datos
            // const parsedData = JSON.parse(body)
            const parsedBody = Buffer.concat.(body).toString()
            res.end(`Received data: ${parsedData.name}`)
        })
    }
})

server.listen(3000)
```

---

### 6. **Blocking y Non-Blocking Code**

**Código Bloqueante**:
El código que bloquea la ejecución de otras operaciones hasta que la tarea actual se complete. Por ejemplo, leer un archivo de forma síncrona bloquea el programa hasta que el archivo se haya leído completamente.

```js
const fs = require('fs')
const data = fs.readFileSync('file.txt', 'utf8') // Bloquea hasta que se lea el archivo
console.log(data)
```

**Código No Bloqueante**:
Las funciones no bloqueantes permiten que otras operaciones continúen mientras se espera la finalización de una tarea.

```js
fs.readFile('file.txt', 'utf8', (err, data) => {
    if (err) throw err
    console.log(data)
})

fs.writeFile('message.txt', message, (err) => {
    console.log(message)
})
```

---

### 7. **Usando el sistema de módulos de Node.js**

Node.js usa el sistema de módulos CommonJS para organizar el código en archivos y reutilizar funciones.

**Crear un módulo:**

Por ejemplo si quieres poner de manera separada las rutas en otro archivo crea el archivo `routes.js`.

```js
cons requestHandler = (req, res) => {
    const url = req.url;
    const method = req.method

    if (url === '/' && method === 'GET') {
        res.writeHead(200, { 'Content-Type': 'text/plain' })
        res.write('Home Page')
        return res.end()
    } else if (url === '/about' && method === 'GET') {
        res.writeHead(200, { 'Content-Type': 'text/plain' })
        res.write('About Page')
        return res.end()
    } else {
        res.writeHead(404, { 'Content-Type': 'text/plain' })
        res.write('Not Found')
        return res.end()
    }
}

module.exports = requestHandler
// Se puede exponer la función globalmente con module.exports
```

En el archivo principal (`app.js` o `server.js`), importa las rutas desde `routes.js`.

```js
const http = require('http')
// Importar las rutas desde routes.js
const routes = require('./routes') // Como no es un módulo global, le decimos la localización con './'

const server = http.createServer(routes)

server.listen(3000, () => {
    console.log('Server running on http://localhost:3000')
})
```
