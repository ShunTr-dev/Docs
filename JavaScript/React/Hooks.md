# Hooks
Un hook es una función especial que permite a los desarrolladores "engancharse" a las características de React (como el estado y el ciclo de vida de los componentes) desde componentes funcionales. Antes de los hooks, las características como el estado y el ciclo de vida solo estaban disponibles en componentes de clase. Con la introducción de los hooks en React 16.8, estas características ahora también están disponibles en componentes funcionales, lo que permite una forma más simple y concisa de escribir componentes React.

### Características de los Hooks

1. **Funciones**: Los hooks son simplemente funciones de JavaScript.
2. **No se usan en clases**: Los hooks solo funcionan en componentes funcionales, no en clases.
3. **Empiezan con "use"**: Todos los hooks tienen el prefijo "use" (ej. `useState`, `useEffect`) para seguir las convenciones de React y facilitar su búsqueda en el código.
4. **Llamados en la raíz del componente**: Deben ser llamados en el nivel superior de un componente funcional, no dentro de bucles, condiciones o funciones anidadas, para asegurar que el orden de los hooks sea el mismo en cada renderizado.

### ¿Por qué usar Hooks?

- **Reutilización de lógica de estado**: Los hooks permiten reutilizar la lógica de estado entre diferentes componentes de una manera más limpia y compartible sin necesidad de usar componentes de orden superior (HOC) o render props.
- **Simplificación de componentes**: Los hooks hacen que los componentes sean más fáciles de entender y mantener al reducir la necesidad de clases.
- **Mejor manejo del ciclo de vida**: Permiten manejar los efectos secundarios y el ciclo de vida de los componentes de una manera más granular y controlada.

### Clasificación

#### Manejo del estado
- [useState](https://github.com/ShunTr-dev/Docs/tree/main/JavaScript/React/Hooks/useState.md)
- [useReducer](https://github.com/ShunTr-dev/Docs/tree/main/JavaScript/React/Hooks/useReducer.md)
- [useSyncExternalStore](https://github.com/ShunTr-dev/Docs/tree/main/JavaScript/React/Hooks/useSyncExternalStore.md)

#### Referencias
- [useRef](https://github.com/ShunTr-dev/Docs/tree/main/JavaScript/React/Hooks/useRef.md)
- [useImperativeHandle](https://github.com/ShunTr-dev/Docs/tree/main/JavaScript/React/Hooks/useImperativeHandle.md)

#### Efectos
- [useEffect](https://github.com/ShunTr-dev/Docs/tree/main/JavaScript/React/Hooks/useEffect.md)
- [useLayoutEffect](https://github.com/ShunTr-dev/Docs/tree/main/JavaScript/React/Hooks/useLayoutEffect.md)
- [useInsertionEffect](https://github.com/ShunTr-dev/Docs/tree/main/JavaScript/React/Hooks/useInsertionEffect.md)

#### Contexto
- [useContext](https://github.com/ShunTr-dev/Docs/tree/main/JavaScript/React/Hooks/useContext.md)

#### Transición
- [useTransition](https://github.com/ShunTr-dev/Docs/tree/main/JavaScript/React/Hooks/useTransition.md)
- [useDeferredValue](https://github.com/ShunTr-dev/Docs/tree/main/JavaScript/React/Hooks/useDeferredValue.md)

#### Rendimiento
- [useMemo](https://github.com/ShunTr-dev/Docs/tree/main/JavaScript/React/Hooks/useMemo.md)
- [useCallback](https://github.com/ShunTr-dev/Docs/tree/main/JavaScript/React/Hooks/useCallback.md)

#### Utilidad
- [useDebugValue](https://github.com/ShunTr-dev/Docs/tree/main/JavaScript/React/Hooks/useDebugValue.md)
- [useId](https://github.com/ShunTr-dev/Docs/tree/main/JavaScript/React/Hooks/useId.md)

#### React 19
- [useFormStatus](https://github.com/ShunTr-dev/Docs/tree/main/JavaScript/React/Hooks/useFormStatus.md)
- [useFormState](https://github.com/ShunTr-dev/Docs/tree/main/JavaScript/React/Hooks/useFormState.md)
- [useOptimistic](https://github.com/ShunTr-dev/Docs/tree/main/JavaScript/React/Hooks/useOptimistic.md)
- [use](https://github.com/ShunTr-dev/Docs/tree/main/JavaScript/React/Hooks/use.md)
