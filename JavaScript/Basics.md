# JavaScript

El nombre oficial del estándar [JavaScript](https://es.wikipedia.org/wiki/JavaScript) es [ECMAScript](https://es.wikipedia.org/wiki/ECMAScript).

Hoy en día, la forma más popular de realizar la [transpilación](https://es.wikipedia.org/wiki/Transpilador) es mediante [`Babel`](<https://es.wikipedia.org/wiki/Babel_(compilador)>). La [transpilación](https://es.wikipedia.org/wiki/Transpilador) se configura automáticamente en las aplicaciones de [React](https://es.wikipedia.org/wiki/React) creadas con [Vite](https://vitejs.dev/).

[Node.js](https://nodejs.org/en) es un entorno de ejecución de [JavaScript](https://es.wikipedia.org/wiki/JavaScript) basado en el motor de [JavaScript](https://es.wikipedia.org/wiki/JavaScript) Chrome V8 de Google y funciona prácticamente en cualquier lugar, desde servidores hasta teléfonos móviles. El código se escribe en archivos que terminan en `.js` que se ejecutan emitiendo el `comando node nombre_del_archivo.js`.

También es posible escribir código [JavaScript](https://es.wikipedia.org/wiki/JavaScript) en la consola de [Node.js](https://nodejs.org/en), que se abre escribiendo `node` en la [línea de comandos](https://es.wikipedia.org/wiki/Interfaz_de_l%C3%ADnea_de_comandos), así como en la consola de herramientas de desarrollo del navegador.

## Tipos de datos primitivos:

-   [`Number`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Number): Un valor numérico se compone de cualquier serie de caracteres numéricos. Aparte de esto también pueden representar conceptos numéricos como `Infinity` o `NaN`. Para transformar valor a número se puede usar la función `Number()`.

-   [`String`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/String): Cualquier conjunto de caracteres (letras, números, símbolos, etc.) entre un conjunto de comillas dobles (`"`), comillas simples (`'`) o comilla invertida (\`) es una primitiva de string. Cuando se llama como función, el [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) `String()` convierte un valor especificado en un literal de `string`.

    Las comillas simples, las comillas dobles y las comillas simples se pueden usar indistintamente para crear primitivas de `string`. Sin embargo, también puedes usar comillas simples para especificar literales de plantillas (a veces llamados "cadenas de plantillas"). A diferencia de los literales de `string` que se crean con comillas simples o dobles, los literales de plantilla permiten la interpolación de cadenas y las cadenas de varias líneas.

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

    Los literales de plantilla pueden contener expresiones de marcador de posición marcadas por un signo de dólar y llaves (`${}`). Estos marcadores de posición se “interpolan” de forma predeterminada, lo que significa que el resultado de la expresión reemplaza al marcador de posición en la `string` final.

    ```js
    console.log( "The result is " + ( 2 + 4 ) + "." );
    > The result is 6.

    console.log( `The result is ${ 2 + 4 }.` );
    > The result is 6.
    ```

-   [`Boolean`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Boolean): La primitiva booleana es un tipo de datos lógico con solo dos valores: `true` y `false`. Los valores que generan `false` incluyen `0`, `null`, `undefined`, `NaN`, una cadena vacía (`""`), un `valor omitido` y un booleano `false`. Todos los demás valores dan como resultado `true`.

-   `null`: La [palabra clave](https://es.wikipedia.org/wiki/Palabra_clave) `null` representa una ausencia de valor definida de forma intencional. `null` es una primitiva, aunque el operador `typeof` muestra que null es un `objeto`.

-   [`undefined`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/undefined): es un valor básico asignado a variables que se acaban de declarar o al valor resultante de una operación que no muestra un valor significativo.

    Aunque `undefined` y `null` tienen algunas superposiciones funcionales, tienen propósitos diferentes. En el sentido más estricto, `null` representa un valor definido intencionalmente como "en blanco", y `undefined` representa la falta de un valor asignado.

-   [`BigInt`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/BigInt): permite operaciones matemáticas en números fuera del rango permitido por `Number`. Para crear un `BigInt`, agrega `n` al final de un literal de número o pasa un valor de cadena entero o numérico a la función `BigInt()`.

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

    Los valores de `BigInt` no heredan los métodos ni las propiedades que proporciona el [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) `Number`, y no se pueden usar con los métodos que proporciona el [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) `Math` integrado de JavaScript. Lo más importante es que no puedes mezclar las primitivas `BigInt` y `Number` en operaciones aritméticas estándar.

-   [`Symbol`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Symbol): Una primitiva de símbolo representa un valor único que nunca coincide con ningún otro valor, incluidos los de otras primitivas de símbolos.
    Te permite usar símbolos como claves de propiedad únicas en un objeto, lo que evita colisiones con claves que cualquier otro código podría agregar a ese [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>).

    Hay tres tipos de símbolos:

    -   Símbolos creados con `Symbol()`
    -   Símbolos compartidos que se configuran y recuperan de un registro de símbolos global con `Symbol.for()`
    -   Los "símbolos conocidos" se definen como propiedades estáticas del [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) `Symbol`. Estos símbolos contienen métodos internos que no se pueden reemplazar accidentalmente.

    `Symbol()` acepta una descripción (o "nombre del símbolo") como argumento opcional. Estas descripciones son etiquetas legibles para fines de depuración y no afectan la unicidad del resultado. Todas las llamadas a `Symbol` muestran un tipo primitivo de símbolo completamente único, incluso si varias llamadas tienen descripciones idénticas:

    ```js
    Symbol( "My symbol." ) === Symbol( "My symbol." );
    > false
    ```

## [Variables](<https://es.wikipedia.org/wiki/Variable_(programaci%C3%B3n)>)

Las variables son una [estructura de datos](https://es.wikipedia.org/wiki/Estructura_de_datos) que asigna un nombre representativo a un valor. Pueden contener datos de cualquier tipo.

El nombre de una variable se denomina [identificador](https://es.wikipedia.org/wiki/Identificador). Un identificador válido debe seguir estas reglas:

-   Los identificadores pueden contener letras [`Unicode`](https://es.wikipedia.org/wiki/Unicode), signos de dólar (`$`), guiones bajos (`_`), dígitos (`0-9`) y algunos caracteres Unicode.
-   Los identificadores no pueden contener espacios en blanco, ya que el analizador usa espacios en blanco para separar los elementos de entrada. Por ejemplo, si intentas llamar a una variable `my Variable` en lugar de `myVariable`, el analizador ve dos identificadores, `my` y `Variable`, y arroja un error de sintaxis ("token inesperado: identificador").
-   Los identificadores deben comenzar con una letra, un guion bajo (`_`) o un signo de dólar (`$`). No pueden empezar con dígitos para evitar confusiones entre identificadores y números.
-   Las "palabras reservadas" o [palabras clave](https://es.wikipedia.org/wiki/Palabra_clave) que ya son sintácticamente significativas no se pueden usar como identificadores.
-   Los identificadores no pueden contener caracteres especiales (`!` `.` `,` `/` `\` `+` `-` `*` `=`).

A partir del ejemplo establecido por los métodos y las propiedades integrados de JavaScript, la mayúscula medial (también estilizada como "[camelCase](https://es.wikipedia.org/wiki/Camel_case)") es una convención muy común para los identificadores compuestos por varias palabras.

Algunos proyectos usan otras convenciones de nomenclatura según el contexto y la naturaleza de los datos. Por ejemplo, la primera letra de una clase suele llevar mayúsculas, por lo que los nombres de clase de varias palabras suelen usar una variante de mayúsculas mediales que se suele llamar "mayúsculas mediales" o [PascalCase](http://wiki.c2.com/?PascalCase).

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

`const` no define realmente una variable sino una constante para la cual el valor ya no se puede cambiar. Por otra parte `let` define una variable normal. El tipo de datos asignados a la variable puede cambiar durante la ejecución. Al principio y almacena un número entero y al final un `string`.

También es posible definir variables en [JavaScript](https://es.wikipedia.org/wiki/JavaScript) usando la [palabra clave](https://es.wikipedia.org/wiki/Palabra_clave) `var`. `var` fue, durante mucho tiempo, la única forma de definir variables. `const` y `let` se agregaron recientemente en la versión ES6. En situaciones específicas, `var` funciona de una manera diferente comparada con las definiciones de variables de la mayoría de los lenguajes.

-   [var, let y const - Qué, por qué y cómo](https://www.youtube.com/watch?v=sjyJBL5fkp8)

## Operadores

### [Operadores de comparación](https://developer.mozilla.org/es/docs/Web/JavaScript/Guide/Expressions_and_operators#comparacion)

Los [operadores de comparación](https://developer.mozilla.org/es/docs/Web/JavaScript/Guide/Expressions_and_operators#comparacion) comparan los valores de dos operandos y evalúan si la declaración que forman es `true` o `false`.

Las comparaciones estrictas con `===` o `!==` no realizan la [coerción](https://developer.mozilla.org/en-US/docs/Glossary/Type_Conversion) de tipos. Para que una comparación estricta evalúe como `true`, los valores que se comparen deben tener el mismo tipo de datos. Por este motivo, `2 == "2"` muestra `true`, pero `2 === "2"` muestra `false`.

-   `===`: Estrictamente igual.
-   `!==`: No estrictamente igual.
-   `==`: Igual (o "inigualable").
-   `!=`: No igual.
-   `>`: Mayor que.
-   `>=`: Mayor o igual que.
-   `<`: Menor que.
-   `<=`: Menor o igual que.

Todos los valores en [JavaScript](https://es.wikipedia.org/wiki/JavaScript) son `true` o `false` de manera implícita, y se pueden forzar al valor booleano correspondiente, por ejemplo, a través del comparador "de forma no estricta". Un conjunto limitado de valores se fuerza a `false`:

-   `0`.
-   `null`.
-   `undefined`.
-   `NaN`.
-   Una cadena vacía (`""`).

Todos los demás valores se convierten en `true`, incluida cualquier string que contenga uno o más caracteres y todos los números que no sean cero. Estos se suelen llamar valores "[Truthy](https://developer.mozilla.org/es/docs/Glossary/Truthy)" y "[Falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)".

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

Muestra el primer [operando](https://es.wikipedia.org/wiki/Operando) solo si ese operando tiene algún valor distinto de `null` o `undefined`. De lo contrario, muestra el segundo operando.

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

El control de flujo es el orden en el que el intérprete de [JavaScript](https://es.wikipedia.org/wiki/JavaScript) ejecuta las declaraciones. Si una secuencia de comandos no incluye declaraciones que alteren su flujo, se ejecuta de principio a fin, una línea a la vez. Las estructuras de control se usan para determinar si un conjunto de declaraciones se ejecuta según un conjunto definido de criterios, si se ejecuta un conjunto de declaraciones repetidamente o si se interrumpe una secuencia de declaraciones.

### Condicionales

#### if...else

Una declaración `if` evalúa una condición dentro de los paréntesis coincidentes que siguen. Si la condición dentro de los paréntesis se evalúa como `true`, se ejecuta el código que sigue a los paréntesis coincidentes. Si la condición dentro de los paréntesis se evalúa como ´false´, se ignora la declaración que la sigue.

```js
if ( true ) console.log( "True." );
> "True."

if ( true ) {
    const myString = "True.";
    console.log( myString );
}
> "True."
```

La [palabra clave](https://es.wikipedia.org/wiki/Palabra_clave) `else` que sigue inmediatamente a una declaración `if` y su declaración ejecutada condicionalmente especifica la declaración que se ejecutará si la condición `if` se evalúa como `false`.

```js
if ( false ) console.log( "True." )''
else console.log( "False" );
> "False."
```

##### Ternarias

`if` ejecuta una sentencia de forma condicional. El [operador ternario](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Operators/Conditional_operator) es la abreviatura para ejecutar una expresión de forma condicional. Como su nombre lo indica, el [operador ternario](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Operators/Conditional_operator) es el único operador de [JavaScript](https://es.wikipedia.org/wiki/JavaScript) que usa tres operandos:

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

#### switch…case

Usa la sentencia `switch` para comparar el valor de una expresión con una lista de valores potenciales definidos con una o más [palabras clave](https://es.wikipedia.org/wiki/Palabra_clave) `case`.

Cuando el intérprete alcanza un `case` con un valor que coincide con la expresión que se está evaluando entre paréntesis después de la [palabra clave](https://es.wikipedia.org/wiki/Palabra_clave) `switch`, ejecuta cualquier declaración que siga a esa cláusula `case`:

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

### Iteración y bucles

Los bucles te permiten repetir un conjunto de declaraciones mientras se cumpla una condición o hasta que se cumpla una condición. Usa bucles para ejecutar un conjunto de instrucciones una cantidad fija de veces, hasta que se logre un resultado específico o hasta que el intérprete llegue al final de una estructura de datos iterable (por ejemplo, el elemento final de un array, un mapa o un conjunto, la propiedad final de un [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) o el último carácter de una cadena).
Si no se pueden cumplir las condiciones durante la ejecución del bucle, este continúa de forma indefinida.

#### while

Se crea un bucle `while` con la [palabra clave](https://es.wikipedia.org/wiki/Palabra_clave) `while` seguida de un par de paréntesis coincidentes que contienen una condición para evaluar. Si la condición especificada se evalúa en un principio como `true`, se ejecuta la instrucción que sigue a esos paréntesis. De lo contrario, el bucle nunca se ejecuta. Después de cada iteración, la condición se vuelve a evaluar y, si aún es `true`, se repite el bucle.

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

#### do…while

Es una variante del bucle `while` en la que la evaluación condicional ocurre al final de cada iteración del bucle. Esto significa que el cuerpo del bucle siempre se ejecuta al menos una vez.

Para crear un bucle `do...while`, usa la [palabra clave](https://es.wikipedia.org/wiki/Palabra_clave) `do` seguida de la declaración (o la declaración de bloque) que se ejecutará en cada iteración del bucle. Inmediatamente después de esa declaración, agrega `while` y los paréntesis que coincidan con la condición que se evaluará. Cuando esta condición ya no se evalúa como `true`, el bucle finaliza.

#### for

Usa bucles `for` para iterar en una cantidad conocida. Para crear un bucle `for`, usa la [palabra clave](https://es.wikipedia.org/wiki/Palabra_clave) `for` seguida de un conjunto de paréntesis que acepte las siguientes tres expresiones en orden y separadas por punto y coma:

-   Una expresión que se evaluará cuando comience el bucle.
-   Una condición que determina si el bucle debe continuar.
-   Una expresión que se ejecutará al final de cada bucle.

Después de estos paréntesis, agrega la declaración que se ejecutará durante el bucle.

```js
for (let i = 0; i < 3; i++) {
    console.log('This loop will run three times.')
}
```

#### forEach

Los métodos `forEach()` que proporcionan los [constructores](<https://es.wikipedia.org/wiki/Constructor_(inform%C3%A1tica)>) [`Array`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Array), [`Map`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map), [`Set`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Set) y `NodeList` proporcionan una abreviatura útil para iterar sobre una estructura de datos en el contexto de una función de devolución de llamada. A diferencia de otras formas de bucle, un bucle creado con cualquier `método forEach()` _no_ se puede interrumpir usando `break` ni `continue`.

`forEach` es un método que pertenece al prototipo de cada estructura de datos. Cada método `forEach` espera una función de devolución de llamada como argumento, aunque varían ligeramente en términos de los argumentos incluidos cuando se llama a esa función. Un segundo argumento opcional especifica un valor `this` para usar como contexto de invocación de la función de devolución de llamada.

La función de devolución de llamada que se usa con `Array.forEach` proporciona parámetros que contienen el valor del elemento actual, el índice del elemento actual y el `array` en el que se invocó el método `forEach`:

```js
const myArray = [ true, false ];
myArray.forEach( ( myElement, i, originalArray ) => {
    console.log( i, myElement, originalArray  );
});
> 0 true Array(3) [ true, false ]
> 1 false Array(3) [ true, false ]
```

La función de devolución de llamada que se usa con `Map.forEach` proporciona parámetros que contienen el valor asociado con el elemento actual, la clave asociada con este y el mapa en el que se invocó el método `forEach`:

```js
const myMap = new Map([
    ['myKey', true],
    ['mySecondKey', false ],
]);
myMap.forEach( ( myValue, myKey, originalMap ) => {
    console.log( myValue, myKey, originalMap  );
});
> true "myKey" Map { myKey → true, mySecondKey → false }
> false "mySecondKey" Map { myKey → true, mySecondKey → false }
```

### JavaScript [Síncrono](https://web.dev/learn/javascript/appendix#main-thread)-[Asíncrono](https://developer.mozilla.org/es/docs/Learn/JavaScript/Asynchronous/Introducing)

Si bien JavaScript es en esencia [síncrono en ejecución](https://web.dev/learn/javascript/appendix#main-thread), hay mecanismos que permiten a los desarrolladores aprovechar el bucle de eventos para realizar tareas asíncronas.

#### Promesas

Una promesa es un marcador de posición para un valor que se desconoce cuando se crea la promesa. Es un contenedor que dicta una operación asíncrona, los términos por los cuales la operación se considera un éxito o un fracaso, las acciones que se deben realizar en cualquier caso y el valor que se genera.

Crea una instancia de promesa mediante el operador `new` con la función de [constructor](<https://es.wikipedia.org/wiki/Constructor_(inform%C3%A1tica)>) `Promise()`. Este [constructor](<https://es.wikipedia.org/wiki/Constructor_(inform%C3%A1tica)>) acepta una función llamada executor como argumento. Esa función ejecutor normalmente se usa para realizar una o más acciones asíncronas y, luego, dictar los términos por los cuales la promesa debe considerarse completada o rechazada de forma correcta. Una promesa se define como pendiente mientras se ejecuta la función ejecutor. Cuando el ejecutor finaliza, una promesa se considera cumplida (o resuelta, en algunas fuentes de documentación) si la función del ejecutor y la acción asíncrona que realiza se completan con éxito, y se rechazan si la función del ejecutor encuentra un error o falla la acción asíncrona. Después de que se cumple o rechaza una promesa, esta se considera cumplida.

El [constructor](<https://es.wikipedia.org/wiki/Constructor_(inform%C3%A1tica)>) llama a la función ejecutor con dos argumentos. Esos argumentos son funciones que te permiten cumplir o rechazar la promesa de forma manual:

```js
const myPromise = new Promise((fulfill, reject) => {})
```

Se llama a las funciones que se usan para cumplir o rechazar una promesa con el valor resultante de la promesa como argumento (por lo general, un error de rechazo):

```js
const myPromise = new Promise( ( fulfill, reject ) => {
  const myResult = true;
  setTimeout(() => {
    if( myResult === true ) {
        fulfill( "This Promise was successful." );
    } else {
        reject( new Error( "This Promise has been rejected." ) );
    }
  }, 10000);
});

myPromise;
> Promise { <state>: "pending" }

myPromise;
> Promise { <state>: "fulfilled", <value>: "This Promise was successful." }
```

##### Encadenamiento de promesas

Se puede actuar sobre el [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) `Promise` resultante con los métodos `then()`, `catch()` y `finally()` heredados del [constructor](<https://es.wikipedia.org/wiki/Constructor_(inform%C3%A1tica)>) `Promise`. Cada uno de estos métodos muestra una promesa, en la que se puede actuar de inmediato con `then()`, `catch()` o `finally()` otra vez, lo que te permite encadenar las promesas resultantes.

`then()` proporciona dos funciones de devolución de llamada como argumentos. Usa la primera para cumplir la promesa resultante y la segunda para rechazarla. Ambos métodos aceptan un solo argumento que le da su valor a la promesa resultante.

```js
const myPromise = new Promise( ( fulfill, reject ) => {
    const myResult = true;
    setTimeout(() => {
        if( myResult === true ) {
            fulfill( "This Promise was fulfilled." );
        } else {
            reject( new Error( "This Promise has been rejected." ) );
        }
    }, 100);
});

myPromise.then( successfulResult => console.log( successfulResult ), failedResult => console.error( failedResult ) );
> "This Promise was successful."
```

También puedes usar then() para controlar solo el estado entregado y catch para manejar el estado rechazado. Llama a catch con un solo argumento que contenga el valor proporcionado en el método de rechazo de la promesa:

```js
const myPromise = new Promise( ( fulfill, reject ) => {
    const myResult = false;
    setTimeout(() => {
        if( myResult === true ) {
            fulfill( "This Promise was fulfilled." );
        } else {
            reject( new Error( "This Promise has been rejected." ) );
        }
    }, 100);
});

myPromise
    .then( fulfilledResult => console.log(fulfilledResult ) )
    .catch( rejectedResult => console.log( rejectedResult ) )
    .finally( () => console.log( "The Promise has settled." ) );
> "Error: This Promise has been rejected."
> "The Promise has settled."
```

A diferencia de `then` y `catch`, que permiten que una función de controlador se ejecute cuando se cumple o se rechaza una promesa, se llama a una función pasada como argumento al método `finally` sin importar si la promesa se cumplió o se rechazó. Se llama a la función del controlador sin argumentos porque no está diseñada para trabajar con los valores que se pasaron desde la Promesa, sino solo para ejecutar el código después de que se completa la Promesa.

##### Simultaneidad

El [constructor](<https://es.wikipedia.org/wiki/Constructor_(inform%C3%A1tica)>) `Promise` proporciona cuatro métodos para trabajar con varias promesas relacionadas mediante un iterable que contiene [objetos](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) Promise. Cada uno de estos métodos muestra una promesa, que se cumple o se rechaza según el estado de las promesas que se le hayan pasado. `Promise.all()`, por ejemplo, crea una promesa que se cumple solo si se cumple cada promesa que se pasa a ese método:

```js
const firstPromise  = new Promise( ( fulfill, reject ) => fulfill( "Successful. ") );
const secondPromise = new Promise( ( fulfill, reject ) => fulfill( "Successful. ") );
const thirdPromise  = new Promise( ( fulfill, reject ) => fulfill( "Successful. ") );
const failedPromise = new Promise( ( fulfill, reject ) => reject( "Failed.") );
const successfulPromises = [ firstPromise, secondPromise, thirdPromise ];
const oneFailedPromise = [ failedPromise, ...successfulPromises ];

Promise.all( successfulPromises )
    .then( ( allValues ) => {
        console.log( allValues );
    })
    .catch( ( failValue ) => {
        console.error( failValue );
    });
> Array(3) [ "Successful. ", "Successful. ", "Successful. " ]

Promise.all( oneFailedPromise  )
    .then( ( allValues ) => {
        console.log( allValues );
    })
    .catch( ( failValue ) => {
        console.error( failValue );
    });
> "Failed."
```

Los métodos de simultaneidad de Promise son los siguientes:

-   `Promise.all()`: Se completa solo si se cumplen todas las promesas proporcionadas.
-   `Promise.any()`: Se completa si se cumple alguna de las promesas proporcionadas y se rechaza solo si se rechazan todas.
-   `Promise.allSettled()`: Se cumplen cuando se cumplen las promesas, independientemente del resultado.
-   `Promise.race()`: Se rechaza o se cumple en función del resultado de la primera promesa que se concilia, se ignoran todas las promesas liquidadas más tarde.
    `async`/`await`

Cuando usas la palabra clave `async` antes de una declaración de función o una expresión de función, cualquier valor que muestre esa función se muestra como una promesa cumplida que contiene ese valor. Esto te permite ejecutar y administrar operaciones asíncronas con los mismos flujos de trabajo que el desarrollo síncrono.

```js
async function myFunction() {
    return "This is my returned value.";
}

myFunction().then( myReturnedValue => console.log( myReturnedValue ) );
> "This is my returned value."
```

La expresión `await` pausa la ejecución de una función asíncrona mientras se establece la promesa asociada. Una vez que se establece la promesa, el valor de la expresión await es el valor cumplido o rechazado de la promesa.

```js
async function myFunction() {
    const myPromise  = new Promise( ( fulfill, reject ) => { setTimeout( () => fulfill( "Successful. "), 5000 ); });
    const myPromisedResult = await myPromise;
    return myPromisedResult;
}

myFunction()
    .then( myResult => console.log( myResult ) )
    .catch( myFailedResult => console.error( myFailedResult ) );
> "Successful."
```

Cualquier valor que no sea promesa incluido en una expresión await se muestra como una promesa completada:

```js
async function myFunction() {
    const myPromisedResult = await "String value.";
    return myPromisedResult;
}

myFunction()
    .then( myResult => console.log( myResult ) )
    .catch( myFailedResult => console.error( myFailedResult ) );
> "String value."
```

## Colecciones indexadas

Una colección indexada es una estructura de datos en la que los elementos se almacenan y se accede a ellos mediante índices numerados. A los valores almacenados en una colección indexada se les asignan índices numerados a partir de `0`, un patrón llamado “indexación cero”. Luego, puedes acceder a los valores almacenados en una colección indexada mediante la referencia a sus índices.

### [Arrays](<https://es.wikipedia.org/wiki/Vector_(inform%C3%A1tica)>)

Un `array` es un contenedor que puede contener cero o más valores de cualquier tipo de datos, incluidos otros arrays o [objetos](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) complejos. A veces, los valores almacenados en un `array` se denominan “elementos” de este.

Al igual que con los tipos de datos primitivos, existen dos enfoques para crear un `array`: como un literal de `array` o mediante la invocación del [constructor](<https://es.wikipedia.org/wiki/Constructor_(inform%C3%A1tica)>) integrado `Array()` de [JavaScript](https://es.wikipedia.org/wiki/JavaScript) con `new Array()`. Asignar un `array` a una variable proporciona una forma iterable y altamente portátil de asignar varios valores a un solo identificador.

```js
const myArray = []
const myArray = new Array()
```

Cuando se pasa un solo valor numérico al [constructor](<https://es.wikipedia.org/wiki/Constructor_(inform%C3%A1tica)>) `Array`, ese valor no se asigna a la posición cero en el `array` resultante. En su lugar, se crea un [arreglo](https://developer.mozilla.org/es/docs/Glossary/Array) con esa cantidad de ranuras vacías para los valores. Esto no impone ninguna limitación en el `array`. Los elementos se pueden agregar y quitar de la misma manera que con un literal de [arreglo](https://developer.mozilla.org/es/docs/Glossary/Array).

Puedes acceder a elementos individuales dentro del `array` con la notación de corchetes (`[]`) que sigue al `array` o su identificador que contiene un número que hace referencia al índice del elemento.

Los `arrays` en [JavaScript](https://es.wikipedia.org/wiki/JavaScript) no son asociativos, lo que significa que no puedes usar una `string` arbitraria como índice. Sin embargo, los valores numéricos que se usan para acceder a los elementos de un `array` se fuerzan a un valor de cadena en segundo plano, lo que significa que puedes usar un valor de cadena que solo contenga caracteres numéricos.

```js
const myArray = [ "My string", 50, true ];

myArray[ 2 ];
> true

myArray[ "2" ];
> true
```

Si intentas acceder a un elemento fuera de los definidos en el array, se generará `undefined`, no un error.

#### Desestructuración

La [desestructuración](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) de la asignación es una manera concisa de extraer un rango de valores de [arreglos](https://developer.mozilla.org/es/docs/Glossary/Array) u [objetos](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) y asignarlos a un conjunto de identificadores, un proceso que a veces se denomina [“desempaquetar”](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) la estructura de datos original, aunque no modifica el [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) ni el [arreglo](https://developer.mozilla.org/es/docs/Glossary/Array) original.

La [asignación de desestructuración](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) usa una lista de identificadores similar a un [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) o [arreglo](https://developer.mozilla.org/es/docs/Glossary/Array) para realizar un seguimiento de los valores. En su forma más simple, llamada desestructuración de patrón de vinculación, cada valor se descomprime del [arreglo](https://developer.mozilla.org/es/docs/Glossary/Array) o el [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) y se asigna a una variable correspondiente, que se inicializa mediante `let` o `const` (o `var`).

Usa llaves (`{}`) para desestructurar un [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) y corchetes (`[]`) para desestructurar un `array`.

```js
const myArray = [ false, true ];
const myObject = { firstValue: false, secondValue: true };

const [ myProp, mySecondProp ] = myObject;
> Uncaught TypeError: myObject is not iterable

const { myElement, mySecondElement } = myArray;

myElement
> undefined

mySecondElement;
> undefined
```

#### Operador de distribución

Usa el operador de distribución (`...`), para expandir una estructura de datos iterable, como un `array`, una cadena o un literal de [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>), en elementos individuales. Al operador de dispersión le sigue inmediatamente la estructura de datos que se expandirá o el identificador de una variable que contiene esa estructura de datos.

```js
const myArray = [ 4, 5, 6 ];
const mySecondArray = [1, 2, 3, ...myArray ];

mySecondArray;
> Array(6) [ 1, 2, 3, 4, 5, 6 ]
```

Puedes usar la sintaxis de distribución sólo en los siguientes contextos:

En el caso de los arrays y strings, la sintaxis de distribución solo se aplica cuando se esperan cero o más argumentos en una llamada a función o cuando se esperan elementos de un `array`. El primer ejemplo de sintaxis del operador de dispersión de esta sección funciona porque pasa `...myArray` como argumento al método integrado `console.log`.

Por ejemplo, no puedes asignar los datos que se distribuyen a una variable fuera de otro [arreglo](https://developer.mozilla.org/es/docs/Glossary/Array).

Para combinar los elementos que conforman dos o más arrays en uno solo:

```js
const myArray = [ 1, 2, 3 ];
const mySecondArray = [ 4, 5, 6 ];
const myNewArray = [ ...myArray, ...mySecondArray ];

myNewArray;
> Array(6) [ 1, 2, 3, 4, 5, 6 ]
```

Para pasar elementos de un `array` como argumentos individuales en una llamada a función:

```js
const myArray = [ true, false ];
const myFunction = ( myArgument, mySecondArgument ) => {
    console.log( myArgument, mySecondArgument );
};

myFunction( ...myArray );
> true false
```

Cabe destacar el hecho de que el contenido de el `array` se puede modificar aunque esté definido como `const`. Como el `array` es un objeto, la variable siempre apunta al mismo [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>). Sin embargo, el contenido del `array` cambia a medida que se le agregan nuevos elementos.

Una forma de iterar a través de los elementos del `array` es usar `forEach` como se ve en el ejemplo. `forEach` recibe una función definida usando la sintaxis de flecha como parámetro.

```js
;(value) => {
    console.log(value)
}
```

`forEach` llama a la función para cada uno de los elementos del `array`, siempre pasando el elemento individual como parámetro. La función como parámetro de `forEach` también puede recibir otros parámetros.

En el ejemplo anterior, se agregó un nuevo elemento al `array` usando el método `push`. Cuando se usa [React](https://es.wikipedia.org/wiki/React), a menudo se usan técnicas de [programación funcional](https://es.wikipedia.org/wiki/Programaci%C3%B3n_funcional). Una característica del paradigma de [programación funcional](https://es.wikipedia.org/wiki/Programaci%C3%B3n_funcional) es el uso de [estructuras de datos inmutables](https://es.wikipedia.org/wiki/Objeto_inmutable). En el código de [React](https://es.wikipedia.org/wiki/React), es preferible usar el método `concat`, que no agrega el elemento al `array`, pero crea un nuevo `array` en la que se incluyen el contenido del `array` anterior y el nuevo elemento.

```js
const t = [1, -1, 3]

const t2 = t.concat(5) // crea un nuevo array

console.log(t) // se imprime [1, -1, 3]
console.log(t2) // se imprime [1, -1, 3, 5]
```

La llamada al método `t.concat(5)` no agrega un nuevo elemento al `array` anterior, pero devuelve un nuevo `array` que, además de contener los elementos del `array` anterior, también contiene el elemento nuevo.

## Colecciones con clave

Puedes usar literales de [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) para almacenar pares clave-valor y [arreglos](https://developer.mozilla.org/es/docs/Glossary/Array) para almacenar colecciones de valores iterables.

### `Map`

Un mapa es una estructura de datos iterable que almacena información como pares [clave-valor](https://es.wikipedia.org/wiki/Base_de_datos_clave-valor), similar a un literal de [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>). A diferencia de los literales de objeto, un mapa permite que los valores y las claves tengan cualquier tipo de datos, y los elementos de orden que se agregan a un mapa se conservan cuando se itera sobre él.

Puedes prepropagar datos de un mapa mediante una sintaxis similar a un `array` que contenga [objetos](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) similares a un `array` compuestos por dos elementos. El primer elemento de cada una de estas estructuras de datos de dos elementos se convierte en la clave, mientras que el segundo se convierte en el valor asociado con esa clave. La forma más simple de esto es un `array` en el que cada elemento es un `array` compuesto por dos elementos: la clave y el valor del elemento que se agregará al mapa.

```js
const myMap = new Map([
    [ "myKey", "A string value" ],
    [ "mySecondKey", 500 ],
    [ "myThirdKey", true ]
]);

myMap;
> Map(3) {'myKey' => 'A string value', 'mySecondKey' => 500, 'myThirdKey' => true}
```

Para obtener, configurar o borrar elementos de Map, usa los métodos heredados del [constructor](<https://es.wikipedia.org/wiki/Constructor_(inform%C3%A1tica)>) `Map`:

```js
const myMap = new Map();

myMap;
> Map(0)

myMap.set( "myKey", "My value." );

myMap.has( "myKey" );
> true

myMap.get( "myKey" );
"My value."

myMap.delete( "myKey" );

myMap;
> Map(0)
```

Un ejemplo más práctico:

```js
const t = [1, 2, 3]

const m1 = t.map((value) => value * 2)
console.log(m1) // se imprime [2, 4, 6]
```

Basado en el `array` anterior, `map` crea un nuevo `array`, para el cual la función dada como parámetro se usa para crear los elementos. En el caso de este ejemplo, el valor original se multiplica por dos.

`Map` también puede transformar el `array` en algo completamente diferente:

```js
const m2 = t.map((value) => '<li>' + value + '</li>')
console.log(m2)
// se imprime [ '<li>1</li>', '<li>2</li>', '<li>3</li>' ]
```

### `set`

Un conjunto es una colección iterable de valores únicos similar a un `array`, aunque un conjunto solo puede contener valores únicos. Al igual que con un mapa, la iteración sobre un conjunto conserva los elementos de orden que se le agregaron.

Debido a que un conjunto no permite elementos duplicados, cuando se crea un conjunto a partir de un `array` que contiene varias instancias del mismo valor, solo retiene la primera instancia de ese valor.

```js
const mySet = new Set([ 1, 2, 3, 2 ]);

mySet;
> Set(3) [ 1, 2, 3 ]
```

Para agregar o quitar elementos de un conjunto, usa los métodos heredados del [constructor](<https://es.wikipedia.org/wiki/Constructor_(inform%C3%A1tica)>) `Set`. Estos métodos actúan sobre un elemento según el valor de este, en lugar de hacer referencia a un índice.

```js
const mySet = new Set();

mySet.add( "My value." );

mySet;
> Set [ "My value." ]

mySet.has( "My value." );
> true

mySet.delete( "My value." );

mySet;
> Set []
```

## [Objetos](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>)

Los [objetos](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) son un tipo de datos discreto de la misma manera en que cada primitivo es un tipo de datos, con una diferencia crítica: a diferencia de las primitivas, los [objetos](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) son mutables. Un [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) puede contener datos asociados con identificadores, como una variable, pero mantiene su tipo de datos object sin importar los datos que contenga.

Además de las primitivas, todos los valores de [JavaScript](https://es.wikipedia.org/wiki/JavaScript) son objetos, aunque incluso los literales primitivos muestran un comportamiento similar a un [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) debido a la herencia prototípica. Se suele decir que [JavaScript](https://es.wikipedia.org/wiki/JavaScript) está formado efectivamente por objetos.

Un literal de [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) es un par de llaves que rodean cero o más pares clave-valor llamados “propiedades”, que pueden contener cualquier valor de JavaScript.

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

Se hace referencia a las propiedades de un [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) usando la notación "de punto", o usando corchetes:

```js
console.log(object1.name) // se imprime Arto Hellas
const fieldName = 'age'
console.log(object1[fieldName]) // se imprime 35

object1.address = 'Helsinki'
object1['secret number'] = 12341
```

La última de las adiciones debe hacerse usando corchetes, porque cuando se usa la notación de puntos, secret number no es un nombre de propiedad válido debido al carácter de espacio.

Naturalmente, los [objetos](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) en [JavaScript](https://es.wikipedia.org/wiki/JavaScript) también pueden tener [métodos](<https://es.wikipedia.org/wiki/M%C3%A9todo_(inform%C3%A1tica)>).

Los [objetos](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) también se pueden definir usando las llamadas funciones de [constructor](<https://es.wikipedia.org/wiki/Constructor_(inform%C3%A1tica)>), lo que da como resultado un mecanismo que recuerda a muchos otros lenguajes de programación, por ejemplo, las clases de Java. A pesar de esta similitud, [JavaScript](https://es.wikipedia.org/wiki/JavaScript) no tiene clases en el mismo sentido que los lenguajes de programación orientados a objetos.

## [Funciones](https://es.wikipedia.org/wiki/Subrutina)

Una [función](https://es.wikipedia.org/wiki/Subrutina) es un bloque modular y reutilizable de sentencias que se usa para realizar un conjunto de tareas relacionadas. Al igual que con todos los valores no primitivos, las funciones son objetos. Son [objetos](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) únicos porque se los puede llamar para ejecutar código, pasar datos en forma de argumentos y devolver un valor.

Se consideran funciones como [objetos](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) de "primera clase", lo que significa que, a pesar de su comportamiento único, pueden usarse en los mismos contextos que cualquier otro [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) de JavaScript. Por ejemplo, una función puede asignarse a una variable, pasarse como argumento a otras funciones y ser devuelta por otras funciones.

Una función definida como una propiedad de un [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) se suele denominar `method`. Al igual que con las variables declaradas con `var`, las declaraciones de funciones realizadas fuera de una función contenedora se agregan al [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) global como métodos.

Una declaración de función (también llamada "declaración de funciones" o "definición de la función") crea una función con nombre que se puede invocar en otro lugar del alcance que la contiene. Las declaraciones de funciones constan de la [palabra clave](https://es.wikipedia.org/wiki/Palabra_clave) function seguida de un identificador, una lista de parámetros separados por comas encerrados entre paréntesis y una declaración de bloque denominada "cuerpo de la función".

```js
function myFunction() {
    console.log( "This is my function." );
};

myFunction();
> "This is my function."
```

Los parámetros en la definición de la función actúan como variables de marcador de posición para los valores que se pueden pasar al cuerpo de la función cuando se la llama. Los valores entre paréntesis cuando se llama a una función son "argumentos". Si se omite un argumento esperado, el parámetro resultante contiene un valor `undefined` porque se declara el parámetro en el cuerpo de la función, pero no se inicializa con un valor.

Para configurar los valores predeterminados de los parámetros, inicialízalos de la misma manera en que inicializarías una variable: un operador de asignación (`=`) seguido de un valor. Si más adelante especificas un argumento para esa función, ese valor nuevo anula el valor predeterminado.

El cuerpo de una función no de flecha también tiene acceso a un [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) arguments tipo `array` con índice cero que contiene todos los valores pasados como argumentos, sin importar si la definición de la función especifica parámetros o no.

```js
function myFunction( myParameter = "omitted" ) {
   console.log( `The value is: ${ myParameter }.` );
};

myFunction( "this string" );
> "The value is: this string."

myFunction();
> "The value is: omitted."
```

### Expresiones de función

Las expresiones de función son funciones creadas en las que se espera una expresión. Con frecuencia, encontrarás expresiones de funciones como valores asignados a una variable. Aunque una declaración de función siempre requiere un nombre, puedes usar expresiones de función para crear funciones anónimas omitiendo el identificador y siguiendo la [palabra clave](https://es.wikipedia.org/wiki/Palabra_clave) function con un par de paréntesis que contengan parámetros opcionales:

```js
const myVariable = function () {}
```

```js
const myVariable = function myFunction() {
    console.log( `I'm a ${ typeof myFunction }.`);
};

typeof myFunction;
> "undefined"

typeof myVariable;
> "function"

myVariable();
> "I'm a function."
```

#### Expresiones de funciones de flecha

Puedes crear una función de flecha donde se espere una expresión, por ejemplo, como un valor asignado a una variable. En su forma más común, una función de flecha se compone de un par de paréntesis coincidentes que contienen cero o más parámetros, una flecha compuesta por un solo signo igual y un carácter mayor que (`=>`), y un par de llaves coincidentes que contienen el cuerpo de la función:

```js
const myFunction = () => {}

const myFunction = (myParameter) => {}
```

Sin embargo, a diferencia de las declaraciones de funciones, se puede acceder a una expresión de función con nombre con el nombre de una función solo dentro de la función en sí.

Las funciones de flecha son únicas, ya que no tienen su propio contexto para los valores `arguments` o `this`. En cambio, heredan ambos valores del entorno que lo contiene de la función de flecha, la función de cierre más cercana que proporciona esos contextos.

### La [palabra clave](https://es.wikipedia.org/wiki/Palabra_clave) `new`

Si llamas a una función con `new`, se crea un [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) nuevo que usa la función llamada como "constructor" para ese objeto:

```js
function MyFunction() {}
const myObject = new MyFunction();

typeof myObject;
> "object"`
```

Esto permite que una "función de [constructor](<https://es.wikipedia.org/wiki/Constructor_(inform%C3%A1tica)>)" proporcione una plantilla para la creación de [objetos](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) que siguen el mismo patrón estructural:

```js
function MyFunction() {
    this.myProperty = true;
}
const myObject = new MyFunction();

myObject.myProperty;
> true
```

El valor de `this` dentro de una función de [constructor](<https://es.wikipedia.org/wiki/Constructor_(inform%C3%A1tica)>) se refiere al [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) que se crea, lo que permite que este se propague con propiedades y métodos en el momento de la creación. Esto permite la creación de [objetos](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) que contengan valores de datos y cualquier método necesario para actuar sobre esos datos como una sola unidad portátil, un concepto llamado "encapsulamiento".

```js
function MyFunction( myArgument ) {
    this.myValue = myArgument;
    this.doubleMyValue = () => myArgument * 2;
}
const myObject = new MyFunction( 10 );

myObject.myValue;
> 10

myObject.doubleMyValue();
> 20
```

### La [palabra clave](https://es.wikipedia.org/wiki/Palabra_clave) `this`

La [palabra clave](https://es.wikipedia.org/wiki/Palabra_clave) `this` se refiere al valor del [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) que está vinculado a la función en el momento de su llamada, lo que significa que su valor es diferente dependiendo de si se llama a una función como método, como función independiente o como [constructor](<https://es.wikipedia.org/wiki/Constructor_(inform%C3%A1tica)>).

Cuando se llama a una función, crea una instancia de la [palabra clave](https://es.wikipedia.org/wiki/Palabra_clave) `this` en segundo plano como referencia al [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) que contiene esa función, lo que otorga acceso a las propiedades y los métodos definidos junto a ella desde su alcance. En algunos casos, trabajar con `this` es similar a trabajar con una variable declarada con `const`. Al igual que una constante, `this` no se puede quitar y su valor no se puede reasignar, pero los métodos y las propiedades del [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) que contiene la [palabra clave](https://es.wikipedia.org/wiki/Palabra_clave) `this` se pueden modificar.

#### Vinculación global

Fuera de una función o del contexto de un objeto, `this` hace referencia a la propiedad `globalThis`, que es una referencia al [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) global en la mayoría de los entornos de JavaScript. En el contexto de una secuencia de comandos que se ejecuta en un navegador web, el [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) global es el [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) `window`. En Node.js, globalThis es el [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) `global`.

#### Vinculación implícita

Cuando se llama a una función como método de un objeto, una instancia de this dentro de ese método hace referencia al [objeto](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) que lo contiene, lo que otorga acceso a los métodos y las propiedades que se encuentran a su lado.

```js
let myObject = {
    myValue: "This is my string.",
    myMethod() {
        console.log( this.myValue );
    }
};

myObject.myMethod();
> "This is my string."
```

#### `this` en funciones de flecha

En las funciones de flecha, `this` se resuelve en una vinculación en un entorno que lo encierra léxicamente. Esto significa que `this` en una función de flecha hace referencia al valor de `this` en el contexto envolvente más cercano.

```js
let myObject = {
    myMethod() { console.log( this ); },
    myArrowFunction: () => console.log( this ),
    myEnclosingMethod: function () {
        this.myArrowFunction = () => { console.log(this) };
    }
};

myObject.myMethod();
> Object { myMethod: myMethod(), myArrowFunction: myArrowFunction() }

myObject.myArrowFunction();
> Window {...}
```

## [Clases](<https://es.wikipedia.org/wiki/Clase_(inform%C3%A1tica)>)

Las clases son funciones especiales que sirven como plantillas para crear [objetos](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) que ya contienen datos, propiedades asociadas con esos datos y métodos relacionados con la manipulación de esos datos. Estos objetos, propiedades y métodos se denominan, en conjunto, "miembros" de la clase.

Para definir una clase, usa la [palabra clave](https://es.wikipedia.org/wiki/Palabra_clave) `class`. Con las prácticas recomendadas y la convención establecida por las funciones de [constructor](<https://es.wikipedia.org/wiki/Constructor_(inform%C3%A1tica)>) integradas de JavaScript, comienza cualquier identificador de una clase con mayúscula. El objetivo de las clases es proporcionar formas más accesibles de trabajar con funciones avanzadas de prototipos y funciones de [constructor](<https://es.wikipedia.org/wiki/Constructor_(inform%C3%A1tica)>).

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

Las funciones definidas dentro del cuerpo de una clase se exponen como métodos de cada instancia de esa clase.

```js
class MyClass {
    classMethod() {
        console.log( "My class method." );
    }
}

const myClassInstance = new MyClass();

myClassInstance.classMethod();
> "My class method."
```

Cuando se crea una instancia de una clase, se llama a un método `constructor()` especial que realiza cualquier "configuración" necesaria para la instancia recién creada y, luego, inicializa las propiedades asociadas a ella. Cualquier argumento que se pase a la clase cuando se crea la instancia estará disponible para el método `constructor()`. Dentro del cuerpo de una clase, el valor de this hace referencia a la instancia en sí, con cualquier propiedad definida en this expuesta como propiedades de cada instancia de esa clase.

```js
class MyClass {
    constructor( myPassedValue ) {
        this.instanceProp = myPassedValue;
    }
    myMethod() {
        console.log( this.instanceProp );
    }
}

const myClassInstance = new MyClass( "A string." );

myClassInstance.myMethod();
> "A string."
```

Si no defines un `constructor()` para tu clase, el motor de [JavaScript](https://es.wikipedia.org/wiki/JavaScript) usa un [constructor](<https://es.wikipedia.org/wiki/Constructor_(inform%C3%A1tica)>) vacío "predeterminado". Cada clase solo puede tener un método especial llamado `constructor()`.

Cuando se trata de sintaxis, las clases y los [objetos](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) creados a partir de ellos recuerdan mucho a las clases y [objetos](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) de Java. Su comportamiento también es bastante similar al de los [objetos](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) Java. En el núcleo, siguen siendo [objetos](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) basados en la herencia prototípica de JavaScript. El tipo de ambos [objetos](<https://es.wikipedia.org/wiki/Objeto_(programaci%C3%B3n)>) es en realidad `Object`, ya que [JavaScript](https://es.wikipedia.org/wiki/JavaScript) esencialmente solo define los tipos `Boolean`, `Null`, `Undefined`, `Number`, `String`, `Symbol`, `BigInt` y `Object`.

## Materiales JavaScript

-   [Elocuent Javascript](https://eloquentjavascript.net/)
-   [The Modern JavaScript Tutorial](https://javascript.info/)
-   [Curso de Google](https://web.dev/learn/javascript)
