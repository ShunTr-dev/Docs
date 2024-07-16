El hook `useDebugValue` puede ser usado para mostrar información adicional en herramientas de depuración como React DevTools. Es particularmente útil para hooks personalizados.

**Ejemplo:**

```jsx
import React, { useState, useDebugValue } from 'react';

function useContador(initialValue) {
  const [count, setCount] = useState(initialValue);

  useDebugValue(count > 5 ? 'Más de 5' : '5 o menos');

  return [count, setCount];
}

function Contador() {
  const [count, setCount] = useContador(0);

  return (
    <div>
      <p>Contador: {count}</p>
      <button onClick={() => setCount(count + 1)}>Incrementar</button>
    </div>
  );
}

export default Contador;
```