Le puedes poner un float a todos los elementos que su display sea block
clear limpia los floats
```
<div class="clearfix"></div>

.clearfix {
    float:none;
    clear: both;
}
```

o usar inline-block

POSICIONAMIENTO RELATIVO ABSOLUTO Y FIJO
```
overflow: hidden; (se oculta lo que salga del div)
overflow: visible;
overflow: scroll;
```

POSICIÓN ABSOLUTA
```
/* position: relative; (Por defecto) */
position: absolute; /* Fulmina todo lo que hay antes y cuando se le mete algo se puede poner como quieras */
top: 0px; /* se pone arriba de todo*/
```

POSICIÓN FIJA
```
position: fixed; /* como la posición absoluta pero se mantiene aunque hagamos scroll*/
```