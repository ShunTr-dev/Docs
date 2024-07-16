El hook `useMemo` te permite memorizar valores calculados para optimizar el rendimiento.

**Ejemplo:**

```jsx
import React, { useState, useMemo } from 'react';

function ContadorConCalculo() {
  const [a, setA] = useState(1);
  const [b, setB] = useState(1);

  const resultado = useMemo(() => {
    return a * b;
  }, [a, b]);

  return (
    <div>
      <input value={a} onChange={e => setA(Number(e.target.value))} />
      <input value={b} onChange={e => setB(Number(e.target.value))} />
      <p>Resultado: {resultado}</p>
    </div>
  );
}

export default ContadorConCalculo;
```