# CSS Transitions y CSS Effects

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

- **Propiedad:** Indica qué propiedad CSS se animará durante la transición, como `color`, `width`, `height`, etc.
- **Duración:** Especifica la duración de la transición en segundos (s) o milisegundos (ms).
- **Función de tiempo:** Define cómo cambia la velocidad de la transición a lo largo del tiempo. Pueden ser funciones predefinidas como `ease`, `ease-in`, `ease-out`, `ease-in-out`, `linear`, o funciones de temporización personalizadas.

## Ejemplo de uso

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
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

- **Mejora la experiencia del usuario:** Las transiciones suaves hacen que la interacción con la página web sea más agradable y atractiva.
- **Fácil de implementar:** Se pueden aplicar fácilmente con solo unas pocas líneas de código CSS.
- **Personalización:** Se pueden ajustar la duración y la función de tiempo para adaptarse a las necesidades específicas de diseño.

## Conclusión

Las transiciones CSS son una herramienta poderosa para agregar dinamismo y mejorar la estética de las páginas web. Con un poco de conocimiento sobre cómo funcionan y un uso adecuado, se pueden crear efectos de animación impresionantes que mejoren la experiencia del usuario.






































Animaciones CSS3
```
#caja {
    animation-name: desplazamiento;
    animation-duration: 10;
    animation-iteration-count: infinite;
    animation-timing-function: linear;
}


@keyframes desplazamiento {
    from {
        margin-left: 0px;
    }
    to {
        margin-left: 100px;
    }
    /* Se puede hacer con porcentajes */
}
```






Ejemplos chorra

Hacer girar un engranaje

```
#logo {
    animation-name: rotate-gear;
    animation-duration: 10;
    animation-iteration-count: infinite;
    animation-timing-function: linear;
}

/* hacer que gire */
@keyframes desplazamiento {
    from {
        transform:rotateZ(0deg);
    }
    to {
        transform:rotateZ(360deg);
    }
}

/* hacer que cuando se entre en el div cambien los atributos */
#logo:hover {
    border-radius:2px;
    color: black;
    backgroud-color: #ccc;
}

/* */
#logo:hover .gear {
    animation: fromBellow 500ms lineal;
}

@keyframes fromBellow {
    0% {
        transform:translateY(0%); /* hay que poner un overflow hidden, si no se verá fuera del div*/
    }
    
    50% {
        transform:translateY(200%);
    }
    100% {
        transform:translateY(0%);
    }
}
```