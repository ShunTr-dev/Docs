---
title: useFormState
date: 2024-07-17 00:00:00 -100
categories: [React, Hooks]
tags: [herramientas]
---

# useFormState

`useFormState` es un hook personalizado que se utiliza para manejar y mantener el estado de un formulario en React. Este hook puede incluir el estado de los campos individuales del formulario, manejar la validación y gestionar eventos relacionados con la interacción del usuario, como cambios en los campos o envíos del formulario.

A continuación, te mostraré cómo puedes implementar `useFormState` para manejar el estado de un formulario básico, incluyendo los valores de los campos y su estado de validación.

```jsx
import { useState } from 'react'

// Hook personalizado useFormState
function useFormState(initialState = {}) {
    const [formState, setFormState] = useState(initialState)

    // Función para actualizar el valor de un campo del formulario
    const updateFieldValue = (fieldName, value) => {
        setFormState((prevState) => ({
            ...prevState,
            [fieldName]: value,
        }))
    }

    // Función para establecer el estado de validación de un campo del formulario
    const setFieldError = (fieldName, error) => {
        setFormState((prevState) => ({
            ...prevState,
            [fieldName]: {
                ...prevState[fieldName],
                error: error,
            },
        }))
    }

    // Función para restablecer el estado de un campo del formulario
    const resetFieldState = (fieldName) => {
        setFormState((prevState) => ({
            ...prevState,
            [fieldName]: initialState[fieldName] || '',
        }))
    }

    // Función para restablecer todos los campos del formulario al estado inicial
    const resetFormState = () => {
        setFormState(initialState)
    }

    return {
        formState,
        updateFieldValue,
        setFieldError,
        resetFieldState,
        resetFormState,
    }
}

export default useFormState
```

### Uso de `useFormState`

Ahora puedes utilizar `useFormState` en cualquier componente funcional de React para manejar el estado de un formulario, incluyendo los valores de los campos, el estado de validación y las funciones para actualizar este estado según las interacciones del usuario.

```jsx
import React from 'react'
import useFormState from './useFormState' // Asegúrate de importar el hook desde el archivo correcto

function MyForm() {
    const { formState, updateFieldValue, setFieldError, resetFieldState, resetFormState } = useFormState({
        username: { value: '', error: '' },
        email: { value: '', error: '' },
        password: { value: '', error: '' },
    })

    const handleSubmit = (event) => {
        event.preventDefault()

        // Validación de campos
        if (!formState.username.value) {
            setFieldError('username', 'El nombre de usuario es requerido')
            return
        }
        if (!formState.email.value) {
            setFieldError('email', 'El correo electrónico es requerido')
            return
        }
        if (!formState.password.value) {
            setFieldError('password', 'La contraseña es requerida')
            return
        }

        // Lógica para enviar el formulario (por ejemplo, una solicitud HTTP)
        submitForm()
        resetFormState()
    }

    const handleChange = (event) => {
        const { name, value } = event.target
        updateFieldValue(name, value)
        // Si se está editando el campo, eliminar el mensaje de error
        if (formState[name].error) {
            setFieldError(name, '')
        }
    }

    return (
        <form onSubmit={handleSubmit}>
            <h2>Registro de Usuario</h2>
            <div>
                <label>Nombre de Usuario:</label>
                <input type="text" name="username" value={formState.username.value} onChange={handleChange} />
                {formState.username.error && <p style={{ color: 'red' }}>{formState.username.error}</p>}
            </div>
            <div>
                <label>Correo Electrónico:</label>
                <input type="email" name="email" value={formState.email.value} onChange={handleChange} />
                {formState.email.error && <p style={{ color: 'red' }}>{formState.email.error}</p>}
            </div>
            <div>
                <label>Contraseña:</label>
                <input type="password" name="password" value={formState.password.value} onChange={handleChange} />
                {formState.password.error && <p style={{ color: 'red' }}>{formState.password.error}</p>}
            </div>
            <button type="submit">Enviar</button>
            <button type="button" onClick={resetFormState}>
                Resetear Formulario
            </button>
        </form>
    )
}

export default MyForm
```

### Desglose del Ejemplo

-   **Implementación de `useFormState`**:

    -   **`useFormState`**: Utiliza el hook `useState` para mantener el estado del formulario (`formState`). Proporciona funciones (`updateFieldValue`, `setFieldError`, `resetFieldState`, `resetFormState`) para actualizar este estado según las interacciones del usuario.

-   **Uso de `useFormState` en un Componente**:

    -   **`MyForm`**: Utiliza `useFormState` para manejar el estado de un formulario de registro de usuario. Implementa funciones para manejar cambios (`handleChange`) y envío (`handleSubmit`) del formulario. También muestra mensajes de error de validación según el estado del campo.

-   **Renderizado del Estado del Formulario**:
    -   El componente `MyForm` muestra campos de entrada para nombre de usuario, correo electrónico y contraseña. Muestra mensajes de error debajo de cada campo si existe un error de validación.

### Consideraciones Adicionales

-   Personaliza el objeto inicial `initialState` de acuerdo con los campos y requisitos específicos de tu formulario.
-   Implementa la lógica de validación necesaria dentro de `handleSubmit` para garantizar que el formulario se envíe correctamente solo cuando todos los campos requeridos estén completos.
-   Asegúrate de manejar adecuadamente las actualizaciones de estado y los mensajes de error según las interacciones del usuario para proporcionar una experiencia de usuario fluida y receptiva.
