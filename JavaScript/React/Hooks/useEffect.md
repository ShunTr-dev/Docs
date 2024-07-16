El hook `useEffect` te permite realizar efectos secundarios en componentes funcionales, como suscribirse a datos, cambiar el DOM directamente, etc.

**Ejemplo:**

```jsx
import React, { useState, useEffect } from 'react';

function ContadorConEfecto() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `Has hecho clic ${count} veces`;

    return () => {
      // Limpieza si es necesario cuando el componente se desmonta
    };
  }, [count]); // Solo vuelve a ejecutar el efecto si count cambia

  return (
    <div>
      <p>Has hecho clic {count} veces</p>
      <button onClick={() => setCount(count + 1)}>
        Haz clic
      </button>
    </div>
  );
}
export default ContadorConEfecto;
```