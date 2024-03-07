# FLEXBOX

CSS Flexbox (Flexible Box Layout) es un módulo de CSS que proporciona un método más eficiente y predecible para diseñar y distribuir elementos dentro de un contenedor, incluso cuando el tamaño de los elementos y del contenedor es desconocido o dinámico. Flexbox ofrece un sistema de diseño unidimensional, lo que significa que se centra en el diseño de una fila o columna de elementos a la vez.

Algunas características y ventajas clave de Flexbox incluyen:

- Diseño flexible y dinámico: Permite a los elementos dentro de un contenedor ajustarse automáticamente según el tamaño del contenedor y el tamaño de los elementos, lo que facilita la creación de diseños adaptables y responsivos.

- Ordenamiento de elementos: Los elementos pueden ser reorganizados fácilmente en función del diseño deseado, independientemente de su orden en el HTML.

- Alineación y distribución: Proporciona varias propiedades para alinear y distribuir elementos dentro de un contenedor, como alinear al centro, alinear a la izquierda, distribuir uniformemente, etc.

- Espaciado flexible: Ofrece un control preciso sobre el espacio entre los elementos, tanto dentro como fuera del contenedor.

- Nesting (Anidamiento) simplificado: Los contenedores flexibles se pueden anidar dentro de otros contenedores flexibles, lo que facilita la creación de diseños complejos y jerárquicos.

- Compatibilidad multiplataforma: Flexbox es compatible con la mayoría de los navegadores modernos, lo que lo convierte en una opción sólida para el diseño de interfaces de usuario en la web.

En resumen, CSS Flexbox es una poderosa herramienta de diseño que simplifica la creación de diseños flexibles y responsivos en la web, ofreciendo un mayor control sobre la disposición y distribución de los elementos en una página.













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