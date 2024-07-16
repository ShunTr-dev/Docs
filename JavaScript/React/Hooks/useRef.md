El hook `useRef` te permite crear una referencia mutable que persiste durante todo el ciclo de vida del componente.

**Ejemplo:**

```jsx
import React, { useRef } from 'react';

function EnfocarInput() {
  const inputEl = useRef(null);

  const enfocar = () => {
    inputEl.current.focus();
  };

  return (
    <div>
      <input ref={inputEl} type="text" />
      <button onClick={enfocar}>Enfocar en el input</button>
    </div>
  );
}

export default EnfocarInput;
```