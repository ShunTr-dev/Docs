# useOptimistic

El hook `useOptimistic` no es una función estándar de React ni una API comúnmente conocida dentro de su ecosistema principal. Sin embargo, puedo guiarte sobre cómo podrías estructurar un hook personalizado llamado `useOptimistic` en React para manejar actualizaciones optimistas en el estado de tu aplicación.

El objetivo de `useOptimistic` en este contexto será proporcionar funciones para realizar actualizaciones optimistas en el estado de tu aplicación, junto con la capacidad de revertir esas actualizaciones si es necesario.

```jsx
import { useState } from 'react'

// Hook personalizado useOptimistic
function useOptimistic(initialState) {
    const [data, setData] = useState(initialState)
    const [optimisticData, setOptimisticData] = useState(null)

    // Función para actualizar los datos de forma optimista
    const updateOptimisticData = (updatedData) => {
        setOptimisticData(updatedData)
    }

    // Función para confirmar los datos optimistas y aplicarlos definitivamente
    const applyOptimisticData = () => {
        setData(optimisticData)
        setOptimisticData(null)
    }

    // Función para revertir los cambios optimistas y restaurar los datos originales
    const revertOptimisticData = () => {
        setOptimisticData(null)
    }

    return {
        data,
        optimisticData,
        updateOptimisticData,
        applyOptimisticData,
        revertOptimisticData,
    }
}

export default useOptimistic
```

### Uso de `useOptimistic`

A continuación, te muestro cómo puedes utilizar `useOptimistic` en un componente funcional de React para manejar actualizaciones optimistas en el estado de los datos.

```jsx
import React from 'react'
import useOptimistic from './useOptimistic' // Asegúrate de importar el hook desde el archivo correcto

function TodoList() {
    const {
        data: todos,
        optimisticData,
        updateOptimisticData,
        applyOptimisticData,
        revertOptimisticData,
    } = useOptimistic([
        { id: 1, text: 'Hacer la compra' },
        { id: 2, text: 'Lavar la ropa' },
        { id: 3, text: 'Pasear al perro' },
    ])

    const handleTodoUpdate = (id, newText) => {
        // Realizar la actualización de manera optimista
        const updatedTodos = todos.map((todo) => {
            if (todo.id === id) {
                return { ...todo, text: newText }
            }
            return todo
        })

        updateOptimisticData(updatedTodos)
    }

    const handleApplyOptimisticData = () => {
        // Aplicar los cambios optimistas de manera definitiva
        applyOptimisticData()
    }

    const handleRevertOptimisticData = () => {
        // Revertir los cambios optimistas
        revertOptimisticData()
    }

    return (
        <div>
            <h2>Lista de Tareas</h2>
            <ul>
                {optimisticData
                    ? optimisticData.map((todo) => (
                          <li key={todo.id}>
                              <input
                                  type="text"
                                  value={todo.text}
                                  onChange={(e) => handleTodoUpdate(todo.id, e.target.value)}
                              />
                          </li>
                      ))
                    : todos.map((todo) => <li key={todo.id}>{todo.text}</li>)}
            </ul>
            {optimisticData && (
                <div>
                    <button onClick={handleApplyOptimisticData}>Guardar Cambios</button>
                    <button onClick={handleRevertOptimisticData}>Cancelar</button>
                </div>
            )}
        </div>
    )
}

export default TodoList
```

### Desglose del Ejemplo

-   **Implementación de `useOptimistic`**:

    -   **`useOptimistic`**: Utiliza el hook `useState` para manejar el estado actual (`data`) y los datos optimistas (`optimisticData`). Proporciona funciones (`updateOptimisticData`, `applyOptimisticData`, `revertOptimisticData`) para realizar y gestionar actualizaciones optimistas en el estado.

-   **Uso de `useOptimistic` en un Componente**:

    -   **`TodoList`**: Utiliza `useOptimistic` para manejar una lista de tareas (`todos`). Implementa funciones (`handleTodoUpdate`, `handleApplyOptimisticData`, `handleRevertOptimisticData`) para realizar actualizaciones optimistas en los datos y manejar la confirmación o reversión de esos cambios.

-   **Renderizado y Manipulación de Datos**:
    -   El componente `TodoList` muestra una lista de tareas, permitiendo editar cada tarea de manera optimista. Muestra botones para confirmar (`Guardar Cambios`) o revertir (`Cancelar`) los cambios optimistas.

### Consideraciones Adicionales

-   Asegúrate de implementar lógica adicional según tus necesidades específicas, como la gestión de errores o la sincronización con una fuente de datos externa.
-   Puedes extender `useOptimistic` con más funciones o parámetros según los requisitos de tu aplicación, como agregar un tiempo de espera antes de confirmar cambios optimistas.
-   El ejemplo proporcionado muestra cómo puedes estructurar un hook personalizado (`useOptimistic`) para manejar actualizaciones optimistas en el estado de tu aplicación React, proporcionando una interfaz clara y reutilizable para gestionar cambios de estado de manera optimista y revertirlos si es necesario.
