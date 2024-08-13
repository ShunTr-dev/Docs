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

### forEach

Los métodos `forEach()` que proporcionan los constructores `Array`, `Map`, `Set` y `NodeList` proporcionan una abreviatura útil para iterar sobre una estructura de datos en el contexto de una función de devolución de llamada. A diferencia de otras formas de bucle, un bucle creado con cualquier `método forEach()` no se puede interrumpir usando `break` ni `continue`.

`forEach` es un método que pertenece al prototipo de cada estructura de datos. Cada método `forEach` espera una función de devolución de llamada como argumento, aunque varían ligeramente en términos de los argumentos incluidos cuando se llama a esa función. Un segundo argumento opcional especifica un valor this para usar como contexto de invocación de la función de devolución de llamada.

La función de devolución de llamada que se usa con Array.forEach proporciona parámetros que contienen el valor del elemento actual, el índice del elemento actual y el array en el que se invocó el método forEach:

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

## Colecciones indexadas

Una colección indexada es una estructura de datos en la que los elementos se almacenan y se accede a ellos mediante índices numerados. A los valores almacenados en una colección indexada se les asignan índices numerados a partir de `0`, un patrón llamado “indexación cero”. Luego, puedes acceder a los valores almacenados en una colección indexada mediante la referencia a sus índices.

### [Arrays](<https://es.wikipedia.org/wiki/Vector_(inform%C3%A1tica)>)

Un array es un contenedor que puede contener cero o más valores de cualquier tipo de datos, incluidos otros arrays o objetos complejos. A veces, los valores almacenados en un array se denominan “elementos” de este.

Al igual que con los tipos de datos primitivos, existen dos enfoques para crear un array: como un literal de array o mediante la invocación del constructor integrado `Array()` de JavaScript con `new Array()`. Asignar un array a una variable proporciona una forma iterable y altamente portátil de asignar varios valores a un solo identificador.

```js
const myArray = []
const myArray = new Array()
```

Cuando se pasa un solo valor numérico al constructor `Array`, ese valor no se asigna a la posición cero en el array resultante. En su lugar, se crea un arreglo con esa cantidad de ranuras vacías para los valores. Esto no impone ninguna limitación en el array. Los elementos se pueden agregar y quitar de la misma manera que con un literal de arreglo.

Puedes acceder a elementos individuales dentro del array con la notación de corchetes (`[]`) que sigue al array o su identificador que contiene un número que hace referencia al índice del elemento.

Los arrays en JavaScript no son asociativos, lo que significa que no puedes usar una string arbitraria como índice. Sin embargo, los valores numéricos que se usan para acceder a los elementos de un array se fuerzan a un valor de cadena en segundo plano, lo que significa que puedes usar un valor de cadena que solo contenga caracteres numéricos.

```js
const myArray = [ "My string", 50, true ];

myArray[ 2 ];
> true

myArray[ "2" ];
> true
```

Si intentas acceder a un elemento fuera de los definidos en el array, se generará `undefined`, no un error.

#### Desestructuración

La desestructuración de la asignación es una manera concisa de extraer un rango de valores de arreglos u objetos y asignarlos a un conjunto de identificadores, un proceso que a veces se denomina “desempaquetar” la estructura de datos original, aunque no modifica el objeto ni el arreglo original.

La asignación de desestructuración usa una lista de identificadores similar a un objeto o arreglo para realizar un seguimiento de los valores. En su forma más simple, llamada desestructuración de patrón de vinculación, cada valor se descomprime del arreglo o el objeto y se asigna a una variable correspondiente, que se inicializa mediante `let` o `const` (o `var`).

Usa llaves (`{}`) para desestructurar un objeto y corchetes (`[]`) para desestructurar un array.

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

Usa el operador de distribución (`...`), para expandir una estructura de datos iterable, como un array, una cadena o un literal de objeto, en elementos individuales. Al operador de dispersión le sigue inmediatamente la estructura de datos que se expandirá o el identificador de una variable que contiene esa estructura de datos.

```js
const myArray = [ 4, 5, 6 ];
const mySecondArray = [1, 2, 3, ...myArray ];

mySecondArray;
> Array(6) [ 1, 2, 3, 4, 5, 6 ]
```

Puedes usar la sintaxis de distribución solo en los siguientes contextos:

En el caso de los arrays y strings, la sintaxis de distribución solo se aplica cuando se esperan cero o más argumentos en una llamada a función o cuando se esperan elementos de un array. El primer ejemplo de sintaxis del operador de dispersión de esta sección funciona porque pasa `...myArray` como argumento al método integrado `console.log`.

Por ejemplo, no puedes asignar los datos que se distribuyen a una variable fuera de otro arreglo.

Para combinar los elementos que conforman dos o más arrays en uno solo:

```js
const myArray = [ 1, 2, 3 ];
const mySecondArray = [ 4, 5, 6 ];
const myNewArray = [ ...myArray, ...mySecondArray ];

myNewArray;
> Array(6) [ 1, 2, 3, 4, 5, 6 ]
```

Para pasar elementos de un array como argumentos individuales en una llamada a función:

```js
const myArray = [ true, false ];
const myFunction = ( myArgument, mySecondArgument ) => {
    console.log( myArgument, mySecondArgument );
};

myFunction( ...myArray );
> true false
```

Cabe destacar el hecho de que el contenido de el array se puede modificar aunque esté definido como `const`. Como el array es un objeto, la variable siempre apunta al mismo objeto. Sin embargo, el contenido del array cambia a medida que se le agregan nuevos elementos.

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

## Colecciones con clave

Puedes usar literales de objeto para almacenar pares clave-valor y arreglos para almacenar colecciones de valores iterables.

### `Map`

Un mapa es una estructura de datos iterable que almacena información como pares clave-valor, similar a un literal de objeto. A diferencia de los literales de objeto, un mapa permite que los valores y las claves tengan cualquier tipo de datos, y los elementos de orden que se agregan a un mapa se conservan cuando se itera sobre él.

Puedes prepropagar datos de un mapa mediante una sintaxis similar a un array (o a cualquier objeto iterador) que contenga objetos similares a un array compuestos por dos elementos. El primer elemento de cada una de estas estructuras de datos de dos elementos se convierte en la clave, mientras que el segundo se convierte en el valor asociado con esa clave. La forma más simple de esto es, en efecto, un array en el que cada elemento es un array compuesto por dos elementos: la clave y el valor del elemento que se agregará al mapa.

```js
const myMap = new Map([
    [ "myKey", "A string value" ],
    [ "mySecondKey", 500 ],
    [ "myThirdKey", true ]
]);

myMap;
> Map(3) {'myKey' => 'A string value', 'mySecondKey' => 500, 'myThirdKey' => true}
```

Para obtener, configurar o borrar elementos de Map, usa los métodos heredados del constructor `Map`:

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

### `set`

Un conjunto es una colección iterable de valores únicos similar a un array, aunque un conjunto solo puede contener valores únicos. Al igual que con un mapa, la iteración sobre un conjunto conserva los elementos de orden que se le agregaron.

Debido a que un conjunto no permite elementos duplicados, cuando se crea un conjunto a partir de un array que contiene varias instancias del mismo valor, solo retiene la primera instancia de ese valor.

```js
const mySet = new Set([ 1, 2, 3, 2 ]);

mySet;
> Set(3) [ 1, 2, 3 ]
```

Para agregar o quitar elementos de un conjunto, usa los métodos heredados del constructor Set. Estos métodos actúan sobre un elemento según el valor de este, en lugar de hacer referencia a un índice.

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

Los objetos son un tipo de datos discreto de la misma manera en que cada primitivo es un tipo de datos, con una diferencia crítica: a diferencia de las primitivas, los objetos son mutables. Un objeto puede contener datos asociados con identificadores, como una variable, pero mantiene su tipo de datos object sin importar los datos que contenga.

Además de las primitivas, todos los valores de JavaScript son objetos, aunque incluso los literales primitivos muestran un comportamiento similar a un objeto debido a la herencia prototípica. Se suele decir que JavaScript está formado efectivamente por objetos.

Un literal de objeto es un par de llaves que rodean cero o más pares clave-valor llamados “propiedades”, que pueden contener cualquier valor de JavaScript.

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

Se hace referencia a las propiedades de un objeto usando la notación "de punto", o usando corchetes:

```js
console.log(object1.name) // se imprime Arto Hellas
const fieldName = 'age'
console.log(object1[fieldName]) // se imprime 35

object1.address = 'Helsinki'
object1['secret number'] = 12341
```

La última de las adiciones debe hacerse usando corchetes, porque cuando se usa la notación de puntos, secret number no es un nombre de propiedad válido debido al carácter de espacio.

Naturalmente, los objetos en JavaScript también pueden tener [métodos](<https://es.wikipedia.org/wiki/M%C3%A9todo_(inform%C3%A1tica)>).

Los objetos también se pueden definir usando las llamadas funciones de constructor, lo que da como resultado un mecanismo que recuerda a muchos otros lenguajes de programación, por ejemplo, las clases de Java. A pesar de esta similitud, JavaScript no tiene clases en el mismo sentido que los lenguajes de programación orientados a objetos.

## [Funciones](https://es.wikipedia.org/wiki/Subrutina)

Una [función](https://es.wikipedia.org/wiki/Subrutina) es un bloque modular y reutilizable de sentencias que se usa para realizar un conjunto de tareas relacionadas. Al igual que con todos los valores no primitivos, las funciones son objetos. Son objetos únicos porque se los puede llamar para ejecutar código, pasar datos en forma de argumentos y devolver un valor.

Se consideran funciones como objetos de "primera clase", lo que significa que, a pesar de su comportamiento único, pueden usarse en los mismos contextos que cualquier otro objeto de JavaScript. Por ejemplo, una función puede asignarse a una variable, pasarse como argumento a otras funciones y ser devuelta por otras funciones.

Una función definida como una propiedad de un objeto se suele denominar `method`. Al igual que con las variables declaradas con `var`, las declaraciones de funciones realizadas fuera de una función contenedora se agregan al objeto global como métodos.

Una declaración de función (también llamada "declaración de funciones" o "definición de la función") crea una función con nombre que se puede invocar en otro lugar del alcance que la contiene. Las declaraciones de funciones constan de la palabra clave function seguida de un identificador, una lista de parámetros separados por comas encerrados entre paréntesis y una declaración de bloque denominada "cuerpo de la función".

```js
function myFunction() {
   console.log( "This is my function." );
};

myFunction();
> "This is my function."
```

Los parámetros en la definición de la función actúan como variables de marcador de posición para los valores que se pueden pasar al cuerpo de la función cuando se la llama. Los valores entre paréntesis cuando se llama a una función son "argumentos". Si se omite un argumento esperado, el parámetro resultante contiene un valor `undefined` porque se declara el parámetro en el cuerpo de la función, pero no se inicializa con un valor.

Para configurar los valores predeterminados de los parámetros, inicialízalos de la misma manera en que inicializarías una variable: un operador de asignación (`=`) seguido de un valor. Si más adelante especificas un argumento para esa función, ese valor nuevo anula el valor predeterminado.

El cuerpo de una función no de flecha también tiene acceso a un objeto arguments tipo `array` con índice cero que contiene todos los valores pasados como argumentos, sin importar si la definición de la función especifica parámetros o no.

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

Las expresiones de función son funciones creadas en las que se espera una expresión. Con frecuencia, encontrarás expresiones de funciones como valores asignados a una variable. Aunque una declaración de función siempre requiere un nombre, puedes usar expresiones de función para crear funciones anónimas omitiendo el identificador y siguiendo la palabra clave function con un par de paréntesis que contengan parámetros opcionales:

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

### La palabra clave `new`

Si llamas a una función con `new`, se crea un objeto nuevo que usa la función llamada como "constructor" para ese objeto:

```js
function MyFunction() {}
const myObject = new MyFunction();

typeof myObject;
> "object"`
```

Esto permite que una "función de constructor" proporcione una plantilla para la creación de objetos que siguen el mismo patrón estructural:

```js
function MyFunction() {
    this.myProperty = true;
}
const myObject = new MyFunction();

myObject.myProperty;
> true
```

El valor de `this` dentro de una función de constructor se refiere al objeto que se crea, lo que permite que este se propague con propiedades y métodos en el momento de la creación. Esto permite la creación de objetos que contengan valores de datos y cualquier método necesario para actuar sobre esos datos como una sola unidad portátil, un concepto llamado "encapsulamiento".

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

### La palabra clave `this`

La palabra clave `this` se refiere al valor del objeto que está vinculado a la función en el momento de su llamada, lo que significa que su valor es diferente dependiendo de si se llama a una función como método, como función independiente o como constructor.

Cuando se llama a una función, crea una instancia de la palabra clave `this` en segundo plano como referencia al objeto que contiene esa función, lo que otorga acceso a las propiedades y los métodos definidos junto a ella desde su alcance. En algunos casos, trabajar con `this` es similar a trabajar con una variable declarada con `const`. Al igual que una constante, `this` no se puede quitar y su valor no se puede reasignar, pero los métodos y las propiedades del objeto que contiene la palabra clave `this` se pueden modificar.

#### Vinculación global

Fuera de una función o del contexto de un objeto, `this` hace referencia a la propiedad `globalThis`, que es una referencia al objeto global en la mayoría de los entornos de JavaScript. En el contexto de una secuencia de comandos que se ejecuta en un navegador web, el objeto global es el objeto `window`. En Node.js, globalThis es el objeto `global`.

#### Vinculación implícita

Cuando se llama a una función como método de un objeto, una instancia de this dentro de ese método hace referencia al objeto que lo contiene, lo que otorga acceso a los métodos y las propiedades que se encuentran a su lado.

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

Las clases son funciones especiales que sirven como plantillas para crear objetos que ya contienen datos, propiedades asociadas con esos datos y métodos relacionados con la manipulación de esos datos. Estos objetos, propiedades y métodos se denominan, en conjunto, "miembros" de la clase.

Para definir una clase, usa la palabra clave `class`. Con las prácticas recomendadas y la convención establecida por las funciones de constructor integradas de JavaScript, comienza cualquier identificador de una clase con mayúscula. El objetivo de las clases es proporcionar formas más accesibles de trabajar con funciones avanzadas de prototipos y funciones de constructor.

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

Si no defines un `constructor()` para tu clase, el motor de JavaScript usa un constructor vacío "predeterminado". Cada clase solo puede tener un método especial llamado `constructor()`.

Cuando se trata de sintaxis, las clases y los objetos creados a partir de ellos recuerdan mucho a las clases y objetos de Java. Su comportamiento también es bastante similar al de los objetos Java. En el núcleo, siguen siendo objetos basados en la herencia prototípica de JavaScript. El tipo de ambos objetos es en realidad `Object`, ya que JavaScript esencialmente solo define los tipos `Boolean`, `Null`, `Undefined`, `Number`, `String`, `Symbol`, `BigInt` y `Object`.

## Materiales JavaScript

-   [Elocuent Javascript](https://eloquentjavascript.net/)
-   [The Modern JavaScript Tutorial](https://javascript.info/)
-   [Curso de Google](https://web.dev/learn/javascript)
