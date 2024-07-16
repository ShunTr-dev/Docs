El hook `useState` te permite añadir el estado de React a un componente funcional.

**Ejemplo:**

```jsx
import React, { useState } from 'react';

function Contador() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Has hecho clic {count} veces</p>
      <button onClick={() => setCount(count + 1)}>
        Haz clic
      </button>
    </div>
  );
}

export default Contador;
```