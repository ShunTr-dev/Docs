# CSS Grid
CSS Grid es un módulo de CSS que permite crear diseños de página más complejos y flexibles en comparación con los métodos tradicionales de diseño web. Con CSS Grid, puedes crear fácilmente una cuadrícula bidimensional donde puedes colocar elementos HTML en filas y columnas.

- Diseño bidimensional: A diferencia de Flexbox, que trabaja principalmente en una dimensión (fila o columna), CSS Grid funciona en dos dimensiones, permitiendo colocar elementos tanto en filas como en columnas.
- División de espacio: CSS Grid divide el espacio del contenedor en filas y columnas definidas por el desarrollador. Esto ofrece un mayor control sobre el diseño de la página.
- Control del flujo de contenido: CSS Grid permite especificar cómo los elementos HTML fluyen dentro de la cuadrícula, lo que brinda una flexibilidad significativa para la disposición de los elementos en la página.
- Alineación y espaciado: Con CSS Grid, puedes alinear y distribuir elementos a lo largo de las filas y columnas de la cuadrícula con propiedades como justify-items, align-items, justify-content, align-content, grid-gap, entre otras.
- Ordenación de elementos: CSS Grid permite cambiar fácilmente el orden de los elementos en la cuadrícula sin alterar el orden en el HTML, lo que proporciona una mayor flexibilidad en el diseño.

En resumen, CSS Grid es una herramienta poderosa que permite crear diseños complejos y flexibles en las páginas web, proporcionando un control preciso sobre la disposición y el flujo de los elementos en una cuadrícula bidimensional. Es especialmente útil para diseñar diseños más avanzados y adaptativos en sitios web modernos.

```html
<div class="container">
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <div>4</div>
    <div>5</div>
    <div>6</div>
</div>

<style type="text/css">
    .container{
        background: #09f;
        border: 3px solid gray;
        border-radius: 10px;
        display: grid;
        grid-template-columns: 
    }

    .container div {
        background: lightblue;
        border: 2px white;
    }
</style>
```

## [CSS Grid](https://github.com/ShunTr-dev/Docs/blob/main/CSS/CSS%20Grid.md) vs [CSS Flex](https://github.com/ShunTr-dev/Docs/blob/main/CSS/CSS%20Flex.md)
CSS Grid y CSS Flexbox son dos herramientas poderosas para el diseño de diseños en CSS, pero tienen diferentes enfoques y funcionalidades. Estas son las diferencias clave entre CSS Grid y CSS Flexbox:

- Modelo de disposición:
* CSS Grid: Funciona en **dos dimensiones** (filas y columnas) y permite colocar elementos en una cuadrícula bidimensional.
* CSS Flexbox: Funciona en **una dimensión** (fila o columna) y es ideal para organizar elementos en una sola dirección, como una fila o una columna.

- Flexibilidad:
* CSS Grid: Proporciona un mayor control sobre el diseño de la página, permitiendo dividir el espacio del contenedor en filas y columnas definidas por el desarrollador.
* CSS Flexbox: Ofrece flexibilidad en la alineación y distribución de elementos en una sola dirección, pero puede no ser tan adecuado para diseños bidimensionales complejos.

- Alineación:
* CSS Grid: Permite alinear elementos tanto en el eje de las filas como en el de las columnas, utilizando propiedades como justify-items, align-items, justify-content, align-content, entre otras.
* CSS Flexbox: Se enfoca en la alineación de elementos a lo largo de un solo eje, con propiedades como justify-content y align-items.

- Orden de los elementos:
* CSS Grid: Facilita cambiar el orden de los elementos en la cuadrícula sin alterar el orden en el HTML, lo que brinda una mayor flexibilidad en el diseño.
* CSS Flexbox: También permite cambiar el orden de los elementos, pero principalmente a lo largo de un eje único.

- Uso recomendado:
* CSS Grid: Es más adecuado para diseños de página complejos y bidimensionales, como esquemas de mosaicos, cuadrículas de imágenes y diseños de estilo editorial.
* CSS Flexbox: Es útil para alinear y distribuir elementos en una sola dirección, como menús de navegación, barras laterales y diseños de elementos en línea.

En resumen, CSS Grid es ideal para diseñar diseños bidimensionales complejos y controlar el flujo de contenido en una página web, mientras que CSS Flexbox es más adecuado para organizar elementos en una sola dirección de manera flexible y eficiente. Ambos pueden utilizarse juntos según las necesidades específicas de diseño de un proyecto.


## Fracciones
Las fracciones (`fr`) son una unidad de medida que se utiliza para distribuir el espacio disponible en una cuadrícula entre las filas o columnas. La unidad `fr` asigna una parte proporcional del espacio restante después de que se hayan asignado los tamaños a las filas o columnas definidas con otras unidades de medida.

```css
.grid-container {
    display: grid;
    grid-template-columns: 1fr 2fr 1fr; /* Tres columnas con la primera y la tercera ocupando una fracción del espacio disponible cada una, y la segunda ocupando el doble de esa cantidad */
    grid-template-rows: 1fr 2fr; /* Dos filas, ambas ocupando una fracción del espacio disponible, siendo la segunda el doble de alta que la primera */
}
```
- `grid-template-columns` especifica tres columnas. La primera y la tercera tienen un tamaño que equivale a una fracción del espacio disponible, mientras que la segunda columna tiene el doble de tamaño que las otras dos.
 - `grid-template-rows` especifica dos filas. Ambas ocupan una fracción del espacio disponible, pero la segunda fila es el doble de alta que la primera.


## grid-template-columns y grid-template-rows
`grid-template-columns` y `grid-template-rows` son una propiedad que se utiliza para definir el tamaño y el número de columnas y filas en una cuadrícula. Esta propiedad permite especificar las dimensiones de las columnas y filas de una cuadrícula mediante valores absolutos, relativos o mediante funciones.

```css
.grid-container {
    display: grid;
    grid-template-columns: 100px 200px 1fr;
    grid-template-rows: 100px 200px 1fr;
}
```
- 100px, 200px y 1fr son los valores que definen el ancho de las columnas.
- 100px y 200px son valores absolutos, lo que significa que las primeras dos columnas tendrán un ancho fijo de 100 píxeles y 200 píxeles, respectivamente.
- 1fr es una unidad de fracción flexible, lo que significa que la tercera columna tomará el espacio restante disponible en el contenedor después de que se asignen los anchos a las primeras dos columnas.

También puedes usar otras unidades de medida (como porcentaje, `em`, `rem`, etc.) o funciones de CSS (como `minmax()`, `repeat()`, etc.) para definir el ancho de las columnas. Además, puedes especificar el número de columnas y sus tamaños de manera más dinámica y flexible según tus necesidades de diseño.
En este caso el valor de `auto` va a ser el navegador el que escoja el valor que ocupe el contenedor en función del contenido del texto.

La propiedad `grid-auto-rows` en se utiliza para establecer el tamaño predeterminado de las filas que se crean automáticamente en una cuadrícula cuando no se especifica explícitamente un tamaño para ellas. Esto significa que grid-auto-rows define el tamaño de las filas que se generan automáticamente cuando se añaden más filas de las que se han especificado explícitamente en la definición de la cuadrícula.

Esta propiedad es útil cuando estás creando una cuadrícula con un número desconocido de elementos y quieres asegurarte de que las filas generadas automáticamente tengan un tamaño consistente. Puedes incluso darle un tamaño a la primera fila con `grid-template-rows: 100px`, y el resto generarlas con el auto.

## repeat()
La función `repeat()` es una forma de repetir un patrón de columnas (`grid-template-columns`) o filas (`grid-template-rows`) en una cuadrícula. Esto es especialmente útil cuando quieres definir un número repetitivo de columnas o filas con el mismo tamaño.

```css
.container{
    grid-template-rows: repeat(number_of_times, size);
}
```
- number_of_times: El número de veces que deseas repetir el patrón.
- size: El tamaño de cada repetición del patrón de columnas o filas.

También puedes combinar repeat() con otras funciones o valores para crear patrones más complejos. Por ejemplo, para crear una cuadrícula con dos filas de 100 píxeles y una fila automática, puedes hacer lo siguiente:
```css
.grid-container {
    display: grid;
    grid-template-rows: repeat(2, 100px) auto;
}
```

## minmax()

La función `minmax()` en es una función que permite especificar un rango mínimo y máximo para el tamaño de las columnas (`grid-template-columns`) o filas (`grid-template-rows`) en una cuadrícula. Esta función es especialmente útil cuando deseas que las columnas o filas tengan un tamaño flexible dentro de un rango dado.

```css
.container {
    grid-template-rows: minmax(min_value, max_value);
}
```

- min_value: Especifica el tamaño mínimo que puede tener la columna o fila.
- max_value: Especifica el tamaño máximo que puede tener la columna o fila.

También puedes combinar minmax() con otras funciones o valores para crear diseños más complejos. Por ejemplo, si deseas una cuadrícula con tres columnas, donde la primera columna tiene un tamaño mínimo de 100 píxeles y un tamaño máximo de 200 píxeles, y las otras dos columnas se expanden automáticamente para llenar el espacio restante, puedes hacer lo siguiente:

```css
.grid-container {
  display: grid;
  grid-template-columns: minmax(100px, 200px) 1fr 1fr;
}
```







# Ejemplo

```html
<div>
    <img src="" />
</div>

<style type="text/css">
    div {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        grid-column-gap 16px
    }

</style>



```























# Recursos:
- [Aprende CSS Grid jugando](https://cssgridgarden.com/#es)
- [GRID: A simple visual cheatsheet](https://grid.malven.co/)
- [A Complete Guide to CSS Grid ](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [CSS Grid CheatSheet](https://quickref.me/css3#css-grid-layout)
![CSS Grid CheatSheet 1](../IMG/css/grid-cheatsheet-1.png)
![CSS Grid CheatSheet 2](../IMG/css/grid-cheatsheet-2.png)
