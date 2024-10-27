# useMemo

El hook `useMemo` en React se utiliza para memorizar (cachear) el resultado de una función costosa y solo recalcularlo cuando una de sus dependencias ha cambiado. Esto es útil para optimizar el rendimiento, evitando cálculos innecesarios en cada renderizado.

1. **Importación**: Primero, necesitas importar el hook desde React.

    ```jsx
    import React, { useMemo } from 'react'
    ```

2. **Sintaxis básica**:
    ```jsx
    const memoizedValue = useMemo(() => {
        // Cálculo costoso
        return result
    }, [dependencies])
    ```
    - **Función de cálculo**: Se ejecuta para calcular el valor cuando alguna de las dependencias ha cambiado.
    - **Dependencias**: Una lista de variables que, si cambian, harán que el valor se vuelva a calcular.

### Ejemplo Básico

Imaginemos que tenemos una lista de números y queremos calcular su suma solo cuando la lista cambia.

```jsx
import React, { useState, useMemo } from 'react'

function SumComponent() {
    const [numbers, setNumbers] = useState([1, 2, 3])

    const sum = useMemo(() => {
        console.log('Calculating sum...')
        return numbers.reduce((acc, number) => acc + number, 0)
    }, [numbers])

    return (
        <div>
            <p>Sum: {sum}</p>
            <button onClick={() => setNumbers([...numbers, numbers.length + 1])}>Add Number</button>
        </div>
    )
}

export default SumComponent
```

### Desglose del Ejemplo

-   **Estado Inicial**:

    ```jsx
    const [numbers, setNumbers] = useState([1, 2, 3])
    ```

    Se utiliza `useState` para almacenar la lista de números.

-   **Cálculo Memorízado**:
    ```jsx
    const sum = useMemo(() => {
        console.log('Calculating sum...')
        return numbers.reduce((acc, number) => acc + number, 0)
    }, [numbers])
    ```
    `useMemo` se utiliza para calcular la suma de los números solo cuando la lista de números cambia. La consola mostrará "Calculating sum..." solo cuando la lista se modifique.

### Uso Avanzado

`useMemo` es útil no solo para cálculos numéricos, sino también para memorizar cualquier valor derivado que sea costoso de calcular, como objetos o listas filtradas.

#### Ejemplo con Filtrado de Lista

Imaginemos que tenemos una lista de objetos y queremos filtrar los elementos que cumplen ciertos criterios.

```jsx
import React, { useState, useMemo } from 'react'

function FilterComponent() {
    const [query, setQuery] = useState('')
    const [items, setItems] = useState([
        { id: 1, name: 'Apple' },
        { id: 2, name: 'Banana' },
        { id: 3, name: 'Cherry' },
        { id: 4, name: 'Date' },
    ])

    const filteredItems = useMemo(() => {
        console.log('Filtering items...')
        return items.filter((item) => item.name.toLowerCase().includes(query.toLowerCase()))
    }, [query, items])

    return (
        <div>
            <input type="text" value={query} onChange={(e) => setQuery(e.target.value)} placeholder="Search..." />
            <ul>
                {filteredItems.map((item) => (
                    <li key={item.id}>{item.name}</li>
                ))}
            </ul>
        </div>
    )
}

export default FilterComponent
```

### Desglose del Ejemplo de Filtrado

-   **Estado Inicial**:

    ```jsx
    const [query, setQuery] = useState('')
    const [items, setItems] = useState([
        { id: 1, name: 'Apple' },
        { id: 2, name: 'Banana' },
        { id: 3, name: 'Cherry' },
        { id: 4, name: 'Date' },
    ])
    ```

    `useState` se utiliza para almacenar la consulta de búsqueda y la lista de elementos.

-   **Filtrado Memorízado**:
    ```jsx
    const filteredItems = useMemo(() => {
        console.log('Filtering items...')
        return items.filter((item) => item.name.toLowerCase().includes(query.toLowerCase()))
    }, [query, items])
    ```
    `useMemo` memoriza la lista filtrada y solo recalcula el filtrado cuando cambian `query` o `items`. La consola mostrará "Filtering items..." solo cuando la consulta o la lista se modifiquen.

### Comparación con `useCallback`

`useMemo` memoriza el resultado de una función, mientras que `useCallback` memoriza la propia función. Usualmente, `useCallback` se utiliza para funciones que se pasan como props a componentes hijos para evitar renderizados innecesarios.

#### Ejemplo Comparativo

```jsx
import React, { useState, useMemo, useCallback } from 'react'

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
            <ChildComponent increment={increment} />
            <p>Memoized Value: {memoizedValue}</p>
            <button onClick={increment}>Increment</button>
        </div>
    )
}

function ChildComponent({ increment }) {
    console.log('ChildComponent rendered')
    return <button onClick={increment}>Increment from Child</button>
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

    `useCallback` memoriza la función `increment` para evitar que se vuelva a crear en cada renderizado, lo que podría causar renderizados innecesarios del componente hijo.

-   **`useMemo`**:
    ```jsx
    const memoizedValue = useMemo(() => {
        return count * 2
    }, [count])
    ```
    `useMemo` memoriza el valor calculado `count * 2` y solo lo recalcula cuando `count` cambia.
