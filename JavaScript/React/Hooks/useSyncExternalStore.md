El hook `useSyncExternalStore` se utiliza para suscribirse a un almacenamiento externo sincronizado, asegurando que las actualizaciones son consistentes.

**Ejemplo:**

```jsx
import React, { useSyncExternalStore } from 'react';

const store = {
  subscribe: (callback) => {
    document.addEventListener('click', callback);
    return () => document.removeEventListener('click', callback);
  },
  getSnapshot: () => document.title
};

function TituloDocumento() {
  const title = useSyncExternalStore(store.subscribe, store.getSnapshot);

  return <p>Título del documento: {title}</p>;
}

export default TituloDocumento;
```
