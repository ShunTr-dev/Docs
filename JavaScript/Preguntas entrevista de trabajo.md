# Preguntas en entrevista de trabajo

### 1. Explica la delegación de eventos.

La delegación de eventos es una técnica en JavaScript en la que asignas un evento a un elemento padre en lugar de asignarlo a cada uno de los elementos hijos individuales. Esto funciona debido a la propagación de eventos (`event bubbling`). En lugar de agregar un manejador de eventos a cada elemento hijo, se asigna a un ancestro común. El evento se propaga desde el elemento hijo al padre y se puede detectar cuál fue el origen del evento usando `event.target`.

**Ejemplo:**

```javascript
document.getElementById('parent').addEventListener('click', function (event) {
    if (event.target.matches('.child')) {
        console.log('Clicked a child element')
    }
})
```

### 2. Explica cómo funciona `this` en JavaScript.

En JavaScript, `this` se refiere al objeto desde el cual se invoca una función. Su valor cambia dependiendo de cómo y dónde se utiliza. En una función global, `this` apunta a `window` (en navegadores). En el contexto de un método de objeto, `this` apunta al objeto en sí.

**Cambios en ES6:** Con las funciones flecha (`=>`), `this` se determina léxicamente, es decir, toma el valor de `this` del contexto en el que se define, no del contexto en el que se ejecuta.

**Ejemplo:**

```javascript
function Person() {
    this.name = 'John'
    setTimeout(() => {
        console.log(this.name) // "John", ya que `this` se refiere al objeto `Person`.
    }, 1000)
}
```

### 3. Explica cómo funciona la herencia prototipal.

La herencia prototipal es un mecanismo en JavaScript mediante el cual los objetos pueden "heredar" propiedades y métodos de otros objetos. Cada objeto tiene una propiedad interna `[[Prototype]]`, que apunta a otro objeto, y de este se heredan las propiedades y métodos.

**Ejemplo:**

```javascript
function Animal(name) {
    this.name = name
}

Animal.prototype.speak = function () {
    console.log(`${this.name} makes a noise`)
}

const dog = new Animal('Dog')
dog.speak() // "Dog makes a noise"
```

### 4. ¿Cuál es la diferencia entre `null`, `undefined` y `undeclared`?

-   **`null`:** Representa la ausencia intencional de un valor.
-   **`undefined`:** Significa que una variable ha sido declarada pero no se le ha asignado valor.
-   **`undeclared`:** Una variable que nunca ha sido declarada en el entorno actual.

**Cómo comprobarlos:**

-   `typeof variable === 'undefined'` para `undefined`.
-   `variable === null` para `null`.
-   Intentar acceder a una variable no declarada dará un error de referencia.

### 5. ¿Qué es un closure y cómo/por qué usarías uno?

Un closure es una función que recuerda su entorno léxico, es decir, las variables que estaban en su alcance al momento de ser definida. Los closures permiten crear funciones con datos privados, mantener un estado, o crear funciones más flexibles.

**Ejemplo:**

```javascript
function outer() {
    let count = 0
    return function inner() {
        count++
        console.log(count)
    }
}

const counter = outer()
counter() // 1
counter() // 2
```

### 6. ¿Qué construcciones de lenguaje utilizas para iterar sobre propiedades de un objeto y elementos de un array?

-   **Objetos:** `for...in` o `Object.keys()`, `Object.values()`, `Object.entries()`.
-   **Arrays:** `for`, `for...of`, `forEach`, `map`, `filter`, `reduce`.

### 7. ¿Cuál es la diferencia principal entre los métodos `Array.forEach()` y `Array.map()`?

-   **`forEach`:** Itera sobre cada elemento pero no devuelve nada. Se usa para efectos secundarios.
-   **`map`:** Itera y retorna un nuevo array con los resultados. Se usa para transformar datos.

**Otros métodos populares:** `filter`, `reduce`, `some`, `every`.

### 8. ¿Cuál es un caso típico para funciones anónimas?

Las funciones anónimas son útiles cuando se pasan como callbacks, por ejemplo, en eventos, en `setTimeout`, o en métodos como `map` y `filter`.

### 9. ¿Cuál es la diferencia entre objetos de host y objetos nativos?

-   **Objetos de host:** Proporcionados por el entorno (navegador, Node.js), como `window`, `document`.
-   **Objetos nativos:** Parte del lenguaje JavaScript, como `Array`, `Object`.

### 10. Explica la diferencia entre `function Person(){}`, `var person = Person()`, y `var person = new Person()`:

-   **`function Person(){}`:** Declara una función.
-   **`var person = Person()`:** Llama a la función sin crear un nuevo objeto.
-   **`var person = new Person()`:** Crea una instancia de `Person` con su propio contexto `this`.

### 11. Explica las diferencias en el uso de `foo` entre `function foo() {}` y `var foo = function() {}`:

-   **`function foo() {}`:** Declaración de función, disponible en todo el contexto debido al hoisting.
-   **`var foo = function() {}`:** Expresión de función, no está disponible antes de su declaración.

### 12. ¿Puedes explicar qué hacen `Function.call` y `Function.apply`? ¿Cuál es la diferencia notable?

Ambos métodos invocan una función con un valor de `this` específico. La diferencia está en cómo se pasan los argumentos:

-   **`call`:** Los argumentos se pasan individualmente.
-   **`apply`:** Los argumentos se pasan como un array.

### 13. Explica `Function.prototype.bind`.

`bind` crea una nueva función que, cuando es llamada, tiene un valor específico de `this`, y opcionalmente argumentos iniciales predefinidos.

### 14. ¿Cuál es la diferencia entre detección de características, inferencia de características y usar la cadena UA?

-   **Detección de características:** Comprobar si una característica está disponible antes de usarla.
-   **Inferencia de características:** Asumir que si una característica existe, otras relacionadas también estarán presentes.
-   **Cadena UA:** Identificación basada en el User-Agent, menos confiable debido a la manipulación por parte de los navegadores.

### 15. Explica "hoisting".

El hoisting es el comportamiento donde las declaraciones de variables y funciones se mueven al principio de su contexto durante la fase de compilación. Solo las declaraciones se levantan, no las asignaciones.

### 16. ¿Qué es la coerción de tipos? ¿Cuáles son los problemas comunes al confiar en ella?

La coerción de tipos es la conversión automática entre tipos. Los problemas comunes incluyen resultados inesperados cuando se combinan tipos como `"" + 1`, que produce `"1"`, o `0 == false`, que evalúa como `true`.

### 17. Describe la propagación de eventos (event bubbling).

En la propagación de eventos, un evento se origina en un elemento y se propaga hacia arriba a través de los ancestros en el DOM.

### 18. Describe la captura de eventos (event capturing).

En la captura de eventos, el evento se propaga desde la raíz del documento hacia el objetivo del evento antes de disparar el manejador.

### 19. ¿Cuál es la diferencia entre un "atributo" y una "propiedad"?

Un atributo es lo que está en el HTML y una propiedad es lo que se maneja en el DOM con JavaScript. Los valores de los atributos pueden sincronizarse con propiedades y viceversa.

### 20. ¿Cuáles son los pros y contras de extender objetos JavaScript integrados?

-   **Pros:** Puedes agregar funcionalidades útiles a objetos existentes.
-   **Contras:** Puede causar conflictos si otras bibliotecas o el propio JavaScript hacen lo mismo.

### 21. ¿Cuál es la diferencia entre `==` y `===`?

-   **`==`:** Realiza coerción de tipos antes de la comparación.
-   **`===`:** Compara estrictamente sin coerción de tipos.

### 22. Explica la política de mismo origen con respecto a JavaScript.

La política de mismo origen previene que scripts en diferentes orígenes accedan a recursos de otros, protegiendo contra ataques como cross-site scripting (XSS).

### 23. ¿Por qué se llama operador ternario? ¿Qué indica la palabra "ternario"?

Se llama así porque opera con tres operandos: una condición, una expresión si es verdadera y otra si es falsa. La palabra "ternario" indica tres partes.

### 24. ¿Qué es el modo estricto? ¿Cuáles son las ventajas/desventajas de usarlo?

El modo estricto (`"use strict";`) introduce una versión más estricta de JavaScript, eliminando malas prácticas y errores silenciosos. Sin embargo, puede romper código más antiguo.

### 25. ¿Cuáles son las ventajas/desventajas de escribir código JavaScript en un lenguaje que se compila a JavaScript?

-   **Ventajas:** Mejora la sintaxis, nuevas características.
-   **Desventajas:** Requiere un paso de compilación, puede hacer más difícil la depuración.

### 26. ¿Qué herramientas y técnicas usas para depurar código JavaScript?

Uso `console.log`, breakpoints en DevTools, y herramientas como `debugger`.

### 27. Explica la diferencia entre objetos mutables e inmutables.

-   **Mutables:** Pueden cambiar su estado (ej. objetos).
-   **Inmutables:** No pueden cambiar después de ser creados (ej. números, cadenas).

**Ejemplo de objeto inmutable:** `Object.freeze({})`.

### 28. Explica la diferencia entre funciones síncronas y asíncronas.

Las funciones síncronas se ejecutan secuencialmente, bloqueando la ejecución. Las funciones asíncronas permiten realizar otras tareas mientras se espera una operación (como una solicitud a un servidor).

### 29. ¿Qué es el event loop?

El event loop es un mecanismo que permite que JavaScript maneje operaciones asíncronas, verificando la cola de tareas y ejecutando callbacks cuando el call stack está vacío.

### 30. ¿Cuáles son las diferencias entre variables creadas con `let`, `var` o `const`?

-   **`var`:** Alcance de función, puede ser redeclarada.
-   **`let`:** Alcance de bloque, no puede ser redeclarada.
-   **`const`:** Igual que `let`, pero no permite reasignación (aunque las propiedades internas pueden cambiar).

**Cambiar propiedades de un objeto `const`:**
Puedes cambiar las propiedades de un objeto definido con `const`, pero no reasignar el objeto completo.

### 31. ¿Cuáles son las diferencias entre clases ES6 y constructores de funciones ES5?

Las clases ES6 proporcionan una sintaxis más limpia y un mecanismo interno para herencia, mientras que las funciones constructoras requieren prototipos manuales para heredar.

### 32. ¿Puedes ofrecer un caso de uso para la nueva sintaxis de función flecha (`=>`)?

Las funciones flecha son útiles para mantener el contexto léxico de `this`, especialmente en callbacks.

### 33. ¿Cuál es la definición de una función de orden superior?

Una función de orden superior es una función que acepta otras funciones como argumentos o retorna una función.

### 34. ¿Puedes dar un ejemplo de desestructuración de un objeto o array?

**Ejemplo de objeto:**

```javascript
const { name, age } = person
```

**Ejemplo de array:**

```javascript
const [first, second] = [1, 2, 3]
```

### 35. ¿Puedes dar un ejemplo de generar una cadena con literales de plantilla ES6?

```javascript
const name = 'John'
const greeting = `Hello, ${name}!`
```

### 36. ¿Puedes dar un ejemplo de una función curry y por qué esta sintaxis ofrece una ventaja?

El currying convierte una función que toma múltiples argumentos en una función que los toma de uno en uno:

```javascript
const add = (x) => (y) => x + y
console.log(add(2)(3)) // 5
```

### 37. ¿Cuáles son los beneficios de usar la sintaxis de propagación y cómo es diferente de la sintaxis de resto?

-   **Propagación (`...`):** Expande un array u objeto.
-   **Resto (`...`):** Recoge argumentos en un array.

**Ejemplo de propagación:**

```javascript
const arr = [1, 2, 3]
console.log([...arr, 4, 5]) // [1, 2, 3, 4, 5]
```

### 38. ¿Cómo puedes compartir código entre archivos?

Puedes usar `export` y `import` en ES6 para compartir módulos.

### 39. ¿Por qué querrías crear miembros de clase estáticos?

Los miembros estáticos pertenecen a la clase en sí, no a instancias. Son útiles para métodos auxiliares.

### 40. ¿Cuál es la diferencia entre los bucles `while` y `do-while`?

-   **`while`:** Evalúa la condición antes de ejecutar el bloque.
-   **`do-while`:** Ejecuta el bloque al menos una vez antes de evaluar la condición.

### 41. ¿Qué es una promesa? ¿Dónde y cómo usarías una promesa?

Una promesa representa la eventual resolución o rechazo de una operación asíncrona. Se usan en operaciones como solicitudes de red.

### 42. Discute cómo usarías principios de Programación Orientada a Objetos en JavaScript.

Puedes usar clases y prototipos para crear objetos con herencia y encapsulación.

### 43. ¿Cuál es la diferencia entre `event.target` y `event.currentTarget`?

-   **`event.target`:** El elemento real donde ocurrió el evento.
-   **`event.currentTarget`:** El elemento al que se le asignó el manejador de eventos.

### 44. ¿Cuál es la diferencia entre `event.preventDefault()` y `event.stopPropagation()`?

-   **`preventDefault`:** Previene la acción por defecto del evento.
-   **`stopPropagation`:** Detiene la propagación del evento en el DOM.

### Preguntas de código:

1. **Haz que esto funcione:**

```javascript
function duplicate(arr) {
    return arr.concat(arr)
}

console.log(duplicate([1, 2, 3, 4, 5])) // [1, 2, 3, 4, 5, 1, 2, 3, 4, 5]
```

2. **Crear un bucle que itere hasta 100 con "fizz", "buzz", y "fizzbuzz":**

```javascript
for (let i = 1; i <= 100; i++) {
    if (i % 15 === 0) console.log('fizzbuzz')
    else if (i % 3 === 0) console.log('fizz')
    else if (i % 5 === 0) console.log('buzz')
    else console.log(i)
}
```

3. **¿Qué se devolverá en cada uno de estos?**

```javascript
console.log('hello' || 'world') // "hello"
console.log('foo' && 'bar') // "bar"
```

4. **Escribe una IIFE (Immediately Invoked Function Expression):**

```javascript
;(function () {
    console.log('IIFE executed')
})()
```

5. **Cuál es el valor de `foo`?**

```javascript
var foo = 10 + '20'
```

El valor de `foo` es '1020'. Esto sucede porque al concatenar un número (10) con una cadena ('20'), JavaScript convierte el número en una cadena y las une.

6. **Cuál será la salida de este código?**

```javascript
console.log(0.1 + 0.2 == 0.3)
```

El resultado será `false`. Esto se debe a la precisión limitada en los números de punto flotante en JavaScript, por lo que 0.1 + 0.2 no es exactamente 0.3, sino algo como 0.30000000000000004.

5. **Cómo harías funcionar este código?**

```javascript
add(2, 5) // 7
add(2)(5) // 7
```

Puedes lograr esto definiendo add de la siguiente manera:

```javascript
function add(x, y) {
    if (y !== undefined) return x + y
    return function (y) {
        return x + y
    }
}
```

Esta función acepta dos argumentos: si se proporcionan ambos de inmediato, suma los números. Si solo se proporciona uno, devuelve una función que espera el segundo argumento.

6. **Qué valor devuelve esta sentencia?**

```javascript
"i'm a lasagna hog".split('').reverse().join('')
```

El resultado es 'goh angasal a m'i'. La cadena se convierte en un `array` de caracteres con `split('')`, se invierte con `reverse()` y luego se une de nuevo en una cadena con `join('')`.

7. **Cuál es el valor de `window.foo`?**

```javascript
window.foo || (window.foo = 'bar')
```

El valor de `window.foo` será 'bar' si `window.foo` no estaba previamente definido o era `falsy` (como `undefined`, `null`, `0`, etc.). Si ya tenía un valor `truthy`, ese valor no cambiará.

8. **Cuál es la salida de las dos alertas de abajo?**

```javascript
var foo = 'Hello'
;(function () {
    var bar = ' World'
    alert(foo + bar)
})()
alert(foo + bar)
```

-   El primer `alert` mostrará 'Hello World'.
-   El segundo `alert` generará un error de referencia, ya que `bar` está definido solo dentro de la función y no está disponible fuera de ella.

9. **Cuál es el valo de `foo.length`?**

```javascript
var foo = []
foo.push(1)
foo.push(2)
```

El valor de `foo.length` será 2. `push` añade elementos al `array` y aumenta la propiedad `length` en consecuencia.

10. **Cuál es el valor de `foo.x`?**

```javascript
var foo = { n: 1 }
var bar = foo
foo.x = foo = { n: 2 }
```

El valor de `foo.x` es `undefined`. La asignación `foo.x = foo = { n: 2 }` se evalúa de derecha a izquierda. Primero, `foo` se reasigna a `{ n: 2 }`, luego se intenta asignar `foo.x`, pero ahora `foo` ya es el nuevo objeto y no tiene la propiedad x.

11. **Qué imprime el siguiente código?**

```javascript
console.log('one')
setTimeout(function () {
    console.log('two')
}, 0)
Promise.resolve().then(function () {
    console.log('three')
})
console.log('four')
```

El orden de la salida es:

-   one
-   four
-   three
-   two

Esto se debe al orden de la ejecución en el event loop de JavaScript:

-   `console.log('one')` se ejecuta primero.
-   `setTimeout` se coloca en la cola de tareas.
-   La promesa se resuelve y su `then` se ejecuta antes que el temporizador.
-   Finalmente, se ejecuta la función dentro de `setTimeout`.

12. **Cuál es la diferencia entre estas cuatro funciones?**

```javascript
doSomething().then(function () {
    return doSomethingElse()
})

doSomething().then(function () {
    doSomethingElse()
})

doSomething().then(doSomethingElse())

doSomething().then(doSomethingElse)
```

-   Primera promesa: La primera devuelve explícitamente el valor de doSomethingElse(), encadenando la promesa.
-   Segunda promesa: Ejecuta `doSomethingElse()`, pero no retorna nada, por lo que la promesa no se encadena.
-   Tercera promesa: Ejecuta `doSomethingElse()` inmediatamente debido a los paréntesis, lo cual no es el comportamiento deseado.
-   Cuarta promesa: Pasa `doSomethingElse` como una función callback, lo que permite que se ejecute correctamente cuando se resuelve la primera promesa.

13. **Qué sacará por consola este código y por qué?**

```javascript
;(function () {
    var a = (b = 3)
})()

console.log('a defined? ' + (typeof a !== 'undefined'))
console.log('b defined? ' + (typeof b !== 'undefined'))
```

-   a defined? false
-   b defined? true

Esto ocurre porque `b = 3` dentro de la función no usa `var`, `let` o `const`, lo que hace que `b` se convierta en una variable global (anexada a `window` en navegadores), mientras que a está limitada al ámbito de la función.

14. **Considerando las dos funciones de abajo. Devuelven lo mismo? Por qué o por qué no?**

```javascript
function foo1() {
    return {
        bar: 'hello',
    }
}

function foo2() {
    return
    {
        bar: 'hello'
    }
}
```

No, no devolverán lo mismo.
En `foo2`, el retorno se interrumpe debido a la nueva línea antes de la llave `{`. En JavaScript, un retorno vacío (`return;`) se asume cuando hay un salto de línea después de return. Como resultado, `foo2` devuelve `undefined`.

### Referencias

[Front-end-Developer-Interview-Questions](https://github.com/h5bp/Front-end-Developer-Interview-Questions/blob/main/src/questions/coding-questions.md)
[Front-end-Developer-Interview-Questions](https://github.com/h5bp/Front-end-Developer-Interview-Questions/blob/main/src/questions/javascript-questions.md)
