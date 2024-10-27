# useLayoutEffect

El hook `useLayoutEffect` es similar a `useEffect`, pero se ejecuta de manera diferente en el ciclo de vida del componente. Mientras que `useEffect` se ejecuta después de que se renderiza el componente y se actualiza el DOM, `useLayoutEffect` se ejecuta después de que se renderiza el componente, pero antes de que el navegador pinte la pantalla. Esto significa que `useLayoutEffect` se ejecuta de forma sincrónica y puede bloquear la actualización del DOM hasta que se complete.

1. **Importación**: Primero, necesitas importar el hook desde React.

    ```jsx
    import React, { useLayoutEffect } from 'react'
    ```

2. **Sintaxis básica**:
    ```jsx
    useLayoutEffect(() => {
        // Código del efecto
        return () => {
            // Código de limpieza (opcional)
        }
    }, [dependencies])
    ```
    - **Función de efecto**: Se ejecuta después de que el componente se renderiza pero antes de que el navegador actualice la pantalla.
    - **Función de limpieza (opcional)**: Se ejecuta antes de que el componente se desmonte o antes de ejecutar el efecto la próxima vez.
    - **Dependencias**: Una lista de variables que, si cambian, harán que el efecto se vuelva a ejecutar.

### Ejemplo Básico

Imaginemos que queremos medir el tamaño de un elemento después de que se haya renderizado.

```jsx
import React, { useState, useLayoutEffect, useRef } from 'react'

function SizeMeasure() {
    const [size, setSize] = useState({ width: 0, height: 0 })
    const divRef = useRef(null)

    useLayoutEffect(() => {
        if (divRef.current) {
            const { offsetWidth, offsetHeight } = divRef.current
            setSize({ width: offsetWidth, height: offsetHeight })
        }
    }, []) // Dependencias vacías significa que esto solo se ejecuta al montar

    return (
        <div>
            <div ref={divRef} style={{ width: '200px', height: '150px', backgroundColor: 'lightblue' }}>
                Measured Div
            </div>
            <p>
                Width: {size.width}px, Height: {size.height}px
            </p>
        </div>
    )
}

export default SizeMeasure
```

### Desglose del Ejemplo

-   **Estado Inicial**:

    ```jsx
    const [size, setSize] = useState({ width: 0, height: 0 })
    ```

    Se utiliza `useState` para almacenar las dimensiones del elemento.

-   **Referencia al Elemento**:

    ```jsx
    const divRef = useRef(null)
    ```

    Se utiliza `useRef` para referenciar el elemento DOM.

-   **Efecto de `useLayoutEffect`**:
    ```jsx
    useLayoutEffect(() => {
        if (divRef.current) {
            const { offsetWidth, offsetHeight } = divRef.current
            setSize({ width: offsetWidth, height: offsetHeight })
        }
    }, [])
    ```
    El `useLayoutEffect` mide las dimensiones del elemento después de que se ha renderizado pero antes de que el navegador pinte la pantalla.

### Efecto con Limpieza

Imaginemos que queremos añadir un event listener al redimensionar la ventana para volver a medir el tamaño del elemento.

```jsx
import React, { useState, useLayoutEffect, useRef } from 'react'

function SizeMeasure() {
    const [size, setSize] = useState({ width: 0, height: 0 })
    const divRef = useRef(null)

    useLayoutEffect(() => {
        const measure = () => {
            if (divRef.current) {
                const { offsetWidth, offsetHeight } = divRef.current
                setSize({ width: offsetWidth, height: offsetHeight })
            }
        }

        measure() // Medir al montar

        window.addEventListener('resize', measure)
        return () => {
            window.removeEventListener('resize', measure)
        }
    }, [])

    return (
        <div>
            <div ref={divRef} style={{ width: '200px', height: '150px', backgroundColor: 'lightblue' }}>
                Measured Div
            </div>
            <p>
                Width: {size.width}px, Height: {size.height}px
            </p>
        </div>
    )
}

export default SizeMeasure
```

### Desglose del Ejemplo de Limpieza

-   **Efecto de `useLayoutEffect` con Limpieza**:

    ```jsx
    useLayoutEffect(() => {
        const measure = () => {
            if (divRef.current) {
                const { offsetWidth, offsetHeight } = divRef.current
                setSize({ width: offsetWidth, height: offsetHeight })
            }
        }

        measure()

        window.addEventListener('resize', measure)
        return () => {
            window.removeEventListener('resize', measure)
        }
    }, [])
    ```

    -   `measure`: Función que mide las dimensiones del elemento.
    -   Se añade un event listener para el evento `resize` de la ventana y se limpia cuando el componente se desmonte.

### Diferencias entre `useEffect` y `useLayoutEffect`

-   **Timing**: `useEffect` se ejecuta después de que el navegador haya pintado la pantalla, mientras que `useLayoutEffect` se ejecuta después de que React ha hecho todas las actualizaciones del DOM pero antes de que el navegador pinte la pantalla.
-   **Uso**: `useLayoutEffect` es más adecuado para efectos que necesitan hacer mediciones del DOM o realizar operaciones que deben ocurrir antes de la pintura del navegador para evitar parpadeos visuales.
