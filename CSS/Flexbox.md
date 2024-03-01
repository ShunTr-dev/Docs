VARIABLES
:root {
	--rojo: red;
}

.rojo {
	var(--rojo);
}


Lo principal es que flexbox es como flotar las cosas pero sin salirse del container como pasa en el float
Con flexbox hay que escoger la caja donde se va a usar.
display: flex, ocupa todo lo que puede
display: inline-flex, se adapta al contenido que tiene dentro

Si lo elementos son muchos y se salen del contenedor podemos hacer un wrap para que salten abajo
Los elementos se pueden ordenar con order

S1 ponemos flex-grow dento de las cajas podemos darle tamaño a los elementos si lo ponemos a 1 significa que todos van a tener el mismo tamaño
Se pueden poner tamaños diferentes para asignar tamaños diferentes
Con flex-shrik reduces el tamaño

flex-basis: calc(100% / 3);

justify-content: localiza las posiciones de los containers en el flex /*alineación horizontal */
align-items: alineación vertical



FLEXBOX CHEATSHEET----------------------------