---
title: CSS transitions y CSS Animations
date: 2020-01-01 00:00:00 -100
categories: [CSS]
tags: [css]     # TAG names should always be lowercase
---


# CSS Transitions

## CSS Transitions

Las transiciones CSS son una técnica utilizada para animar cambios en las propiedades de los elementos HTML. Permiten suavizar la transición entre un **estado inicial** y un **estado final**, creando efectos visuales más atractivos y dinámicos.

## Funcionamiento

Las transiciones CSS se definen mediante la propiedad `transition`, que se aplica a los elementos HTML que se desean animar. Esta propiedad especifica qué propiedades CSS se animarán, la duración de la transición y la función de temporización que se utilizará para controlar la velocidad de la animación.

```css
/* Ejemplo de uso de la propiedad transition */
.element {
    transition: propiedad duración función-de-tiempo;
}
```

-   **Propiedad:** Indica qué propiedad CSS se animará durante la transición, como `color`, `width`, `height`, etc.
-   **Duración:** Especifica la duración de la transición en segundos (s) o milisegundos (ms).
-   **Función de tiempo:** Define cómo cambia la velocidad de la transición a lo largo del tiempo. Pueden ser funciones predefinidas como `ease`, `ease-in`, `ease-out`, `ease-in-out`, `linear`, o funciones de temporización personalizadas.

## Ejemplo de uso

```html
<!DOCTYPE html>
<html lang="es">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Transiciones CSS</title>
        <style>
            /* Estilos de la caja */
            .caja {
                width: 100px;
                height: 100px;
                background-color: blue;
                transition: width 1s ease-in-out;
            }
            /* Cambio de color en hover */
            .caja:hover {
                width: 200px;
                background-color: red;
            }
        </style>
    </head>
    <body>
        <div class="caja"></div>
    </body>
</html>
```

En este ejemplo, cuando pasas el cursor sobre la caja, la propiedad `width` cambia de 100px a 200px con una transición suave de 1 segundo, mientras que el color de fondo cambia de azul a rojo.

## Ventajas

-   **Mejora la experiencia del usuario:** Las transiciones suaves hacen que la interacción con la página web sea más agradable y atractiva.
-   **Fácil de implementar:** Se pueden aplicar fácilmente con solo unas pocas líneas de código CSS.
-   **Personalización:** Se pueden ajustar la duración y la función de tiempo para adaptarse a las necesidades específicas de diseño.

## `transition-duration`

La propiedad `transition-duration` en se utiliza para especificar la duración de la transición animada entre dos estados de un elemento. Puede ser un número positivo seguido de una unidad de tiempo, como segundos (s) o milisegundos (ms).

```html
<div class="pulser"></div>

<style type="text/css">
    .pulser {
        width: 50px;
        height: 50px;
        background: #09f;
        border-radius: 50%;
        position: relative;
        transition-duration: 2s;
    }

    .pulser:hover {
        scale: 2;
        background: purple;
        box-shadow: 0 0 10px purple;
        /* En este caso poner el transition en el hover no tiene sentido, ya que cuando se saliese de este estado, volvería a las propiedades iniciales SIN animación */
    }

    body {
        display: grid;
        place-content: center;
        min-height: 50vh;
    }
</style>
```

Con la propiedad `transition-property` podríamos especificar qué propiedades CSS deben ser animadas durante una transición. En este ejemplo podríamos poner `transition-property: scale;` Para que solamente se animara la escala. Esto viene bien por que por defecto viene con `transition-property: all;`y esto tiene un coste importante en el rendimiento en la web, sobretodo en el tema shadows.

## `transition-delay`

La propiedad `transition-delay` se utiliza para especificar el tiempo de espera antes de que comience una transición. Esto permite controlar cuándo se activará la transición después de que se haya producido un cambio en las propiedades CSS del elemento.

```css
/* Se aplica una transición con un retraso de 0.5 segundos */
.elemento {
    transition-delay: 0.5s;
}
```

## `transition-timing-function`

La propiedad `transition-timing-function` se utiliza para especificar cómo cambia la velocidad de la transición entre los estados inicial y final de un elemento animado. Esta propiedad define la función de temporización que controla la aceleración y desaceleración de la animación durante su ejecución.

### Funciones de temporización predefinidas:

1. **ease:** Inicia lentamente, luego acelera y finaliza lentamente.
2. **ease-in:** Inicia lentamente y luego acelera.
3. **ease-out:** Inicia rápidamente y luego desacelera.
4. **ease-in-out:** Inicia lentamente, acelera, luego desacelera al final.
5. **linear:** La animación avanza a una velocidad constante.

### `steps()`

La función `steps()` en `transition-timing-function` se utiliza para crear una animación de transición con pasos en lugar de una animación continua y fluida. Esta función permite dividir la transición en un número específico de pasos, dando la impresión de que la animación avanza en incrementos definidos.

```css
transition-timing-function: steps(n, start|end);
```

-   **n:** Número entero que especifica la cantidad de pasos en la transición.
-   **start|end:** Especifica dónde se ubicarán los puntos de inicio o finalización de cada paso. `start` indica que los valores cambiarán al inicio de cada paso, mientras que `end` indica que los valores cambiarán al final de cada paso.

### `cubic-bezier()`

La función `cubic-bezier()` en la propiedad `transition-timing-function` permite crear funciones de temporización personalizadas para controlar la velocidad de una transición animada de manera más precisa. Esta función utiliza la interpolación de curvas cúbicas de Bézier para definir la aceleración y desaceleración de la animación en diferentes puntos de su duración.

```css
transition-timing-function: cubic-bezier(x1, y1, x2, y2);
```

-   **x1, y1, x2, y2:** Coordenadas de control que definen la forma de la curva cúbica de Bézier. Estos valores deben estar en el rango de 0 a 1.

Dentro de las herramientas de desarrollador puedes crear la animación tuya persinalizada sin tener que preocuaparte de hacerla a mano.

Para ver las diferencias entre todo este tipo de animaciones se puede acudir a esta [web](https://easings.co/)

## `transition`

`transition` es la forma acortada de unir todas las propiedades en una línea.

```css
selector {
    transition: propiedad duración tipo [retraso];
}
```

-   **selector:** Especifica el elemento al que se aplicará la transición.
-   **propiedad:** Indica qué propiedad CSS deseas animar durante la transición.
-   **duración:** Especifica la duración de la transición en segundos (s) o milisegundos (ms).
-   **tipo:** Define cómo cambia la velocidad de la transición a lo largo del tiempo. Puede ser `ease`, `ease-in`, `ease-out`, `ease-in-out`, `linear`, o una función de temporización personalizada.
-   **retraso (opcional):** Especifica un tiempo de espera antes de que comience la transición.

```css
/* Aplica una transición en el color de fondo con una duración de 1 segundo */
.elemento {
    transition: background-color 1s ease-in-out;
}

.otro-elemento {
    transition: background 300ms linear, scale 500ms ease-in-out, box-shadow 1s ease;
}
```

## `@media prefers-reduced-motion`

La regla `@media prefers-reduced-motion` en CSS es una forma de consultar si el usuario prefiere reducir o deshabilitar las animaciones y transiciones en una página web debido a condiciones como la sensibilidad a los movimientos o el consumo de recursos.

```css
/* Estilos predeterminados */
.elemento {
    transition: background-color 0.5s ease-in-out;
}

/* Estilos para usuarios que prefieren reducir el movimiento */
@media (prefers-reduced-motion: reduce) {
    .elemento {
        transition: none; /* Desactiva todas las transiciones */
    }
}
```

# CSS Animations

Las animaciones permiten crear efectos visuales dinámicos y atractivos sin necesidad de usar JavaScript. Con CSS, puedes definir keyframes que especifican cómo cambian las propiedades de un elemento a lo largo del tiempo, lo que te permite crear animaciones personalizadas y controladas.

### Sintaxis básica:

1. Define los keyframes utilizando la regla `@keyframes`. Los keyframes especifican los estados de la animación en diferentes puntos en el tiempo.

    ```css
    @keyframes nombre-de-la-animacion {
        0% {
            /* también se puede poner from */
            /* Estilos en el inicio de la animación */
        }
        100% {
            /* también se puede poner to */
            /* Estilos en el final de la animación */
        }
    }
    ```

2. Aplica la animación al elemento deseado utilizando la propiedad `animation`. Puedes especificar la duración, el nombre de la animación, el tipo de temporización y más.

    ```css
    selector {
        animation: nombre-de-la-animacion duracion [tipo] [retraso] [iteracion] [direccion] [relleno];
    }
    ```

    - **nombre-de-la-animacion:** El nombre de los keyframes definidos previamente.
    - **duracion:** La duración de la animación en segundos (s) o milisegundos (ms).
    - **tipo (opcional):** El tipo de temporización de la animación, como `ease`, `ease-in`, `ease-out`, `ease-in-out`, `linear`, etc.
    - **retraso (opcional):** El tiempo de espera antes de que comience la animación.
    - **iteracion (opcional):** El número de veces que se repite la animación, o `infinite` para repetirla indefinidamente.
    - **direccion (opcional):** La dirección de la animación, como `normal`, `reverse`, `alternate`, etc.
    - **relleno (opcional):** Controla cómo se aplican los estilos al elemento antes y después de la animación.

```css
/* Definición de keyframes */
@keyframes mover {
    0% {
        transform: translateX(0);
    }
    50% {
        transform: translateX(100px);
    }
    100% {
        transform: translateX(200px);
    }
}

/* Aplicación de la animación */
.elemento {
    animation: mover 2s ease-in-out infinite alternate;
}
```

En este ejemplo, se define una animación llamada `mover` que desplaza el elemento horizontalmente a lo largo de tres etapas. Luego, se aplica esta animación al elemento `.elemento` con una duración de 2 segundos, temporización `ease-in-out`, repetición infinita en dirección alterna.

### Ventajas:

-   **Sin JavaScript:** Las animaciones en CSS permiten agregar interactividad y dinamismo a una página web sin necesidad de usar JavaScript.
-   **Mejora del rendimiento:** Las animaciones en CSS suelen ser más eficientes que las animaciones en JavaScript, ya que aprovechan la aceleración por hardware del navegador.
-   **Facilidad de uso:** Con una sintaxis simple, las animaciones en CSS son fáciles de implementar y mantener.

## Ejemplo de pulser

```html
<div class="pulser"></div>

<style type="text/css">
    .pulser {
        width: 50px;
        height: 50px;
        background: #09f;
        border-radius: 50%;
        position: relative;
    }

    .pulser::after {
        content: '';
        position: absolute;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        background: #09f;
        boder-radius: 50%;
        z-index: -1;
        scale: 2;
        opacity: 0.5;

        animation-name: pulse;
        animation-duration: 2s;
        animation-delay: 1s;
        animation-timing-function: ease-in-out;
        animation-iteration-count: infinite;
    }

    @keyframes pulse {
        0% {
            opacity: 0;
        }

        50% {
            scale: 2;
            opacity: 40%;
        }

        100% {
            opacity: 100%;
        }
    }

    .pulser:hover {
        scale: 2;
        background: purple;
        box-shadow: 0 0 10px purple;
        /* En este caso poner el transition en el hover no tiene sentido, ya que cuando se saliese de este estado, volvería a las propiedades iniciales SIN animación */
    }

    body {
        display: grid;
        place-content: center;
        min-height: 50vh;
    }
</style>
```

## `animation-fill-mode`

La propiedad `animation-fill-mode` es una propiedad que especifica cómo se aplicarán los estilos al elemento objetivo antes y después de que se ejecute la animación. Esta propiedad determina si el elemento mantiene los estilos aplicados al final de la animación o si vuelve a su estado original.

-   **valor:** Puede ser uno de los siguientes:
    -   `none`: No se aplican estilos al elemento antes o después de la animación.
    -   `forwards`: Los estilos del último keyframe se mantienen aplicados al elemento después de la animación.
    -   `backwards`: Los estilos del primer keyframe se aplican al elemento antes de que comience la animación.
    -   `both`: Se aplican los estilos del primer keyframe antes de que comience la animación y los estilos del último keyframe después de que finalice la animación.

```css
/* Aplica estilos del primer keyframe antes de la animación y del último keyframe después de la animación */
.elemento {
    animation-name: animacion;
    animation-duration: 2s;
    animation-fill-mode: both;
}

@keyframes animacion {
    0% {
        opacity: 0;
    }
    100% {
        opacity: 1;
    }
}
```

# Enlaces

-   [Scroll driven animations](https://scroll-driven-animations.style/)
