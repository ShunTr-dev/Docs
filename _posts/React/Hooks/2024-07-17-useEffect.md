---
title: useEffect
date: 2024-07-17 00:00:00 -100
categories: [React, Hooks]
tags: [herramientas]
---

# useEffect

El hook `useEffect` es uno de los hooks más importantes y versátiles en React. Se utiliza para gestionar efectos secundarios en componentes funcionales, como hacer llamadas a APIs, suscribirse a servicios, actualizar el DOM, y mucho más.

**Nota: Se recomienda no usarlo como cambios directos a elementos de escucha (es mejor usar un onClick) y para traer datos de lugares externos, que se recomienda usar (React query[https://www.npmjs.com/package/react-query]) o la herramienta del propio (framework[https://nextjs.org/])**

1. **Importación**: Primero, necesitas importar el hook desde React.

    ```jsx
    import React, { useEffect } from 'react'
    ```

2. **Sintaxis básica**:
    ```jsx
    useEffect(() => {
        // Código del efecto
        return () => {
            // Código de limpieza (opcional)
        }
    }, [dependencies])
    ```
    - **Función de efecto**: Se ejecuta después de que el componente se monte y después de cada actualización si las dependencias han cambiado.
    - **Función de limpieza (opcional)**: Se ejecuta antes de que el componente se desmonte o antes de ejecutar el efecto la próxima vez.
    - **Dependencias**: Una lista de variables que, si cambian, harán que el efecto se vuelva a ejecutar.

### Ejemplo Básico

Imaginemos que queremos hacer una llamada a una API para obtener datos cuando el componente se monta.

```jsx
import React, { useState, useEffect } from 'react'

function DataFetcher() {
    const [data, setData] = useState(null)

    useEffect(() => {
        // Efecto: Hacer una llamada a una API
        fetch('https://api.example.com/data')
            .then((response) => response.json())
            .then((data) => setData(data))
    }, []) // Dependencias vacías significa que esto solo se ejecuta al montar

    return (
        <div>
            <h1>Fetched Data</h1>
            {data ? <pre>{JSON.stringify(data, null, 2)}</pre> : <p>Loading...</p>}
        </div>
    )
}

export default DataFetcher
```

### Desglose del Ejemplo

-   **Estado Inicial**:

    ```jsx
    const [data, setData] = useState(null)
    ```

    Se utiliza `useState` para almacenar los datos obtenidos de la API.

-   **Efecto de `useEffect`**:
    ```jsx
    useEffect(() => {
        fetch('https://api.example.com/data')
            .then((response) => response.json())
            .then((data) => setData(data))
    }, [])
    ```
    El `useEffect` hace una llamada a la API cuando el componente se monta. Las dependencias vacías (`[]`) aseguran que esto solo ocurra una vez.

### Limpieza de Efectos

Cuando el efecto implica una suscripción o algún recurso que debe limpiarse, puedes devolver una función de limpieza.

#### Ejemplo con Suscripción

Imaginemos que tenemos un servicio de suscripción a un WebSocket que necesitamos limpiar cuando el componente se desmonte.

```jsx
import React, { useState, useEffect } from 'react'

function WebSocketComponent() {
    const [messages, setMessages] = useState([])

    useEffect(() => {
        const socket = new WebSocket('ws://example.com/socket')

        socket.addEventListener('message', (event) => {
            setMessages((prevMessages) => [...prevMessages, event.data])
        })

        // Función de limpieza
        return () => {
            socket.close()
        }
    }, []) // Dependencias vacías significa que esto solo se ejecuta al montar

    return (
        <div>
            <h1>Messages</h1>
            <ul>
                {messages.map((msg, index) => (
                    <li key={index}>{msg}</li>
                ))}
            </ul>
        </div>
    )
}

export default WebSocketComponent
```

### Desglose del Ejemplo de Limpieza

-   **Efecto de `useEffect` con Limpieza**:

    ```jsx
    useEffect(() => {
        const socket = new WebSocket('ws://example.com/socket')

        socket.addEventListener('message', (event) => {
            setMessages((prevMessages) => [...prevMessages, event.data])
        })

        return () => {
            socket.close()
        }
    }, [])
    ```

    -   La conexión WebSocket se crea al montar el componente.
    -   Se añade un listener para recibir mensajes.
    -   Se devuelve una función de limpieza que cierra el WebSocket cuando el componente se desmonte.

### Efectos con Dependencias

Los efectos pueden depender de variables que cambian. Imaginemos que queremos hacer una nueva llamada a una API cada vez que cambie una variable `query`.

```jsx
import React, { useState, useEffect } from 'react'

function SearchComponent() {
    const [query, setQuery] = useState('react')
    const [results, setResults] = useState([])

    useEffect(() => {
        if (query) {
            fetch(`https://api.example.com/search?q=${query}`)
                .then((response) => response.json())
                .then((data) => setResults(data.results))
        }
    }, [query]) // Ejecuta el efecto cuando `query` cambia

    return (
        <div>
            <input type="text" value={query} onChange={(e) => setQuery(e.target.value)} />
            <ul>
                {results.map((result, index) => (
                    <li key={index}>{result.name}</li>
                ))}
            </ul>
        </div>
    )
}

export default SearchComponent
```

### Desglose del Ejemplo con Dependencias

-   **Dependencia `query`**:
    ```jsx
    useEffect(() => {
        if (query) {
            fetch(`https://api.example.com/search?q=${query}`)
                .then((response) => response.json())
                .then((data) => setResults(data.results))
        }
    }, [query])
    ```
    El efecto se ejecuta cada vez que `query` cambia, haciendo una nueva llamada a la API y actualizando los resultados.
