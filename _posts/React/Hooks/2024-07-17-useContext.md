---
title: useContext
date: 2024-07-17 00:00:00 -100
categories: [React, Hooks]
tags: [react, hooks, usecontext]
---

# useContext

El hook `useContext` en React se utiliza para acceder al contexto proporcionado por el componente `Context.Provider` más cercano en la jerarquía de componentes. Permite a los componentes consumir valores de contexto sin necesidad de pasar props manualmente a través de cada nivel del árbol de componentes.

1. **Importación**: Primero, necesitas importar el hook desde React.

    ```jsx
    import React, { useContext } from 'react'
    ```

2. **Sintaxis básica**:
    ```jsx
    const value = useContext(MyContext)
    ```
    - **`MyContext`**: El objeto de contexto creado con `React.createContext`.
    - **`value`**: El valor actual del contexto proporcionado por el contexto más cercano en la jerarquía de componentes.

### Creación de un Contexto

Primero, creemos un contexto que proporcionará un tema para la aplicación.

```jsx
import React, { createContext, useState } from 'react'

// Creamos un contexto con un valor inicial
const ThemeContext = createContext('light')

// Componente proveedor que envuelve la aplicación
function ThemeProvider({ children }) {
    const [theme, setTheme] = useState('light')

    const toggleTheme = () => {
        setTheme((prevTheme) => (prevTheme === 'light' ? 'dark' : 'light'))
    }

    return <ThemeContext.Provider value={{ theme, toggleTheme }}>{children}</ThemeContext.Provider>
}

export { ThemeProvider, ThemeContext }
```

### Uso de `useContext`

Ahora podemos consumir el contexto `ThemeContext` en cualquier componente hijo dentro del árbol del `ThemeProvider`.

```jsx
import React, { useContext } from 'react'
import { ThemeContext } from './ThemeProvider'

function ThemeToggler() {
    const { theme, toggleTheme } = useContext(ThemeContext)

    return <button onClick={toggleTheme}>Switch to {theme === 'light' ? 'dark' : 'light'} mode</button>
}

export default ThemeToggler
```

### Desglose del Ejemplo

-   **Creación del Contexto**:

    ```jsx
    const ThemeContext = createContext('light')
    ```

    Creamos un contexto con un valor inicial de `'light'`.

-   **Proveedor de Contexto**:

    ```jsx
    <ThemeContext.Provider value={{ theme, toggleTheme }}>{children}</ThemeContext.Provider>
    ```

    `ThemeProvider` envuelve la aplicación y proporciona el contexto `ThemeContext` a todos los componentes descendientes.

-   **Consumo de Contexto con `useContext`**:

    ```jsx
    const { theme, toggleTheme } = useContext(ThemeContext)
    ```

    `useContext` se utiliza en `ThemeToggler` para acceder al valor del contexto `ThemeContext` y a la función `toggleTheme` proporcionada por `ThemeProvider`.

-   **Uso del Contexto en Componente Hijo**:
    ```jsx
    <button onClick={toggleTheme}>Switch to {theme === 'light' ? 'dark' : 'light'} mode</button>
    ```
    El botón cambia el tema entre "light" y "dark" usando la función `toggleTheme` del contexto.

### Uso Avanzado

`useContext` es útil para compartir datos que son necesarios en varios componentes sin tener que pasar props manualmente a través de cada nivel del árbol de componentes. También puede ser usado para manejar estados globales o temas como en el ejemplo anterior.

#### Ejemplo con Autenticación

Imaginemos que tenemos un contexto para manejar la autenticación de usuario.

##### Creación del Contexto

```jsx
import React, { createContext, useState } from 'react'

const AuthContext = createContext()

function AuthProvider({ children }) {
    const [user, setUser] = useState(null)

    const login = (username, password) => {
        // Lógica de autenticación aquí...
        setUser({ username })
    }

    const logout = () => {
        setUser(null)
    }

    return <AuthContext.Provider value={{ user, login, logout }}>{children}</AuthContext.Provider>
}

export { AuthProvider, AuthContext }
```

##### Consumo del Contexto

```jsx
import React, { useContext, useState } from 'react'
import { AuthContext } from './AuthProvider'

function Login() {
    const { login } = useContext(AuthContext)
    const [username, setUsername] = useState('')
    const [password, setPassword] = useState('')

    const handleLogin = () => {
        login(username, password)
    }

    return (
        <div>
            <input type="text" value={username} onChange={(e) => setUsername(e.target.value)} placeholder="Username" />
            <input
                type="password"
                value={password}
                onChange={(e) => setPassword(e.target.value)}
                placeholder="Password"
            />
            <button onClick={handleLogin}>Login</button>
        </div>
    )
}

export default Login
```

### Desglose del Ejemplo de Autenticación

-   **Creación del Contexto de Autenticación**:

    ```jsx
    const AuthContext = createContext()
    ```

    Creamos un contexto para manejar la autenticación de usuario.

-   **Proveedor de Contexto de Autenticación**:

    ```jsx
    <AuthContext.Provider value={{ user, login, logout }}>{children}</AuthContext.Provider>
    ```

    `AuthProvider` envuelve la aplicación y proporciona el contexto `AuthContext` a todos los componentes descendientes.

-   **Consumo de Contexto con `useContext`**:

    ```jsx
    const { login } = useContext(AuthContext)
    ```

    `useContext` se utiliza en `Login` para acceder a la función `login` proporcionada por `AuthProvider`.

-   **Uso del Contexto en el Componente Hijo**:
    ```jsx
    <button onClick={handleLogin}>Login</button>
    ```
    El botón llama a `handleLogin`, que a su vez llama a la función `login` del contexto para autenticar al usuario con el nombre de usuario y contraseña ingresados.
