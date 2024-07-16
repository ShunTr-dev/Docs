El hook `useContext` te permite suscribirte a un contexto de React y usarlo en tus componentes funcionales.

**Ejemplo:**

```jsx
import React, { useContext } from 'react';

const TemaContext = React.createContext('light');

function Boton() {
  const tema = useContext(TemaContext);

  return (
    <button style={{ background: tema === 'dark' ? '#333' : '#FFF', color: tema === 'dark' ? '#FFF' : '#000' }}>
      {tema === 'dark' ? 'Modo Oscuro' : 'Modo Claro'}
    </button>
  );
}

function App() {
  return (
    <TemaContext.Provider value="dark">
      <Boton />
    </TemaContext.Provider>
  );
}

export default App;
```