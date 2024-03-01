SelectoresSelector universal. Toma todos los elementos del documento
```
* {
    font-family: Verdana, Geneva;
}
```

Selector de etiqueta
```
h1 {
    background: red;
}

footer a {
    //selecciona los enlaces del footer
}
```

Selector de identificador
```
<div id="description"></div>

#description {
    border 1px solid black;
}

#titulo, #description {
    border 1px solid black;
}

#usuario form {
    border: 5px solid blue;
}

#usuario form * {
    display: block;
}
```

Selector de clase
```
<p class="parrafo"></p>

.parrafo {
    font-style: italic;
}
```

Selector de atributo
```
input[type="text"] {
    width: 200px;
}

input[type="submit"] {
    width: 200px;
}
```

Selector hijo
```
/*Se le pone a los elementos después del marcador */
#menu > li > a {
    color: red;
}
```