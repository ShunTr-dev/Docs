# Preguntas en entrevista de trabajo

## Cuál es el valor de `foo`?

```javascript
var foo = 10 + '20'
```

El valor de `foo` es '1020'. Esto sucede porque al concatenar un número (10) con una cadena ('20'), JavaScript convierte el número en una cadena y las une.

## Cuál será la salida de este código?

```javascript
console.log(0.1 + 0.2 == 0.3)
```

El resultado será `false`. Esto se debe a la precisión limitada en los números de punto flotante en JavaScript, por lo que 0.1 + 0.2 no es exactamente 0.3, sino algo como 0.30000000000000004.

## Cómo harías funcionar este código?

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

## Qué valor devuelve esta sentencia?

```javascript
"i'm a lasagna hog".split('').reverse().join('')
```

El resultado es 'goh angasal a m'i'. La cadena se convierte en un `array` de caracteres con `split('')`, se invierte con `reverse()` y luego se une de nuevo en una cadena con `join('')`.

## Cuál es el valor de `window.foo`?

```javascript
window.foo || (window.foo = 'bar')
```

El valor de `window.foo` será 'bar' si `window.foo` no estaba previamente definido o era `falsy` (como `undefined`, `null`, `0`, etc.). Si ya tenía un valor `truthy`, ese valor no cambiará.

## Cuál es la salida de las dos alertas de abajo?

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

## Cuál es el valo de `foo.length`?

```javascript
var foo = []
foo.push(1)
foo.push(2)
```

El valor de `foo.length` será 2. `push` añade elementos al `array` y aumenta la propiedad `length` en consecuencia.

## Cuál es el valor de `foo.x`?

```javascript
var foo = { n: 1 }
var bar = foo
foo.x = foo = { n: 2 }
```

El valor de `foo.x` es `undefined`. La asignación `foo.x = foo = { n: 2 }` se evalúa de derecha a izquierda. Primero, `foo` se reasigna a `{ n: 2 }`, luego se intenta asignar `foo.x`, pero ahora `foo` ya es el nuevo objeto y no tiene la propiedad x.

## Qué imprime el siguiente código?

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

## Cuál es la diferencia entre estas cuatro preguntas?

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

## Qué sacará por consola este código y por qué?

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

## Considerando las dos funciones de abajo. Devuelven lo mismo? Por qué o por qué no?

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
En `foo2`, el retorno se interrumpe debido a la nueva línea antes de la llave `{`. En JavaScript, un retorno vacío (`return;`) se asume cuando hay un salto de línea después de return. Como resultado, `foo2` devuelve undefined.

### Referencias

[Front-end-Developer-Interview-Questions](https://github.com/h5bp/Front-end-Developer-Interview-Questions/blob/main/src/questions/coding-questions.md)
