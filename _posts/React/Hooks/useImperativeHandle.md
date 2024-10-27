# useImperativeHandle

El hook `useImperativeHandle` en React se utiliza para personalizar la instancia de un objeto `ref` expuesto a componentes padres. Este hook es especialmente útil cuando necesitas exponer ciertos métodos o propiedades de un componente hijo al componente padre de una manera controlada.

1. **Importación**: Primero, necesitas importar el hook desde React.

    ```jsx
    import React, { useImperativeHandle, forwardRef, useRef } from 'react'
    ```

2. **Sintaxis básica**:
    ```jsx
    useImperativeHandle(
        ref,
        () => ({
            // Métodos y propiedades expuestos
        }),
        [dependencies]
    )
    ```
    - **`ref`**: La referencia pasada desde el componente padre.
    - **Función de creación**: Retorna un objeto con los métodos y propiedades que deseas exponer.
    - **Dependencias**: Una lista de variables que, si cambian, harán que la instancia del objeto `ref` se actualice.

### Ejemplo Básico

Imaginemos que tenemos un componente de entrada personalizado que queremos que el componente padre pueda enfocar y limpiar.

#### Componente Hijo

```jsx
import React, { useImperativeHandle, forwardRef, useRef } from 'react'

const CustomInput = forwardRef((props, ref) => {
    const inputRef = useRef()

    useImperativeHandle(ref, () => ({
        focus: () => {
            inputRef.current.focus()
        },
        clear: () => {
            inputRef.current.value = ''
        },
    }))

    return <input ref={inputRef} {...props} />
})

export default CustomInput
```

#### Componente Padre

```jsx
import React, { useRef } from 'react'
import CustomInput from './CustomInput'

function ParentComponent() {
    const inputRef = useRef()

    return (
        <div>
            <CustomInput ref={inputRef} placeholder="Enter text" />
            <button onClick={() => inputRef.current.focus()}>Focus Input</button>
            <button onClick={() => inputRef.current.clear()}>Clear Input</button>
        </div>
    )
}

export default ParentComponent
```

### Desglose del Ejemplo

-   **Creación de la Referencia en el Padre**:

    ```jsx
    const inputRef = useRef()
    ```

    Se crea una referencia en el componente padre que se pasará al componente hijo.

-   **Exposición de Métodos en el Hijo**:

    ```jsx
    useImperativeHandle(ref, () => ({
        focus: () => {
            inputRef.current.focus()
        },
        clear: () => {
            inputRef.current.value = ''
        },
    }))
    ```

    `useImperativeHandle` se utiliza para exponer los métodos `focus` y `clear` al componente padre.

-   **Uso de la Referencia en el Padre**:
    ```jsx
    <button onClick={() => inputRef.current.focus()}>Focus Input</button>
    <button onClick={() => inputRef.current.clear()}>Clear Input</button>
    ```
    El componente padre llama a los métodos expuestos a través de `inputRef`.

### Uso Avanzado

`useImperativeHandle` es útil cuando trabajas con componentes complejos o cuando necesitas un control fino sobre las interacciones entre componentes padres e hijos.

#### Ejemplo con Componente de Modal

Imaginemos que tenemos un componente de modal que el componente padre necesita poder abrir y cerrar programáticamente.

##### Componente Hijo (Modal)

```jsx
import React, { useState, useImperativeHandle, forwardRef } from 'react'

const Modal = forwardRef((props, ref) => {
    const [isOpen, setIsOpen] = useState(false)

    useImperativeHandle(ref, () => ({
        open: () => setIsOpen(true),
        close: () => setIsOpen(false),
    }))

    if (!isOpen) return null

    return (
        <div
            style={{
                position: 'fixed',
                top: '50%',
                left: '50%',
                transform: 'translate(-50%, -50%)',
                backgroundColor: 'white',
                padding: '1rem',
                zIndex: 1000,
            }}>
            <button onClick={() => setIsOpen(false)}>Close</button>
            <div>{props.children}</div>
        </div>
    )
})

export default Modal
```

##### Componente Padre

```jsx
import React, { useRef } from 'react'
import Modal from './Modal'

function ParentComponent() {
    const modalRef = useRef()

    return (
        <div>
            <button onClick={() => modalRef.current.open()}>Open Modal</button>
            <Modal ref={modalRef}>
                <h1>Modal Content</h1>
            </Modal>
        </div>
    )
}

export default ParentComponent
```

### Desglose del Ejemplo de Modal

-   **Estado de Apertura del Modal**:

    ```jsx
    const [isOpen, setIsOpen] = useState(false)
    ```

    `isOpen` controla si el modal está abierto o cerrado.

-   **Exposición de Métodos en el Hijo**:

    ```jsx
    useImperativeHandle(ref, () => ({
        open: () => setIsOpen(true),
        close: () => setIsOpen(false),
    }))
    ```

    `useImperativeHandle` expone los métodos `open` y `close` para controlar el estado del modal desde el componente padre.

-   **Uso de la Referencia en el Padre**:
    ```jsx
    <button onClick={() => modalRef.current.open()}>Open Modal</button>
    <Modal ref={modalRef}>
      <h1>Modal Content</h1>
    </Modal>
    ```
    El componente padre usa la referencia `modalRef` para abrir y cerrar el modal.
