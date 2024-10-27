---
title: useCallback
date: 2024-07-17 00:00:00 -100
categories: [React, Hooks]
tags: [herramientas]
---

# useCallback

El hook `useCallback` en React se utiliza para memorizar (cachear) funciones y así evitar que se creen nuevamente en cada renderizado, lo cual puede ayudar a mejorar el rendimiento de componentes, especialmente cuando estas funciones se pasan como props a componentes hijos que podrían renderearse innecesariamente.

### Introducción a `useCallback`

1. **Importación**: Primero, necesitas importar el hook desde React.

    ```jsx
    import React, { useCallback } from 'react'
    ```

2. **Sintaxis básica**:
    ```jsx
    const memoizedCallback = useCallback(() => {
        // Función lógica
    }, [dependencies])
    ```
    - **Función lógica**: La función que quieres memorizar.
    - **Dependencias**: Una lista de variables que, si cambian, harán que la función se vuelva a crear.

### Ejemplo Básico

Imaginemos que tenemos un componente que maneja un contador y pasa una función de incremento a un componente hijo.

#### Componente Padre

```jsx
import React, { useState, useCallback } from 'react'
import ChildComponent from './ChildComponent'

function ParentComponent() {
    const [count, setCount] = useState(0)

    const increment = useCallback(() => {
        setCount((c) => c + 1)
    }, [])

    return (
        <div>
            <p>Count: {count}</p>
            <ChildComponent onIncrement={increment} />
        </div>
    )
}

export default ParentComponent
```

#### Componente Hijo

```jsx
import React from 'react'

function ChildComponent({ onIncrement }) {
    console.log('ChildComponent rendered')
    return <button onClick={onIncrement}>Increment from Child</button>
}

export default ChildComponent
```

### Desglose del Ejemplo

-   **Creación del Estado y Función de Incremento**:

    ```jsx
    const [count, setCount] = useState(0)

    const increment = useCallback(() => {
        setCount((c) => c + 1)
    }, [])
    ```

    `useState` se utiliza para manejar el estado del contador. `useCallback` memoriza la función `increment` para evitar que se recree en cada renderizado, a menos que cambien sus dependencias (que en este caso es una lista vacía, por lo tanto nunca cambia).

-   **Uso de la Función en el Componente Hijo**:

    ```jsx
    <ChildComponent onIncrement={increment} />
    ```

    La función `increment` se pasa al componente hijo `ChildComponent` como una prop.

-   **Renderizado Condicional del Componente Hijo**:
    ```jsx
    console.log('ChildComponent rendered')
    ```
    El componente hijo solo se renderiza de nuevo si sus props cambian. Al usar `useCallback`, garantizamos que la función `increment` no cambia en cada renderizado del componente padre, evitando renderizados innecesarios del componente hijo.

### Uso Avanzado

`useCallback` es especialmente útil cuando se trabaja con listas de elementos o componentes complejos que podrían renderearse muchas veces.

#### Ejemplo con Lista de Items

Imaginemos que tenemos una lista de items y queremos manejar eventos en cada item de manera eficiente.

##### Componente Padre

```jsx
import React, { useState, useCallback } from 'react'
import ListItem from './ListItem'

function ItemList() {
    const [items, setItems] = useState(['Item 1', 'Item 2', 'Item 3'])

    const handleItemClick = useCallback((item) => {
        console.log(`Clicked on: ${item}`)
    }, [])

    return (
        <ul>
            {items.map((item) => (
                <ListItem key={item} item={item} onClick={handleItemClick} />
            ))}
        </ul>
    )
}

export default ItemList
```

##### Componente Hijo (ListItem)

```jsx
import React from 'react'

function ListItem({ item, onClick }) {
    console.log(`Rendering: ${item}`)
    return <li onClick={() => onClick(item)}>{item}</li>
}

export default ListItem
```

### Desglose del Ejemplo de Lista

-   **Función de Manejo de Click**:

    ```jsx
    const handleItemClick = useCallback((item) => {
        console.log(`Clicked on: ${item}`)
    }, [])
    ```

    `useCallback` memoriza la función `handleItemClick`, asegurando que no se recree en cada renderizado del componente padre.

-   **Renderizado de la Lista de Items**:
    ```jsx
    {
        items.map((item) => <ListItem key={item} item={item} onClick={handleItemClick} />)
    }
    ```
    Cada `ListItem` recibe la misma instancia de `handleItemClick`, evitando renderizados innecesarios.

### Comparación con `useMemo`

Mientras que `useCallback` memoriza funciones, `useMemo` memoriza el resultado de funciones. Ambos hooks son útiles para optimización, pero se utilizan en contextos ligeramente diferentes.

#### Ejemplo Comparativo

```jsx
import React, { useState, useCallback, useMemo } from 'react'

function ParentComponent() {
    const [count, setCount] = useState(0)

    const increment = useCallback(() => {
        setCount((c) => c + 1)
    }, [])

    const memoizedValue = useMemo(() => {
        return count * 2
    }, [count])

    return (
        <div>
            <p>Memoized Value: {memoizedValue}</p>
            <button onClick={increment}>Increment</button>
        </div>
    )
}

export default ParentComponent
```

### Desglose del Ejemplo Comparativo

-   **`useCallback`**:

    ```jsx
    const increment = useCallback(() => {
        setCount((c) => c + 1)
    }, [])
    ```

    Memoriza la función `increment` para que no cambie entre renderizados, a menos que cambien las dependencias.

-   **`useMemo`**:
    ```jsx
    const memoizedValue = useMemo(() => {
        return count * 2
    }, [count])
    ```
    Memoriza el valor calculado `count * 2` y solo lo recalcula cuando `count` cambia.
