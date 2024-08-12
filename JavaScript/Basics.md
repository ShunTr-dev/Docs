# JavaScript

El nombre oficial del estándar [JavaScript](https://es.wikipedia.org/wiki/JavaScript) es [ECMAScript](https://es.wikipedia.org/wiki/ECMAScript).

Hoy en día, la forma más popular de realizar la [transpilación](https://es.wikipedia.org/wiki/Transpilador) es mediante `Babel`. La [transpilación](https://es.wikipedia.org/wiki/Transpilador) se configura automáticamente en las aplicaciones de React creadas con Vite.

[Node.js](https://nodejs.org/en) es un entorno de ejecución de JavaScript basado en el motor de JavaScript Chrome V8 de Google y funciona prácticamente en cualquier lugar, desde servidores hasta teléfonos móviles. El código se escribe en archivos que terminan en .js que se ejecutan emitiendo el `comando node nombre_del_archivo.js`.

También es posible escribir código JavaScript en la consola de Node.js, que se abre escribiendo node en la línea de comandos, así como en la consola de herramientas de desarrollo del navegador. Las revisiones más recientes de Chrome manejan las características más nuevas de JavaScript bastante bien sin transpilar el código. Alternativamente, puedes utilizar una herramienta como JS Bin.

JavaScript recuerda, tanto en nombre como en sintaxis, a Java. Pero cuando se trata del mecanismo central del lenguaje, no podrían ser más diferentes. Viniendo de un entorno de Java, el comportamiento de JavaScript puede parecer un poco extraño, especialmente si uno no hace el esfuerzo de buscar sus características.

## [Variables](<https://es.wikipedia.org/wiki/Variable_(programaci%C3%B3n)>)

En JavaScript, hay algunas formas de definir las [variables](<https://es.wikipedia.org/wiki/Variable_(programaci%C3%B3n)>):

```js
const x = 1
let y = 5

console.log(x, y) // se imprime 1, 5
y += 10
console.log(x, y) // se imprime 1, 15
y = 'sometext'
console.log(x, y) // se imprime 1, sometext
x = 4 // provoca un error
```

`const` no define realmente una variable sino una constante para la cual el valor ya no se puede cambiar. Por otra parte `let` define una variable normal.
También vemos que el tipo de datos asignados a la variable puede cambiar durante la ejecución. Al principio y almacena un número entero y al final un string.

También es posible definir variables en JavaScript usando la palabra clave `var`. `var` fue, durante mucho tiempo, la única forma de definir variables. `const` y `let` se agregaron recientemente en la versión ES6. En situaciones específicas, `var` funciona de una manera diferente comparada con las definiciones de variables de la mayoría de los lenguajes.

-   [var, let y const - Qué, por qué y cómo](https://www.youtube.com/watch?v=sjyJBL5fkp8)

## [Arrays](<https://es.wikipedia.org/wiki/Vector_(inform%C3%A1tica)>)

Un [array](<https://es.wikipedia.org/wiki/Vector_(inform%C3%A1tica)>) y un par de ejemplos de su uso:

```js
const t = [1, -1, 3]

t.push(5)

console.log(t.length) // se imprime 4
console.log(t[1]) // se imprime -1

t.forEach((value) => {
    console.log(value) // se imprimen los números 1, -1, 3, 5 cada uno en su propia línea
})
```

Cabe destacar el hecho de que el contenido de el array se puede modificar aunque esté definido como const. Como el array es un objeto, la variable siempre apunta al mismo objeto. Sin embargo, el contenido del array cambia a medida que se le agregan nuevos elementos.

Una forma de iterar a través de los elementos del array es usar forEach como se ve en el ejemplo. forEach recibe una función definida usando la sintaxis de flecha como parámetro.

```js
;(value) => {
    console.log(value)
}
```

`forEach` llama a la función para cada uno de los elementos del array, siempre pasando el elemento individual como parámetro. La función como parámetro de forEach también puede recibir otros parámetros.

En el ejemplo anterior, se agregó un nuevo elemento al array usando el método `push`. Cuando se usa [React](https://es.wikipedia.org/wiki/React), a menudo se usan técnicas de programación funcional. Una característica del paradigma de [programación funcional](https://es.wikipedia.org/wiki/Programaci%C3%B3n_funcional) es el uso de estructuras de datos inmutables. En el código de React, es preferible usar el método concat, que no agrega el elemento al array, pero crea un nuevo array en la que se incluyen el contenido del array anterior y el nuevo elemento.

```js
const t = [1, -1, 3]

const t2 = t.concat(5) // crea un nuevo array

console.log(t) // se imprime [1, -1, 3]
console.log(t2) // se imprime [1, -1, 3, 5]
```

La llamada al método `t.concat(5)` no agrega un nuevo elemento al array anterior, pero devuelve un nuevo array que, además de contener los elementos del array anterior, también contiene el elemento nuevo.

Hay muchos métodos útiles definidos para arrays. Veamos un breve ejemplo del uso del método `map`.

```js
const t = [1, 2, 3]

const m1 = t.map((value) => value * 2)
console.log(m1) // se imprime [2, 4, 6]
```

Basado en el array anterior, `map` crea un nuevo array, para el cual la función dada como parámetro se usa para crear los elementos. En el caso de este ejemplo, el valor original se multiplica por dos.

`Map` también puede transformar el array en algo completamente diferente:

```js
const m2 = t.map((value) => '<li>' + value + '</li>')
console.log(m2)
// se imprime [ '<li>1</li>', '<li>2</li>', '<li>3</li>' ]
```

Aquí un array lleno de valores enteros se transforma en un array que contiene strings de HTML utilizando el método `map`.

Los elementos individuales de un array son fáciles de asignar a variables con la ayuda de la asignación de desestructuración.

```js
const t = [1, 2, 3, 4, 5]

const [first, second, ...rest] = t

console.log(first, second) // se imprime 1, 2
console.log(rest) // se imprime [3, 4 ,5]
```

Gracias a la asignación, las variables `first` y `second` recibirán los dos primeros enteros del array como sus valores. Los enteros restantes se "recopilan" en un array propio que luego se asigna a la variable `rest`.

## [Objetos](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>)

Hay algunas formas diferentes de definir [objetos](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) en JavaScript. Un método muy común es usar objetos literales, que sucede al enumerar sus propiedades entre llaves:

```js
const object1 = {
    name: 'Arto Hellas',
    age: 35,
    education: 'PhD',
}

const object2 = {
    name: 'Full Stack web application development',
    level: 'intermediate studies',
    size: 5,
}

const object3 = {
    name: {
        first: 'Dan',
        last: 'Abramov',
    },
    grades: [2, 3, 5, 3],
    department: 'Stanford University',
}
```

Los valores de las propiedades pueden ser de cualquier tipo, como `enteros`, `strings`, `arrays`, `objetos`...

Se hace referencia a las propiedades de un objeto usando la notación "de punto", o usando corchetes:

```js
console.log(object1.name) // se imprime Arto Hellas
const fieldName = 'age'
console.log(object1[fieldName]) // se imprime 35
```

También puedes agregar propiedades a un objeto sobre la marcha usando notación de puntos o corchetes:

```js
object1.address = 'Helsinki'
object1['secret number'] = 12341
```

La última de las adiciones debe hacerse usando corchetes, porque cuando se usa la notación de puntos, secret number no es un nombre de propiedad válido debido al carácter de espacio.

Naturalmente, los objetos en JavaScript también pueden tener [métodos](<https://es.wikipedia.org/wiki/M%C3%A9todo_(inform%C3%A1tica)>).

Los objetos también se pueden definir usando las llamadas funciones de constructor, lo que da como resultado un mecanismo que recuerda a muchos otros lenguajes de programación, por ejemplo, las clases de Java. A pesar de esta similitud, JavaScript no tiene clases en el mismo sentido que los lenguajes de programación orientados a objetos.

## [Funciones](https://es.wikipedia.org/wiki/Subrutina)

Declaración de una [función](https://es.wikipedia.org/wiki/Subrutina):

```js
const sum = (p1, p2) => {
    console.log(p1)
    console.log(p2)
    return p1 + p2
}
```

y la función se llama:

```js
const result = sum(1, 5)
console.log(result)
```

Si hay un solo parámetro, podemos excluir los paréntesis de la definición:

```js
const square = (p) => {
    console.log(p)
    return p * p
}
```

Si la función solo contiene una expresión, entonces las llaves no son necesarias. En este caso, la función solo devuelve el resultado de su única expresión. Ahora, si eliminamos la impresión de la consola, podemos acortar aún más la definición de la función:

```js
const square = (p) => p * p
```

Esta forma es particularmente útil cuando se manipulan arrays, por ejemplo, cuando se usa el método `map`:

```js
const t = [1, 2, 3]
const tSquared = t.map((p) => p * p)
// tSquared ahora es [1, 4, 9]
```

Hay dos formas de hacer referencia a la función; uno está dando un nombre en una declaración de función.

```js
function product(a, b) {
    return a * b
}

const result = product(2, 6)
// result ahora es 12
```

La otra forma de definir la función es usando una expresión de función. En este caso, no es necesario darle un nombre a la función y la definición puede residir entre el resto del código:

```js
const average = function (a, b) {
    return (a + b) / 2
}

const result = average(2, 5)
// result ahora es 3.5
```

## Métodos de objeto y "this"

Las funciones de flecha y las funciones definidas usando la palabra clave `function` varían sustancialmente cuando se trata de cómo se comportan con respecto a la palabra clave `this`, que se refiere al objeto en sí.

Podemos asignar métodos a un objeto definiendo propiedades que son funciones:

```js
const arto = {
    name: 'Arto Hellas',
    age: 35,
    education: 'PhD',
    greet: function () {
        console.log('hello, my name is ' + this.name)
    },
}

arto.greet() // se imprime "hello, my name is Arto Hellas"
```

Los métodos se pueden asignar a los objetos incluso después de la creación del objeto:

```js
const arto = {
    name: 'Arto Hellas',
    age: 35,
    education: 'PhD',
    greet: function () {
        console.log('hello, my name is ' + this.name)
    },
}

arto.growOlder = function () {
    this.age += 1
}
console.log(arto.age) // se imprime 35
arto.growOlder()
console.log(arto.age) // se imprime 36
```

Modifiquemos ligeramente el objeto:

```js
const arto = {
    name: 'Arto Hellas',
    age: 35,
    education: 'PhD',
    greet: function () {
        console.log('hello, my name is ' + this.name)
    },
    doAddition: function (a, b) {
        console.log(a + b)
    },
}

arto.doAddition(1, 4) // se imprime 5

const referenceToAddition = arto.doAddition
referenceToAddition(10, 15) // se imprime 25
```

Ahora el objeto tiene el método `doAddition` que calcula la suma de números que se le da como parámetros. El método se llama de la forma habitual, utilizando el objeto `arto.doAddition(1, 4)` o almacenando una referencia de método en una variable y llamando al método a través de la variable: `referenceToAddition(10, 15)`.

Si intentamos hacer lo mismo con el método `greet` nos encontramos con un problema:

```js
arto.greet() // se imprime "hello, my name is Arto Hellas"

const referenceToGreet = arto.greet
referenceToGreet() // se imprime "hello, my name is undefined"
```

Al llamar al método a través de una referencia, el método pierde el conocimiento de cuál era el `this` original. A diferencia de otros lenguajes, en JavaScript el valor de `this` se define en función de cómo el método se llama. Cuando se llama al método a través de una referencia, el valor de this se convierte en el llamado objeto global y el resultado final a menudo no es lo que el desarrollador de software había previsto originalmente.

Perder la pista de `this` al escribir código JavaScript genera algunos problemas potenciales. A menudo surgen situaciones en las que React o Node (o más específicamente el motor JavaScript del navegador web) necesita llamar a algún método en un objeto que el desarrollador ha definido.

Una situación que lleva a la "desaparición" de `this` surge cuando establecemos un tiempo de espera para llamar a la función `greet` en el objeto `arto`, usando la función `setTimeout`.

```js
const arto = {
    name: 'Arto Hellas',
    greet: function () {
        console.log('hello, my name is ' + this.name)
    },
}

setTimeout(arto.greet, 1000)
```

Como se mencionó, el valor de `this` en JavaScript se define en función de cómo se llama al método. Cuando `setTimeout` llama al método, es el motor JavaScript el que realmente llama al método y, en ese punto, `this` se refiere al objeto global.

Existen varios mecanismos mediante los cuales se puede conservar el `this`original. Uno de ellos es usar un método llamado `bind`:

```js
setTimeout(arto.greet.bind(arto), 1000)
```

Al llamar a `arto.greet.bind(arto)` se crea una nueva función donde `this` está obligado a apuntar a `arto`, independientemente de dónde y cómo se llame al método.

Usando funciones de flecha es posible resolver algunos de los problemas relacionados con `this`. Sin embargo, no deben usarse como métodos para objetos porque entonces `this` no funciona en absoluto.

## [Clases](<https://es.wikipedia.org/wiki/Clase_(inform%C3%A1tica)>)

No existe un mecanismo de clase como los de los lenguajes de programación orientados a objetos. Sin embargo, hay características en JavaScript que hacen posible "simular" [clases orientadas a objetos](<https://es.wikipedia.org/wiki/Clase_(inform%C3%A1tica)>).

En el siguiente ejemplo definimos una "clase" llamada `Person` y dos objetos `Person`:

```js
class Person {
    constructor(name, age) {
        this.name = name
        this.age = age
    }
    greet() {
        console.log('hello, my name is ' + this.name)
    }
}

const adam = new Person('Adam Ondra', 29)
adam.greet()

const janja = new Person('Janja Garnbret', 23)
janja.greet()
```

Cuando se trata de sintaxis, las clases y los objetos creados a partir de ellos recuerdan mucho a las clases y objetos de Java. Su comportamiento también es bastante similar al de los objetos Java. En el núcleo, siguen siendo objetos basados en la herencia prototípica de JavaScript. El tipo de ambos objetos es en realidad `Object`, ya que JavaScript esencialmente solo define los tipos `Boolean`, `Null`, `Undefined`, `Number`, `String`, `Symbol`, `BigInt` y `Object`.

## Materiales JavaScript

-   [Elocuent Javascript](https://eloquentjavascript.net/)
-   [The Modern JavaScript Tutorial](https://javascript.info/)
