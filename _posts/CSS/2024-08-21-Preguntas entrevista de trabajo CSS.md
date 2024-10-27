---
title: Preguntas entrevista de trabajo CSS
date: 2024-08-21 00:00:00 -100
categories: [CSS]
tags: [herramientas]
---

Aquí tienes las traducciones y respuestas a las preguntas en castellano:

### 1. ¿Qué es la especificidad de los selectores en CSS y cómo funciona?

La especificidad determina qué estilo se aplicará a un elemento cuando múltiples reglas de CSS coinciden. Funciona otorgando puntos según el tipo de selector: los selectores de ID son más específicos que los de clase, y estos últimos son más específicos que los selectores de etiqueta. Cuanto mayor es la especificidad, mayor prioridad tiene el estilo.

### 2. ¿Cuál es la diferencia entre "resetear" y "normalizar" CSS? ¿Cuál elegirías y por qué?

Resetear CSS elimina todos los estilos predeterminados del navegador, mientras que normalizar CSS ajusta esos estilos para hacerlos más consistentes entre navegadores. Normalizar es preferible en la mayoría de los casos, ya que mantiene ciertas convenciones útiles y reduce inconsistencias.

### 3. Describe cómo funcionan los floats.

Los floats permiten que un elemento se alinee a la izquierda o derecha dentro de su contenedor, permitiendo que el texto o contenido contiguo lo rodee. Los elementos flotantes salen del flujo normal del documento y requieren técnicas especiales para limpiar o evitar problemas de contenedor colapsado.

### 4. Describe el z-index y cómo se forma un contexto de apilamiento.

El `z-index` controla el orden de apilamiento (qué elemento se superpone a otro) en el eje z. Un contexto de apilamiento se crea en ciertos elementos (como aquellos con posición relativa, absoluta o fixed) y afecta cómo los hijos se superponen dentro de ese contexto.

### 5. Describe el BFC (Block Formatting Context) y cómo funciona.

El BFC es una propiedad del diseño en CSS que controla cómo se comportan los elementos dentro de un contenedor. Los elementos en un BFC no se superan con otros elementos flotantes y pueden contener correctamente los elementos flotantes. Un BFC se puede activar con propiedades como `overflow: hidden` o `display: flow-root`.

### 6. ¿Cuáles son las técnicas de limpieza (clearing) y cuál es adecuada para cada contexto?

Las técnicas comunes incluyen el uso de un elemento vacío con `clear: both`, el uso de `overflow: hidden` en el contenedor o la técnica de clearfix mediante pseudo-elementos. `clearfix` es generalmente la mejor opción para contenedores que necesitan adaptarse dinámicamente.

### 7. ¿Cómo abordarías la corrección de problemas de estilo específicos del navegador?

Identificaría los problemas usando herramientas como `Can I Use`, consultaría las herramientas de desarrollo de los navegadores y utilizaría hacks o prefijos específicos cuando sea necesario, aunque en última instancia priorizaría soluciones que funcionen en todos los navegadores.

### 8. ¿Cómo servirías tus páginas para navegadores con restricciones de funciones?

Usaría estrategias como progressive enhancement (mejora progresiva) y graceful degradation (degradación elegante), además de incluir polyfills o cargar estilos alternativos.

### 9. ¿Cuáles son las diferentes maneras de ocultar contenido visualmente (y que esté disponible solo para lectores de pantalla)?

Puedes usar `visibility: hidden`, `opacity: 0`, `position: absolute; left: -9999px` o la técnica `clip-path`. El uso de `sr-only` es común para accesibilidad.

### 10. ¿Has usado un sistema de grid? ¿Cuál prefieres?

Sí, se pueden usar sistemas de grid como Bootstrap o CSS Grid nativo. La preferencia depende del proyecto, pero CSS Grid ofrece mayor flexibilidad y control para diseños complejos.

### 11. ¿Has utilizado o implementado media queries o layouts/CSS específicos para móviles?

Sí, los media queries permiten adaptar el diseño a diferentes tamaños de pantalla. Se pueden usar para layouts responsive o enfoques mobile-first.

### 12. ¿Estás familiarizado con el estilo de SVG?

Sí, puedes estilizar SVG usando CSS o atributos dentro del archivo SVG. Las propiedades como `fill`, `stroke` y `transform` son comunes.

### 13. ¿Puedes dar un ejemplo de una propiedad `@media` diferente a `screen`?

Sí, `@media print` se usa para estilos destinados a la impresión. Otros ejemplos incluyen `speech` para lectores de pantalla.

### 14. ¿Cuáles son algunos de los "gotchas" al escribir CSS eficiente?

Evitar reglas redundantes, minimizar el uso de selectores universales (`*`), y evitar la sobreespecificidad son claves para un CSS eficiente.

### 15. ¿Cuáles son las ventajas/desventajas de usar preprocesadores CSS?

Los preprocesadores como SASS o LESS permiten el uso de variables, mixins y funciones, lo que facilita la organización. Sin embargo, pueden añadir complejidad y requerir configuración adicional.

### 16. ¿Cómo implementarías un diseño web que use fuentes no estándar?

Utilizaría `@font-face` o fuentes web como Google Fonts. Es importante incluir formatos alternativos para mayor compatibilidad.

### 17. Explica cómo un navegador determina qué elementos coinciden con un selector CSS.

El navegador lee los selectores de derecha a izquierda. Evalúa qué elementos coinciden con el selector más específico y luego verifica los elementos padres según el selector.

### 18. Describe los pseudo-elementos y para qué se usan.

Los pseudo-elementos como `::before` y `::after` permiten añadir contenido decorativo sin modificar el HTML. Se usan para estilos adicionales como iconos o efectos visuales.

### 19. Explica tu comprensión del modelo de caja y cómo decirle al navegador que renderice en diferentes modelos.

El modelo de caja define cómo se calculan los tamaños de los elementos con `padding`, `border` y `content`. Puedes cambiar el comportamiento usando `box-sizing: border-box` para incluir `padding` y `border` en el tamaño total.

### 20. ¿Qué hace `* { box-sizing: border-box; }`? ¿Cuáles son sus ventajas?

Cambia el cálculo del tamaño de todos los elementos para que `padding` y `border` se incluyan en el tamaño declarado, evitando desbordamientos y simplificando el diseño.

### 21. ¿Qué es la propiedad `display` en CSS y puedes dar ejemplos de su uso?

`display` controla cómo se presentan los elementos. Ejemplos incluyen `block`, `inline`, `inline-block`, `flex` y `grid`.

### 22. ¿Cuál es la diferencia entre `inline` e `inline-block`?

`inline` no respeta el `width` ni `height`, mientras que `inline-block` permite establecer esas propiedades pero mantiene el flujo en línea.

### 23. ¿Cuál es la diferencia entre los selectores `nth-of-type()` y `nth-child()`?

`nth-of-type()` selecciona el enésimo hijo de un tipo específico de elemento, mientras que `nth-child()` selecciona el enésimo hijo independientemente de su tipo.

### 24. ¿Cuál es la diferencia entre un elemento posicionado relativamente, fijo, absolutamente y estáticamente?

-   **Static:** Posición predeterminada.
-   **Relative:** Desplazado relativo a su posición normal.
-   **Absolute:** Posicionado respecto al contenedor posicionado más cercano.
-   **Fixed:** Posicionado respecto a la ventana del navegador y permanece fijo al desplazarse.

### 25. ¿Qué frameworks CSS has utilizado y cómo los mejorarías?

Frameworks como Bootstrap y Tailwind se utilizan ampliamente. Pueden mejorarse personalizando la configuración o reduciendo el CSS no utilizado para optimizar el rendimiento.

### 26. ¿Has usado CSS Grid?

Sí, CSS Grid es útil para layouts bidimensionales complejos, permitiendo un control preciso sobre filas y columnas.

### 27. ¿Puedes explicar la diferencia entre codificar un sitio para ser responsive frente a usar una estrategia mobile-first?

La codificación responsive adapta el diseño según el tamaño de pantalla, mientras que mobile-first implica diseñar para móviles primero y luego escalar para pantallas más grandes.

### 28. ¿Has trabajado con gráficos retina? ¿Cuándo y qué técnicas usaste?

Sí, gráficos retina se utilizan para dispositivos con alta densidad de píxeles. Técnicas incluyen usar imágenes SVG o servir imágenes de mayor resolución con `srcset`.

### 29. ¿Hay alguna razón por la que querrías usar `translate()` en lugar de posicionamiento absoluto, o viceversa?

`translate()` no afecta el flujo del documento y es más eficiente para animaciones. El posicionamiento absoluto se usa cuando se necesita que el elemento esté fuera del flujo normal.

### 30. ¿Cómo es útil la propiedad clearfix?

Clearfix se utiliza para contener elementos flotantes dentro de su contenedor sin colapsar. Utiliza pseudo-elementos para agregar un clear después del contenido flotante.

### 31. ¿Puedes explicar la diferencia entre `px`, `em` y `rem` en relación con el tamaño de fuente?

-   **px:** Tamaño absoluto, independiente de la configuración del usuario.
-   **em:** Relativo al tamaño de la fuente del elemento padre.
-   **rem:** Relativo al tamaño de la fuente raíz (`html`).

### 32. ¿Puedes dar un ejemplo de una pseudo-clase? ¿Un caso de uso?

Un ejemplo es `:hover`, que aplica estilos cuando el cursor está sobre un elemento. Es útil para efectos interactivos en botones o enlaces.

### 33. ¿Cuál es la diferencia entre un elemento de nivel bloque y un elemento en línea? ¿Puedes dar ejemplos de cada tipo?

-   **Bloque:** Ocupa todo el ancho disponible y empieza en una nueva línea (ej., `div`, `p`).
-   **En línea:** Solo ocupa el ancho necesario y no inicia una nueva línea (ej., `span

`, `a`).

### 34. ¿Cuál es la diferencia entre CSS Grid y Flexbox? ¿Cuándo usarías uno sobre el otro?

Flexbox es mejor para layouts unidimensionales (filas o columnas), mientras que CSS Grid es para layouts bidimensionales más complejos (filas y columnas simultáneamente).

### 35. ¿Cuál es la diferencia entre layouts fijos, fluidos y responsivos?

-   **Fijo:** Tamaño definido y no cambia con el viewport.
-   **Fluido:** Usa unidades relativas y se ajusta al tamaño del viewport.
-   **Responsivo:** Combina ambos con media queries para adaptar el diseño a diferentes dispositivos.

### Referencias

[Front-end-Developer-Interview-Questions](https://github.com/h5bp/Front-end-Developer-Interview-Questions/blob/main/src/questions/css-questions.md)
