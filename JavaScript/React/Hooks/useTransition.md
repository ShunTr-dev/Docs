El hook `useTransition` permite definir una transición para las actualizaciones de estado, lo que puede mejorar el rendimiento en interfaces de usuario complejas.

**Ejemplo:**

```jsx
import React, { useState, useTransition } from 'react';

function ListaFiltrada() {
  const [query, setQuery] = useState('');
  const [isPending, startTransition] = useTransition();

  const handleChange = (e) => {
    startTransition(() => {
      setQuery(e.target.value);
    });
  };

  const filteredItems = items.filter(item => item.includes(query));

  return (
    <div>
      <input type="text" onChange={handleChange} />
      {isPending && <div>Cargando...</div>}
      <ul>
        {filteredItems.map(item => <li key={item}>{item}</li>)}
      </ul>
    </div>
  );
}

const items = ['React', 'Vue', 'Angular', 'Svelte', 'Ember'];

export default ListaFiltrada;
```