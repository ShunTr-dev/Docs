El hook `useImperativeHandle` te permite personalizar la instancia del objeto que se expone cuando se usa `ref` en un componente funcional.

**Ejemplo:**

```jsx
import React, { useRef, useImperativeHandle, forwardRef } from 'react';

const Input = forwardRef((props, ref) => {
  const inputRef = useRef();

  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    },
    clear: () => {
      inputRef.current.value = '';
    }
  }));

  return <input ref={inputRef} />;
});

function Padre() {
  const inputRef = useRef();

  return (
    <div>
      <Input ref={inputRef} />
      <button onClick={() => inputRef.current.focus()}>Enfocar</button>
      <button onClick={() => inputRef.current.clear()}>Limpiar</button>
    </div>
  );
}

export default Padre;
```