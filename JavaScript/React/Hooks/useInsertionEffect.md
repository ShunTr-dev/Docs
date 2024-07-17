# useInsertionEffect

El hook `useInsertionEffect` se utiliza para inyectar estilos en el DOM antes de que se aplique el renderizado del navegador. Este hook es especialmente útil cuando trabajas con bibliotecas de estilización en línea como styled-components o Emotion, donde necesitas garantizar que los estilos CSS se apliquen antes de que cualquier otro efecto pueda causar un parpadeo visual o inconsistencias en el diseño.

1. **Importación**: Primero, necesitas importar el hook desde React.

    ```jsx
    import React, { useInsertionEffect } from 'react'
    ```

2. **Sintaxis básica**:
    ```jsx
    useInsertionEffect(() => {
        // Código para insertar estilos
        return () => {
            // Código de limpieza (opcional)
        }
    }, [dependencies])
    ```
    - **Función de inserción**: Se ejecuta inmediatamente después de que React ha realizado todas las mutaciones del DOM antes de que el navegador aplique los estilos y renderice la pantalla.
    - **Función de limpieza (opcional)**: Se ejecuta antes de que el componente se desmonte o antes de ejecutar la inserción la próxima vez.
    - **Dependencias**: Una lista de variables que, si cambian, harán que la inserción se vuelva a ejecutar.

### Ejemplo Básico

Imaginemos que queremos inyectar estilos en el DOM utilizando `useInsertionEffect`.

```jsx
import React, { useInsertionEffect, useState } from 'react'

function StyledComponent() {
    const [color, setColor] = useState('blue')

    useInsertionEffect(() => {
        const style = document.createElement('style')
        style.textContent = `
      .dynamic-color {
        color: ${color};
      }
    `
        document.head.appendChild(style)

        return () => {
            document.head.removeChild(style)
        }
    }, [color])

    return (
        <div>
            <p className="dynamic-color">This text will have a dynamic color!</p>
            <button onClick={() => setColor('red')}>Change to Red</button>
            <button onClick={() => setColor('green')}>Change to Green</button>
        </div>
    )
}

export default StyledComponent
```

### Desglose del Ejemplo

-   **Estado Inicial**:

    ```jsx
    const [color, setColor] = useState('blue')
    ```

    Se utiliza `useState` para almacenar el color dinámico.

-   **Efecto de `useInsertionEffect`**:

    ```jsx
    useInsertionEffect(() => {
        const style = document.createElement('style')
        style.textContent = `
        .dynamic-color {
          color: ${color};
        }
      `
        document.head.appendChild(style)

        return () => {
            document.head.removeChild(style)
        }
    }, [color])
    ```

    -   Se crea un elemento `<style>` y se añade al `<head>` del documento para aplicar estilos dinámicos.
    -   La función de limpieza elimina el elemento `<style>` del documento cuando el efecto se vuelve a ejecutar o el componente se desmonte.

### Diferencias entre `useInsertionEffect`, `useEffect` y `useLayoutEffect`

-   **`useEffect`**: Se ejecuta después de que el navegador ha pintado la pantalla. Ideal para efectos que no afectan el renderizado visual inmediato, como las llamadas a APIs.
-   **`useLayoutEffect`**: Se ejecuta después de que React ha hecho las mutaciones del DOM, pero antes de que el navegador pinte la pantalla. Útil para medir el DOM y evitar parpadeos visuales.
-   **`useInsertionEffect`**: Se ejecuta inmediatamente después de que React ha hecho las mutaciones del DOM, antes de que el navegador aplique estilos y renderice. Ideal para inyectar estilos CSS críticos que deben aplicarse antes del renderizado.

### Uso Avanzado

Cuando trabajas con bibliotecas de estilización en línea como Emotion o styled-components, `useInsertionEffect` puede ser extremadamente útil para asegurar que los estilos se apliquen de manera sincrónica y eviten cualquier parpadeo visual.

#### Ejemplo con styled-components

Si estás utilizando `styled-components`, podrías usar `useInsertionEffect` para asegurarte de que los estilos dinámicos se inyecten en el momento adecuado.

```jsx
import React, { useInsertionEffect, useState } from 'react'
import styled, { css, StyleSheetManager } from 'styled-components'

function StyledComponent() {
    const [color, setColor] = useState('blue')

    useInsertionEffect(() => {
        const style = document.createElement('style')
        style.textContent = `
      .dynamic-color {
        color: ${color};
      }
    `
        document.head.appendChild(style)

        return () => {
            document.head.removeChild(style)
        }
    }, [color])

    const DynamicText = styled.p`
        font-size: 20px;
        &.dynamic-color {
            color: ${color};
        }
    `

    return (
        <div>
            <DynamicText className="dynamic-color">This text will have a dynamic color!</DynamicText>
            <button onClick={() => setColor('red')}>Change to Red</button>
            <button onClick={() => setColor('green')}>Change to Green</button>
        </div>
    )
}

export default StyledComponent
```

El hook `useInsertionEffect` es una herramienta especializada para manejar la inyección de estilos CSS de manera sincrónica antes de que el navegador pinte la pantalla. Es especialmente útil cuando necesitas asegurar que los estilos críticos se apliquen sin causar parpadeos visuales, y se puede combinar eficazmente con bibliotecas de estilización en línea. Entender cómo y cuándo usar `useInsertionEffect` en lugar de otros hooks de efecto puede mejorar significativamente la experiencia visual y el rendimiento de tus aplicaciones React.
