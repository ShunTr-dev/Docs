El hook `useCallback` te permite memorizar funciones, útil para optimizar componentes hijos que dependen de funciones que se pasan como props.

**Ejemplo:**

```jsx
import React, { useState, useCallback } from 'react';

function Hijo({ incrementar }) {
  return <button onClick={incrementar}>Incrementar</button>;
}

function Padre() {
  const [count, setCount] = useState(0);

  const incrementar = useCallback(() => {
    setCount(c => c + 1);
  }, []);

  return (
    <div>
      <p>Contador: {count}</p>
      <Hijo incrementar={incrementar} />
    </div>
  );
}

export default Padre;
```