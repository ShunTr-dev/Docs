El hook `useId` genera identificadores únicos que pueden ser usados para atributos `id` en elementos del DOM.

**Ejemplo:**

```jsx
import React, { useId } from 'react';

function Formulario() {
  const id = useId();

  return (
    <div>
      <label htmlFor={id}>Nombre:</label>
      <input id={id} type="text" />
    </div>
  );
}

export default Formulario;
```
