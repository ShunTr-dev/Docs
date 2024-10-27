---
title: useFormStatus
date: 2024-07-17 00:00:00 -100
categories: [React, Hooks]
tags: [herramientas]
---

# useFormStatus
Este hook es útil para manejar el estado de validación o estado general de un formulario, permitiendo mostrar mensajes de éxito, error o información mientras se interactúa con los campos del formulario.

### Implementación de `useFormStatus`

El hook `useFormStatus` manejará el estado del formulario y proporcionará funciones para actualizar este estado según las interacciones del usuario.

```jsx
import { useState } from 'react';

// Estados posibles del formulario
const FORM_STATUS = {
  IDLE: 'idle',
  SUBMITTING: 'submitting',
  SUCCESS: 'success',
  ERROR: 'error'
};

// Hook personalizado useFormStatus
function useFormStatus(initialState = FORM_STATUS.IDLE) {
  const [status, setStatus] = useState(initialState);

  // Función para establecer el estado del formulario a "Submitting"
  const setSubmitting = () => {
    setStatus(FORM_STATUS.SUBMITTING);
  };

  // Función para establecer el estado del formulario a "Success"
  const setSuccess = () => {
    setStatus(FORM_STATUS.SUCCESS);
  };

  // Función para establecer el estado del formulario a "Error"
  const setError = () => {
    setStatus(FORM_STATUS.ERROR);
  };

  // Función para establecer el estado del formulario a "Idle"
  const setIdle = () => {
    setStatus(FORM_STATUS.IDLE);
  };

  return {
    status,
    setStatus,
    setSubmitting,
    setSuccess,
    setError,
    setIdle
  };
}

export default useFormStatus;
```

### Uso de `useFormStatus`

Ahora puedes usar `useFormStatus` en cualquier componente funcional de React para manejar y mostrar el estado del formulario según sea necesario.

```jsx
import React from 'react';
import useFormStatus from './useFormStatus'; // Asegúrate de importar el hook desde el archivo correcto

function MyForm() {
  const { status, setSubmitting, setSuccess, setError, setIdle } = useFormStatus();

  const handleSubmit = async (event) => {
    event.preventDefault();
    setSubmitting();

    try {
      // Lógica para enviar el formulario (por ejemplo, una solicitud HTTP)
      await submitForm();
      setSuccess();
    } catch (error) {
      setError();
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <h2>Formulario de Ejemplo</h2>
      {status === 'success' && <p style={{ color: 'green' }}>¡Formulario enviado con éxito!</p>}
      {status === 'error' && <p style={{ color: 'red' }}>Hubo un problema al enviar el formulario.</p>}
      <button type="submit" disabled={status === 'submitting'}>Enviar Formulario</button>
      <button type="button" onClick={setIdle} disabled={status === 'idle'}>Resetear Estado</button>
    </form>
  );
}

export default MyForm;
```

### Desglose del Ejemplo

- **Implementación de `useFormStatus`**:
  - **`FORM_STATUS`**: Define constantes que representan los estados posibles del formulario (`idle`, `submitting`, `success`, `error`).
  - **`useFormStatus`**: Utiliza el hook `useState` para mantener el estado del formulario. Proporciona funciones (`setSubmitting`, `setSuccess`, `setError`, `setIdle`) para actualizar este estado según las interacciones del usuario.

- **Uso de `useFormStatus` en un Componente**:
  - **`MyForm`**: Utiliza `useFormStatus` para manejar el estado del formulario. Implementa un manejo de envío (`handleSubmit`) que establece el estado a `submitting` al enviar el formulario, y luego cambia el estado a `success` o `error` según el resultado.

- **Renderizado del Estado del Formulario**:
  - El componente `MyForm` muestra mensajes de éxito o error según el estado actual del formulario (`status`). También incluye botones para enviar el formulario y resetear el estado.

### Consideraciones Adicionales

- Puedes personalizar los estados del formulario (`FORM_STATUS`) según las necesidades específicas de tu aplicación.
- Asegúrate de manejar las transiciones de estado de manera adecuada dentro de tu lógica de negocio o de envío de formularios.

Este enfoque te proporciona una manera flexible y controlada de manejar el estado de los formularios en tus aplicaciones React, lo cual es esencial para proporcionar retroalimentación adecuada al usuario y mejorar la experiencia general de uso.