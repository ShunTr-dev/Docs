El hook `useLayoutEffect` es similar a `useEffect`, pero se ejecuta de manera sincrónica después de que todas las mutaciones del DOM hayan terminado. Es útil para leer el layout del DOM y sincronizarlo de nuevo.

**Ejemplo:**

```jsx
import React, { useState, useLayoutEffect, useRef } from 'react';

function AnchoCaja() {
  const [width, setWidth] = useState(0);
  const boxRef = useRef(null);

  useLayoutEffect(() => {
    setWidth(boxRef.current.offsetWidth);
  }, []);

  return (
    <div>
      <div ref={boxRef} style={{ width: '50%', height: '100px', backgroundColor: 'lightblue' }} />
      <p>Ancho de la caja: {width}px</p>
    </div>
  );
}

export default AnchoCaja;
```