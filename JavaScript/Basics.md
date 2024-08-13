# JavaScript

El nombre oficial del estándar [JavaScript](https://es.wikipedia.org/wiki/JavaScript) es [ECMAScript](https://es.wikipedia.org/wiki/ECMAScript).

Hoy en día, la forma más popular de realizar la [transpilación](https://es.wikipedia.org/wiki/Transpilador) es mediante `Babel`. La [transpilación](https://es.wikipedia.org/wiki/Transpilador) se configura automáticamente en las aplicaciones de React creadas con Vite.

[Node.js](https://nodejs.org/en) es un entorno de ejecución de JavaScript basado en el motor de JavaScript Chrome V8 de Google y funciona prácticamente en cualquier lugar, desde servidores hasta teléfonos móviles. El código se escribe en archivos que terminan en .js que se ejecutan emitiendo el `comando node nombre_del_archivo.js`.

También es posible escribir código JavaScript en la consola de Node.js, que se abre escribiendo node en la línea de comandos, así como en la consola de herramientas de desarrollo del navegador. Las revisiones más recientes de Chrome manejan las características más nuevas de JavaScript bastante bien sin transpilar el código. Alternativamente, puedes utilizar una herramienta como JS Bin.

JavaScript recuerda, tanto en nombre como en sintaxis, a Java. Pero cuando se trata del mecanismo central del lenguaje, no podrían ser más diferentes. Viniendo de un entorno de Java, el comportamiento de JavaScript puede parecer un poco extraño, especialmente si uno no hace el esfuerzo de buscar sus características.

## Tipos de datos primitivos:

-   `Number`: Un valor numérico se compone de cualquier serie de caracteres numéricos. Aparte de esto también pueden representar conceptos numéricos como `Infinity` o `NaN`. Para transformar valor a número se puede usar la función `Number()`.

-   `String`: Cualquier conjunto de caracteres (letras, números, símbolos, etc.) entre un conjunto de comillas dobles ("), comillas simples (') o comillas simples (\`) es una primitiva de string. Cuando se llama como función, el objeto `String()` convierte un valor especificado en un literal de string.

Las comillas simples, las comillas dobles y las comillas simples se pueden usar indistintamente para crear primitivas de strings. Sin embargo, también puedes usar comillas simples para especificar literales de plantillas (a veces llamados "cadenas de plantillas"). A diferencia de los literales de string que se crean con comillas simples o dobles, los literales de plantilla permiten la interpolación de cadenas y las cadenas de varias líneas.

```js
const myString = "This
is a string.";
> Uncaught SyntaxError: "" string literal contains an unescaped line break

const myString = `This
is a string.`;

console.log( myString );

> This
is a string.
```

Los literales de plantilla pueden contener expresiones de marcador de posición marcadas por un signo de dólar y llaves (${}). Estos marcadores de posición se “interpolan” de forma predeterminada, lo que significa que el resultado de la expresión reemplaza al marcador de posición en la string final.

```js
console.log( "The result is " + ( 2 + 4 ) + "." );
> The result is 6.

console.log( `The result is ${ 2 + 4 }.` );
> The result is 6.
```

-   `Boolean`: La primitiva booleana es un tipo de datos lógico con solo dos valores: `true` y `false`. Los valores que generan `false` incluyen `0`, `null`, `undefined`, `NaN`, una cadena vacía (`""`), un `valor omitido` y un booleano `false`. Todos los demás valores dan como resultado `true`.

-   `null`: La palabra clave `null` representa una ausencia de valor definida de forma intencional. `null` es una primitiva, aunque el operador `typeof` muestra que null es un `objeto`.

-   `undefined`: es un valor básico asignado a variables que se acaban de declarar o al valor resultante de una operación que no muestra un valor significativo.

Aunque `undefined` y `null` tienen algunas superposiciones funcionales, tienen propósitos diferentes. En el sentido más estricto, `null` representa un valor definido intencionalmente como "en blanco", y `undefined` representa la falta de un valor asignado.

-   `BigInt`: permite operaciones matemáticas en números fuera del rango permitido por `Number`. Para crear un `BigInt`, agrega `n` al final de un literal de número o pasa un valor de cadena entero o numérico a la función `BigInt()`.

```js
const myNumber = 9999999999999999;
const myBigInt = 9999999999999999n;

typeof myNumber;
> "number"

typeof myBigInt;
> "bigint"

myNumber;
> 10000000000000000

myBigInt;
> 9999999999999999n
```

En este ejemplo, `9999999999999999` está fuera del rango de dígitos que `Number` puede representar de forma segura, lo que genera un error de redondeo.

Los valores de `BigInt` no heredan los métodos ni las propiedades que proporciona el objeto `Number`, y no se pueden usar con los métodos que proporciona el objeto `Math` integrado de JavaScript. Lo más importante es que no puedes mezclar las primitivas `BigInt` y `Number` en operaciones aritméticas estándar

-   `Symbol`: Una primitiva de símbolo representa un valor único que nunca coincide con ningún otro valor, incluidos los de otras primitivas de símbolos.
    Te permite usar símbolos como claves de propiedad únicas en un objeto, lo que evita colisiones con claves que cualquier otro código podría agregar a ese objeto.

    Hay tres tipos de símbolos:

    -   Símbolos creados con `Symbol()`
    -   Símbolos compartidos que se configuran y recuperan de un registro de símbolos global con `Symbol.for()`
    -   Los "símbolos conocidos" se definen como propiedades estáticas del objeto `Symbol`. Estos símbolos contienen métodos internos que no se pueden reemplazar accidentalmente.

`Symbol()` acepta una descripción (o "nombre del símbolo") como argumento opcional. Estas descripciones son etiquetas legibles para fines de depuración y no afectan la unicidad del resultado. Todas las llamadas a `Symbol` muestran un tipo primitivo de símbolo completamente único, incluso si varias llamadas tienen descripciones idénticas:

```js
Symbol( "My symbol." ) === Symbol( "My symbol." );
> false
```

## [Variables](<https://es.wikipedia.org/wiki/Variable_(programaci%C3%B3n)>)

Las variables son una [estructura de datos](https://es.wikipedia.org/wiki/Estructura_de_datos) que asigna un nombre representativo a un valor. Pueden contener datos de cualquier tipo.

El nombre de una variable se denomina identificador. Un identificador válido debe seguir estas reglas:

-   Los identificadores pueden contener letras `Unicode`, signos de dólar (`$`), guiones bajos (`_`), dígitos (`0-9`) y algunos caracteres Unicode.
-   Los identificadores no pueden contener espacios en blanco, ya que el analizador usa espacios en blanco para separar los elementos de entrada. Por ejemplo, si intentas llamar a una variable my `Variable` en lugar de `myVariable`, el analizador ve dos identificadores, `my` y `Variable`, y arroja un error de sintaxis ("token inesperado: identificador").
-   Los identificadores deben comenzar con una letra, un guion bajo (`_`) o un signo de dólar (`$`). No pueden empezar con dígitos para evitar confusiones entre identificadores y números.
-   Las "palabras reservadas" que ya son sintácticamente significativas no se pueden usar como identificadores.
-   Los identificadores no pueden contener caracteres especiales (`!` `.` `,` `/` `\` `+` `-` `*` `=`).

A partir del ejemplo establecido por los métodos y las propiedades integrados de JavaScript, la mayúscula medial (también estilizada como "[camelCase](https://es.wikipedia.org/wiki/Camel_case)") es una convención muy común para los identificadores compuestos por varias palabras. El uso de mayúsculas mediales es la práctica de utilizar mayúsculas en la primera letra de cada palabra, excepto en la primera, para mejorar la legibilidad sin espacios.

Algunos proyectos usan otras convenciones de nomenclatura según el contexto y la naturaleza de los datos. Por ejemplo, la primera letra de una clase suele llevar mayúsculas, por lo que los nombres de clase de varias palabras suelen usar una variante de mayúsculas mediales que se suele llamar "mayúsculas mediales" o [Pascal](http://wiki.c2.com/?PascalCase).

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

## Operadores

### Operadores de comparación

Los operadores de comparación comparan los valores de dos operandos y evalúan si la declaración que forman es `true` o `false`.

Las comparaciones estrictas con `===` o `!==` no realizan la coerción de tipos. Para que una comparación estricta evalúe como true, los valores que se comparen deben tener el mismo tipo de datos. Por este motivo, `2 == "2"` muestra true, pero `2 === "2"` muestra false.

-   `===`: Estrictamente igual.
-   `!==`: No estrictamente igual.
-   `==`: Igual (o "inigualable").
-   `!=`: No igual.
-   `>`: Mayor que.
-   `>=`: Mayor o igual que.
-   `<`: Menor que.
-   `<=`: Menor o igual que.

Todos los valores en JavaScript son `true` o `false` de manera implícita, y se pueden forzar al valor booleano correspondiente, por ejemplo, a través del comparador "de forma no estricta". Un conjunto limitado de valores se fuerza a `false`:

    - `0`.
    - `null`.
    - `undefined`.
    - `NaN`.
    - Una cadena vacía (`""`).

Todos los demás valores se convierten en `true`, incluida cualquier string que contenga uno o más caracteres y todos los números que no sean cero. Estos se suelen llamar valores "de verdad" y "falsidad".

### Operadores lógicos

Usa los operadores lógicos AND (`&&`), OR (`||`) y NOT (`!`) para controlar el flujo de una secuencia de comandos en función de la evaluación de dos o más sentencias condicionales.

```js
2 === 3 || 5 === 5;
> true

2 === 2 && 2 === "2"
> false

2 === 2 && !"My string."
> false
```

### Operador coalescente nulo

Muestra el primer operando solo si ese operando tiene algún valor distinto de `null` o `undefined`. De lo contrario, muestra el segundo operando.

```js
null ?? "My string"
> "My string"

undefined ?? "My string"
> "My string"

true ?? "My string";
> true
```

### Operadores lógicos de asignación

Usa operadores de asignación para asignar el valor de un segundo operador a un primer operador. El ejemplo más común es un signo igual (`=`), que se usa para asignar un valor a una variable declarada.

## Control de flujo

El control de flujo es el orden en el que el intérprete de JavaScript ejecuta las declaraciones. Si una secuencia de comandos no incluye declaraciones que alteren su flujo, se ejecuta de principio a fin, una línea a la vez. Las estructuras de control se usan para determinar si un conjunto de declaraciones se ejecuta según un conjunto definido de criterios, si se ejecuta un conjunto de declaraciones repetidamente o si se interrumpe una secuencia de declaraciones.

## Condicionales

### if...else

Una declaración `if` evalúa una condición dentro de los paréntesis coincidentes que siguen. Si la condición dentro de los paréntesis se evalúa como `true`, se ejecuta la declaración o declaración de bloque que sigue a los paréntesis coincidentes. Si la condición dentro de los paréntesis se evalúa como ´false´, se ignora la declaración que la sigue.

```js
if ( true ) console.log( "True." );
> "True."

if ( true ) {
    const myString = "True.";
    console.log( myString );
}
> "True."
```

La palabra clave `else` que sigue inmediatamente a una declaración `if` y su declaración ejecutada condicionalmente especifica la declaración que se ejecutará si la condición `if` se evalúa como `false`.

```js
if ( false ) console.log( "True." )''
else console.log( "False" );
> "False."
```

#### Ternarias

`if` ejecuta una sentencia de forma condicional. El operador ternario (más preciso, pero menos común, se llama operador condicional ternario) es la abreviatura para ejecutar una expresión de forma condicional. Como su nombre lo indica, el operador ternario es el único operador de JavaScript que usa tres operandos:

-   Una condición que se evaluará, seguida de un signo de interrogación (`?`).
-   La expresión que se ejecutará si la condición se evalúa como `true`, seguida de dos puntos (`:`).
-   La expresión que se ejecutará si la condición se evalúa como `false`.

```js
const myFirstResult  = true  ? "First value." : "Second value.";
const mySecondResult = false ? "First value." : "Second value.";

myFirstResult;
> "First value."

mySecondResult;
> "Second value."
```

### switch…case

Usa la sentencia `switch` para comparar el valor de una expresión con una lista de valores potenciales definidos con una o más palabras clave case.

Cuando el intérprete alcanza un case con un valor que coincide con la expresión que se está evaluando entre paréntesis después de la palabra clave switch, ejecuta cualquier declaración que siga a esa cláusula case:

```js
switch ( 2 + 2 === 4 ) {
    case false:
        console.log( "False." );
        break;

    case true:
        console.log( "True." );
        break;

    default:
        console.log("Default response");
}
> "True."
```

## Iteración y bucles

Los bucles te permiten repetir un conjunto de declaraciones mientras se cumpla una condición o hasta que se cumpla una condición. Usa bucles para ejecutar un conjunto de instrucciones una cantidad fija de veces, hasta que se logre un resultado específico o hasta que el intérprete llegue al final de una estructura de datos iterable (por ejemplo, el elemento final de un array, un mapa o un conjunto, la propiedad final de un objeto o el último carácter de una cadena).
Si no se pueden cumplir las condiciones durante la ejecución del bucle, este continúa de forma indefinida.

### while

Se crea un bucle `while` con la palabra clave `while` seguida de un par de paréntesis coincidentes que contienen una condición para evaluar. Si la condición especificada se evalúa en un principio como `true`, se ejecuta la instrucción que sigue a esos paréntesis. De lo contrario, el bucle nunca se ejecuta. Después de cada iteración, la condición se vuelve a evaluar y, si aún es `true`, se repite el bucle.

```js
let iterationCount = 0;
while( iterationCount < 3 ) {
    iterationCount++;
    console.log( `Loop ${ iterationCount }.` );
}
> "Loop 1."
> "Loop 2."
```

Si el intérprete encuentra una declaración `continue` en un bucle `while`, detiene esa iteración, vuelve a evaluar la condición y, si es posible, continúa el bucle.

```js
let iterationCount = 0;
while( iterationCount <= 5 ) {
    iterationCount++;
    if( iterationCount === 3 ) {
        continue;
    }
    console.log( `Loop ${ iterationCount }.` );
}
console.log( "Loop ended." );
> "Loop 1."
> "Loop 2."
> "Loop 4."
> "Loop 5."
> "Loop ended."
```

Si el intérprete encuentra una declaración `break` en un bucle `while`, se detiene la iteración y no se vuelve a evaluar la condición, lo que permite que el intérprete continúe.

```js
let iterationCount = 1;
while( iterationCount <= 5 ) {
    if( iterationCount === 3 ) {
        console.log(`Iteration skipped.``);`
        break;
    }
    console.log( `Loop ${ iterationCount }.` );
    iterationCount++;
}
console.log( "Loop ended." );
> "Loop 1."
> "Loop 2."
> "Iteration skipped.
> "Loop ended."
```

### do…while

Es una variante del bucle `while` en la que la evaluación condicional ocurre al final de cada iteración del bucle. Esto significa que el cuerpo del bucle siempre se ejecuta al menos una vez.

Para crear un bucle `do...while`, usa la palabra clave `do` seguida de la declaración (o la declaración de bloque) que se ejecutará en cada iteración del bucle. Inmediatamente después de esa declaración, agrega `while` y los paréntesis que coincidan con la condición que se evaluará. Cuando esta condición ya no se evalúa como `true`, el bucle finaliza.

### for

Usa bucles `for` para iterar en una cantidad conocida.Para crear un bucle `for`, usa la palabra clave `for` seguida de un conjunto de paréntesis que acepte las siguientes tres expresiones en orden y separadas por punto y coma:

-   Una expresión que se evaluará cuando comience el bucle.
-   Una condición que determina si el bucle debe continuar
-   Una expresión que se ejecutará al final de cada bucle

Después de estos paréntesis, agrega la declaración que se ejecutará durante el bucle.

```js
for (let i = 0; i < 3; i++) {
    console.log('This loop will run three times.')
}
```

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
