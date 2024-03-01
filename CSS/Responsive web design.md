usar %

MEDIA QUERIES
```
/* Desde la anchura de 632px hasta la anchura 888px hasta de pantalla tienen prioridad estos estilos */
@media (max-width: 888px){
    #articles {
        bacground-color: red;
    }
}

@media (max-width: 632px){
    #articles {
        bacground-color: blue;
    }
}
```

VIEWPORT
Poner la etiqueta en el header
```
<meta name="viewport" content="width=device-width, user-scalable=no" />
```