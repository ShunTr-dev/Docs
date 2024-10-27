# useReducer

El hook `useReducer` es otra opción (a parte de `useState`) para manejar el estado en componentes funcionales en React. Es particularmente útil para gestionar estados complejos y lógica de actualización más avanzada. Veamos una descripción detallada de `useReducer`, su uso y ejemplos.
No se usa tanto como `useState`, pero es muy bueno gestionando estados que tienen relaciones.

1. **Importación**: Primero, necesitas importar el hook desde React.

    ```jsx
    import React, { useReducer } from 'react'
    ```

2. **Sintaxis básica**:
    ```jsx
    const [state, dispatch] = useReducer(reducer, initialState)
    ```
    - `state`: El valor actual del estado.
    - `dispatch`: Una función que se usa para enviar acciones que actualizarán el estado.
    - `reducer`: Una función que determina cómo actualizar el estado en respuesta a una acción.
    - `initialState`: El valor inicial del estado.

### Definición del Reducer

El reducer es una función que toma el estado actual y una acción, y devuelve un nuevo estado. La firma del reducer es:

```jsx
;(state, action) => newState
```

### Ejemplo Básico

```jsx
import React, { useReducer } from 'react'

// Definición del estado inicial
const initialState = { count: 0 }

// Definición del reducer
function reducer(state, action) {
    switch (action.type) {
        case 'increment':
            return { count: state.count + 1 }
        case 'decrement':
            return { count: state.count - 1 }
        default:
            throw new Error()
    }
}

function Counter() {
    // Uso de useReducer
    const [state, dispatch] = useReducer(reducer, initialState)

    return (
        <div>
            <p>You clicked {state.count} times</p>
            <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
            <button onClick={() => dispatch({ type: 'decrement' })}>Decrement</button>
        </div>
    )
}

export default Counter
```

### Desglose del Ejemplo

-   **Estado Inicial**:

```jsx
const initialState = { count: 0 }
```

Define el estado inicial del contador.

-   **Reducer**:

```jsx
function reducer(state, action) {
    switch (action.type) {
        case 'increment':
            return { count: state.count + 1 }
        case 'decrement':
            return { count: state.count - 1 }
        default:
            throw new Error()
    }
}
```

    El reducer maneja dos tipos de acciones: `increment` y `decrement`, y actualiza el estado en consecuencia.

-   **Uso de `useReducer`**:

```jsx
const [state, dispatch] = useReducer(reducer, initialState)
```

`state` es el estado actual, y `dispatch` es una función para enviar acciones al reducer.

-   **Envío de Acciones**:

```jsx
<button onClick={() => dispatch({ type: 'increment' })}>
    Increment
</button>
<button onClick={() => dispatch({ type: 'decrement' })}>
    Decrement
</button>
```

Se utilizan botones para enviar acciones al reducer, lo que actualiza el estado.

### Estado Complejo

`useReducer` es muy útil cuando se maneja un estado más complejo. Por ejemplo, un formulario con múltiples campos.

```jsx
import React, { useReducer } from 'react'

const initialState = {
    name: '',
    age: '',
    email: '',
}

function reducer(state, action) {
    switch (action.type) {
        case 'updateField':
            return {
                ...state,
                [action.field]: action.value,
            }
        default:
            throw new Error()
    }
}

function UserForm() {
    const [state, dispatch] = useReducer(reducer, initialState)

    const handleChange = (e) => {
        dispatch({
            type: 'updateField',
            field: e.target.name,
            value: e.target.value,
        })
    }

    return (
        <form>
            <label>
                Name:
                <input name="name" value={state.name} onChange={handleChange} />
            </label>
            <br />
            <label>
                Age:
                <input name="age" value={state.age} onChange={handleChange} />
            </label>
            <br />
            <label>
                Email:
                <input name="email" value={state.email} onChange={handleChange} />
            </label>
            <br />
            <p>Name: {state.name}</p>
            <p>Age: {state.age}</p>
            <p>Email: {state.email}</p>
        </form>
    )
}

export default UserForm
```

### Desglose del Ejemplo de Estado Complejo

-   **Estado Inicial**:

```jsx
const initialState = {
    name: '',
    age: '',
    email: '',
}
```

-   **Reducer**:

```jsx
function reducer(state, action) {
    switch (action.type) {
        case 'updateField':
            return {
                ...state,
                [action.field]: action.value,
            }
        default:
            throw new Error()
    }
}
```

-   **Envío de Acciones en el Formulario**:

```jsx
const handleChange = (e) => {
    dispatch({
        type: 'updateField',
        field: e.target.name,
        value: e.target.value,
    })
}
```
