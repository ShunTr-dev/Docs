---
title: useSyncExternalStore
date: 2024-07-17 00:00:00 -100
categories: [React, Hooks]
tags: [herramientas]
---

# useSyncExternalStore

`useSyncExternalStore` es un hook avanzado de React que se utiliza para suscribirse a un almacenamiento externo y sincronizar el estado de tu componente con ese almacenamiento. Este hook es especialmente útil cuando necesitas sincronizar el estado de tu componente con una fuente de datos externa que puede cambiar fuera del ciclo de vida del componente de React, como una API o un almacenamiento global.
Este Hook se usa muy raramente.

### Introducción a `useSyncExternalStore`

1. **Importación**: Primero, necesitas importar el hook desde React.

    ```jsx
    import { useSyncExternalStore } from 'react'
    ```

2. **Sintaxis básica**:
    ```jsx
    const state = useSyncExternalStore(subscribe, getSnapshot, getServerSnapshot)
    ```
    - `subscribe`: Una función que se usa para suscribirse a los cambios del almacenamiento externo.
    - `getSnapshot`: Una función que devuelve el estado actual del almacenamiento externo.
    - `getServerSnapshot`: (Opcional) Una función que devuelve el estado actual del almacenamiento externo cuando se renderiza en el servidor (para aplicaciones que utilizan SSR).

### Ejemplo Básico

Imaginemos que tenemos un almacenamiento externo simple que contiene un contador, y queremos sincronizar nuestro componente con este contador.

#### Almacenamiento Externo Simulado

Primero, creamos una pequeña utilidad para simular un almacenamiento externo.

```jsx
// externalStore.js
let count = 0
const listeners = new Set()

function increment() {
    count += 1
    listeners.forEach((listener) => listener())
}

function subscribe(listener) {
    listeners.add(listener)
    return () => listeners.delete(listener)
}

function getSnapshot() {
    return count
}

export { increment, subscribe, getSnapshot }
```

#### Componente React usando `useSyncExternalStore`

```jsx
import React from 'react'
import { useSyncExternalStore } from 'react'
import { increment, subscribe, getSnapshot } from './externalStore'

function Counter() {
    const count = useSyncExternalStore(subscribe, getSnapshot)

    return (
        <div>
            <p>Count: {count}</p>
            <button onClick={increment}>Increment</button>
        </div>
    )
}

export default Counter
```

### Desglose del Ejemplo

-   **Almacenamiento Externo**:

    -   `count`: Variable que mantiene el estado del contador.
    -   `listeners`: Conjunto de funciones que se llaman cuando `count` cambia.
    -   `increment`: Función que incrementa el contador y notifica a los suscriptores.
    -   `subscribe`: Función que permite a los componentes suscribirse a los cambios en `count`.
    -   `getSnapshot`: Función que devuelve el valor actual de `count`.

-   **Uso de `useSyncExternalStore` en el Componente**:

    ```jsx
    const count = useSyncExternalStore(subscribe, getSnapshot)
    ```

    `useSyncExternalStore` se usa para suscribirse al almacenamiento externo y obtener el estado actual del contador.

-   **Incrementar el Contador**:
    ```jsx
    <button onClick={increment}>Increment</button>
    ```
    El botón llama a la función `increment`, que incrementa el contador y notifica a los suscriptores.

### Estado Inicial en SSR

Si estás usando renderizado del lado del servidor (SSR), puedes pasar una tercera función a `useSyncExternalStore` que obtiene el estado inicial en el servidor.

```jsx
const state = useSyncExternalStore(subscribe, getSnapshot, getServerSnapshot)
```

-   **getServerSnapshot**: Esta función se llama en el servidor para obtener el estado inicial del almacenamiento externo.

### Ejemplo Completo con SSR

```jsx
import React from 'react'
import { useSyncExternalStore } from 'react'
import { increment, subscribe, getSnapshot } from './externalStore'

// Función para obtener el estado en el servidor
function getServerSnapshot() {
    return 0 // Estado inicial del contador en el servidor
}

function Counter() {
    const count = useSyncExternalStore(subscribe, getSnapshot, getServerSnapshot)

    return (
        <div>
            <p>Count: {count}</p>
            <button onClick={increment}>Increment</button>
        </div>
    )
}

export default Counter
```

### Conclusión

El hook `useSyncExternalStore` es útil para sincronizar componentes React con estados externos que pueden cambiar fuera del ciclo de vida del componente. Este hook es especialmente valioso en aplicaciones que necesitan mantenerse sincronizadas con fuentes de datos externas en tiempo real o en escenarios de SSR. Al entender cómo suscribirse y obtener instantáneas del estado externo, puedes manejar más eficazmente estados complejos y cambiantes en tus aplicaciones React.
