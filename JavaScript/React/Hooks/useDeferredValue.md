El hook `useDeferredValue` permite diferir el valor que se está renderizando para mejorar el rendimiento en componentes que realizan renderizados costosos.

**Ejemplo:**

```jsx
import React, { useState, useDeferredValue } from 'react';

function App() {
  const [value, setValue] = useState('');
  const deferredValue = useDeferredValue(value);

  return (
    <div>
      <input value={value} onChange={e => setValue(e.target.value)} />
      <ExpensiveComponent value={deferredValue} />
    </div>
  );
}

function ExpensiveComponent({ value }) {
  const items = Array.from({ length: 10000 }, (_, i) => <div key={i}>{value}</div>);
  return <div>{items}</div>;
}

export default App;
```