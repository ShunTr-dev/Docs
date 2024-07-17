# useState

El hook `useState` te permite añadir el estado de React a un componente funcional.
Es ideal para componentes que necesitan un estado simple.
Se utiliza para añadir estado a los componentes funcionales, algo que antes solo se podía hacer con componentes de clase.

1. **Importación**: Primero, necesitas importar el hook desde React.

```jsx
import React, { useState } from 'react'
```

2. **Sintaxis básica**:

```jsx
const [state, setState] = useState(initialState)
```

-   `state`: El valor actual del estado.
-   `setState`: Una función que se usa para actualizar el estado.
-   `initialState`: El valor inicial del estado, puede ser cualquier tipo de dato (número, string, objeto, array, etc.).

### Ejemplo Básico

Imaginemos que tenemos un contador que queremos incrementar cada vez que se haga clic en un botón.

```jsx
import React, { useState } from 'react'

function Counter() {
    // Declarar una variable de estado llamada "count" y establecer su valor inicial en 0
    const [count, setCount] = useState(0)

    return (
        <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>Click me</button>
        </div>
    )
}

export default Counter
```

### Desglose del Ejemplo

-   **Declaración del Estado**: `const [count, setCount] = useState(0);`

    -   `count` es la variable que contiene el estado actual, que inicialmente es `0`.
    -   `setCount` es la función que actualiza el valor de `count`.
    -   `useState(0)` inicializa el estado con `0`.

-   **Uso del Estado en el JSX**:

```jsx
<p>You clicked {count} times</p>
```

    Aquí, `count` se utiliza para mostrar el número actual de clics.

-   **Actualización del Estado**:

```jsx
<button onClick={() => setCount(count + 1)}>Click me</button>
```

Cada vez que se hace clic en el botón, `setCount` se llama con `count + 1`, actualizando así el estado.

### Actualización Basada en el Estado Anterior

Cuando actualizas el estado basándote en el valor anterior, es más seguro usar una función de actualización que toma el valor anterior como argumento:

```jsx
<button onClick={() => setCount((prevCount) => prevCount + 1)}>Click me</button>
```

### Estado Complejo

`useState` puede manejar estados complejos como objetos y arrays. Es importante crear copias del estado anterior cuando se actualiza para mantener la inmutabilidad.

**Actualizando un objeto:**

```jsx
const [user, setUser] = useState({ name: 'John', age: 30 })

const updateUserName = () => {
    setUser((prevUser) => ({
        ...prevUser,
        name: 'Jane',
    }))
}
```

**Actualizando un array:**

```jsx
const [items, setItems] = useState(['Item 1', 'Item 2'])

const addItem = () => {
    setItems((prevItems) => [...prevItems, `Item ${prevItems.length + 1}`])
}
```

### Ejemplo Completo con Objeto

```jsx
import React, { useState } from 'react'

function UserProfile() {
    const [user, setUser] = useState({
        name: 'John',
        age: 30,
        email: 'john@example.com',
    })

    const updateEmail = () => {
        setUser((prevUser) => ({
            ...prevUser,
            email: 'john.doe@example.com',
        }))
    }

    return (
        <div>
            <p>Name: {user.name}</p>
            <p>Age: {user.age}</p>
            <p>Email: {user.email}</p>
            <button onClick={updateEmail}>Update Email</button>
        </div>
    )
}

export default UserProfile
```
