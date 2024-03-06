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