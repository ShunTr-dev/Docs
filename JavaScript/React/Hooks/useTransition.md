# useTransition

El hook `useTransition` en React es parte de las nuevas API de React Concurrent Mode, diseñado para manejar las animaciones y transiciones de manera fluida y optimizada, especialmente cuando se realizan cambios en el estado que podrían causar re-renderizados visibles en la interfaz de usuario.

### Introducción a `useTransition`

1. **Importación**: Primero, necesitas importar el hook desde React.

    ```jsx
    import React, { useState, useTransition } from 'react'
    ```

2. **Sintaxis básica**:
    ```jsx
    const [startTransition, isPending] = useTransition({ timeoutMs })
    ```
    - **`startTransition`**: Función para iniciar una transición de manera concurrente.
    - **`isPending`**: Booleano que indica si la transición está pendiente.
    - **`timeoutMs`** (opcional): Tiempo máximo en milisegundos que React esperará antes de renderear la interfaz de usuario nuevamente.

### Ejemplo Básico

Vamos a crear un componente simple que muestra cómo usar `useTransition` para animar cambios de estado.

```jsx
import React, { useState, useTransition } from 'react'

function TransitionComponent() {
    const [isVisible, setIsVisible] = useState(false)
    const [startTransition, isPending] = useTransition({ timeoutMs: 200 })

    const toggleVisibility = () => {
        startTransition(() => {
            setIsVisible((prev) => !prev)
        })
    }

    return (
        <div>
            <button onClick={toggleVisibility}>Toggle Visibility</button>
            {isPending ? <p>Loading...</p> : null}
            {isVisible ? <div style={{ width: '100px', height: '100px', background: 'red' }} /> : null}
        </div>
    )
}

export default TransitionComponent
```

### Desglose del Ejemplo

-   **Estado y Función de Toggle**:

    ```jsx
    const [isVisible, setIsVisible] = useState(false)
    ```

    `useState` se utiliza para manejar el estado de visibilidad del componente.

-   **Inicio de la Transición**:

    ```jsx
    const [startTransition, isPending] = useTransition({ timeoutMs: 200 })
    ```

    `useTransition` se llama para obtener `startTransition`, una función que inicia la transición de manera concurrente, y `isPending`, un booleano que indica si la transición está en curso.

-   **Función para Alternar la Visibilidad**:

    ```jsx
    const toggleVisibility = () => {
        startTransition(() => {
            setIsVisible((prev) => !prev)
        })
    }
    ```

    Cuando se hace clic en el botón, `toggleVisibility` se llama y usa `startTransition` para cambiar el estado de `isVisible` de manera que inicie una transición concurrente.

-   **Renderizado Condicional y Feedback Visual**:
    ```jsx
    {
        isPending ? <p>Loading...</p> : null
    }
    {
        isVisible ? <div style={{ width: '100px', height: '100px', background: 'red' }} /> : null
    }
    ```
    Se muestra un mensaje de carga (`Loading...`) mientras la transición está en curso (`isPending` es verdadero). Cuando `isVisible` es verdadero, se muestra un div rojo, que representa el componente visible.

### Uso Avanzado

`useTransition` es particularmente útil cuando se trata de manejar animaciones o transiciones complejas, especialmente en interfaces de usuario dinámicas o aplicaciones con muchos cambios de estado.

#### Ejemplo con Lista de Elementos

Vamos a crear un ejemplo donde una lista de elementos se anima al agregar o eliminar elementos.

```jsx
import React, { useState, useTransition } from 'react'

function ListComponent() {
    const [items, setItems] = useState([])
    const [startTransition, isPending] = useTransition({ timeoutMs: 300 })

    const addItem = () => {
        startTransition(() => {
            setItems((prevItems) => [...prevItems, items.length])
        })
    }

    const removeItem = () => {
        startTransition(() => {
            setItems((prevItems) => prevItems.slice(0, -1))
        })
    }

    return (
        <div>
            <button onClick={addItem}>Add Item</button>
            <button onClick={removeItem} disabled={items.length === 0}>
                Remove Item
            </button>
            {isPending ? <p>Loading...</p> : null}
            <ul>
                {items.map((item) => (
                    <li key={item}>Item {item}</li>
                ))}
            </ul>
        </div>
    )
}

export default ListComponent
```

### Desglose del Ejemplo de Lista

-   **Estado y Funciones de Modificación**:

    ```jsx
    const [items, setItems] = useState([])
    ```

    `useState` maneja el estado de la lista de elementos.

-   **Inicio de la Transición**:

    ```jsx
    const [startTransition, isPending] = useTransition({ timeoutMs: 300 })
    ```

    `useTransition` se utiliza para obtener `startTransition`, una función para iniciar transiciones concurrentes, y `isPending`, un booleano que indica si hay una transición pendiente.

-   **Funciones para Agregar y Quitar Elementos**:

    ```jsx
    const addItem = () => {
        startTransition(() => {
            setItems((prevItems) => [...prevItems, items.length])
        })
    }

    const removeItem = () => {
        startTransition(() => {
            setItems((prevItems) => prevItems.slice(0, -1))
        })
    }
    ```

    `addItem` y `removeItem` utilizan `startTransition` para agregar y quitar elementos de la lista respectivamente, iniciando transiciones concurrentes.

-   **Renderizado Condicional y Feedback Visual**:
    ```jsx
    {
        isPending ? <p>Loading...</p> : null
    }
    ;<ul>
        {items.map((item) => (
            <li key={item}>Item {item}</li>
        ))}
    </ul>
    ```
    Se muestra un mensaje de carga (`Loading...`) mientras la transición está en curso (`isPending` es verdadero). La lista de elementos se renderiza usando `items.map` con elementos `<li>`.
