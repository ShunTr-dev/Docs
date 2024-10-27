---
title: Preguntas entrevista de trabajo HTML
date: 2024-08-21 00:00:00 -100
categories: [HTML]
tags: [herramientas]
---

### 1. ¿Qué hace un doctype?

El `<!DOCTYPE>` en HTML le indica al navegador qué versión de HTML se está utilizando, ayudando a evitar problemas de renderizado. En HTML5, el doctype es `<!DOCTYPE html>`, y se utiliza para activar el "modo estándar" en lugar del "modo quirks", garantizando que las páginas se rendericen de manera coherente en todos los navegadores.

### 2. ¿Cómo sirves una página con contenido en varios idiomas?

Para servir una página multilingüe, se puede utilizar el atributo `lang` en la etiqueta `<html>` o en elementos específicos para identificar el idioma. Ejemplo: `<html lang="es">`. Además, puedes usar etiquetas `<link rel="alternate" hreflang="x">` para indicar versiones alternativas del contenido en otros idiomas.

### 3. ¿De qué debes tener cuidado al diseñar o desarrollar para sitios multilingües?

Al desarrollar sitios multilingües, hay que tener en cuenta:

-   Diferencias en la longitud de textos entre idiomas.
-   Direccionalidad del texto (por ejemplo, RTL en idiomas como árabe).
-   Formatos regionales para fechas, números y moneda.
-   Uso adecuado de `hreflang` para SEO.
-   Codificación correcta de caracteres (UTF-8) para admitir todos los idiomas.

### 4. ¿Para qué son útiles los atributos `data-`?

Los atributos `data-` permiten almacenar información personalizada en elementos HTML sin interferir con otros atributos o afectar el DOM. Son útiles para pasar datos a JavaScript o para almacenar configuraciones y valores dinámicos.

### 5. Considerando HTML5 como una plataforma web abierta, ¿cuáles son sus componentes fundamentales?

HTML5 se compone de varias tecnologías clave:

-   **Estructura y semántica:** Nuevas etiquetas semánticas como `<article>`, `<section>`, `<header>`, `<footer>`.
-   **Multimedia:** Etiquetas nativas como `<audio>` y `<video>`.
-   **Gráficos y visualización:** Soporte para `<canvas>` y SVG.
-   **APIs y almacenamiento:** Web Storage (localStorage y sessionStorage), Geolocation API, WebSockets.
-   **Formularios mejorados:** Nuevos tipos de input (`email`, `date`, etc.) y validación nativa.

### 6. Describe la diferencia entre una cookie, `sessionStorage` y `localStorage`.

-   **Cookies:** Se utilizan para almacenar pequeños datos en el navegador y son enviadas en cada solicitud HTTP. Tienen un tamaño limitado (alrededor de 4 KB) y se pueden configurar con una fecha de expiración.
-   **`sessionStorage`:** Almacena datos solo durante la sesión de la página. Los datos se eliminan cuando se cierra la pestaña o el navegador.
-   **`localStorage`:** Almacena datos de manera persistente, incluso si se cierra el navegador. Los datos permanecen hasta que se eliminan manualmente.

### 7. Describe la diferencia entre `<script>`, `<script async>` y `<script defer>`.

-   **`<script>`:** Los scripts son cargados y ejecutados inmediatamente, bloqueando la carga del contenido hasta que terminen de ejecutarse.
-   **`<script async>`:** Los scripts se cargan en paralelo al contenido de la página y se ejecutan tan pronto como se descargan. No se garantiza un orden específico si hay varios scripts.
-   **`<script defer>`:** Los scripts se cargan en paralelo, pero su ejecución se retrasa hasta que toda la página haya sido completamente cargada. Se ejecutan en el orden en que aparecen en el HTML.

### 8. ¿Por qué generalmente es una buena idea colocar las etiquetas CSS `<link>` entre `<head></head>` y las etiquetas JS `<script>` justo antes de `</body>`? ¿Conoces alguna excepción?

Colocar los enlaces CSS en `<head>` asegura que los estilos se carguen antes de renderizar la página, evitando un "parpadeo" sin estilos. Colocar los scripts JS al final permite que el contenido se cargue antes de que los scripts puedan bloquear la renderización. Una excepción puede ser si se necesita un script crítico para la interfaz (por ejemplo, scripts que afectan la estructura inicial).

### 9. ¿Qué es el renderizado progresivo?

El renderizado progresivo implica mostrar contenido tan pronto como esté disponible, en lugar de esperar a que toda la página se cargue. Esto mejora la experiencia del usuario, especialmente en conexiones lentas, al permitirles ver partes del contenido mientras otros recursos siguen cargándose.

### 10. ¿Por qué usarías el atributo `srcset` en una etiqueta de imagen? Explica el proceso que usa el navegador al evaluar su contenido.

El atributo `srcset` permite especificar diferentes versiones de una imagen para distintas resoluciones o anchos de pantalla. El navegador selecciona la imagen más adecuada según el dispositivo del usuario, mejorando el rendimiento y la calidad visual. Evalúa `srcset` basándose en las reglas dadas y en la densidad de píxeles del dispositivo.

### 11. ¿Has usado diferentes lenguajes de plantillas HTML?

Sí, lenguajes como Pug, Handlebars y EJS son ejemplos comunes. Estos lenguajes permiten escribir plantillas HTML más dinámicas, con sintaxis simplificada, variables, y lógica condicional, facilitando la generación de contenido en aplicaciones.

### 12. ¿Cuál es la diferencia entre canvas y SVG?

-   **Canvas:** Utiliza un lienzo bitmap para dibujar gráficos 2D mediante JavaScript. Es más adecuado para gráficos complejos y en tiempo real, como juegos.
-   **SVG:** Usa gráficos vectoriales escalables basados en XML. Es mejor para gráficos estáticos y escalables como logos, diagramas e iconos.

### 13. ¿Qué son los elementos vacíos en HTML?

Los elementos vacíos son etiquetas que no requieren un contenido o etiqueta de cierre. Ejemplos comunes son `<img>`, `<input>`, `<br>`, y `<meta>`. Estos elementos no pueden contener texto ni otros elementos dentro de ellos.

### Referencias

[Front-end-Developer-Interview-Questions](https://github.com/h5bp/Front-end-Developer-Interview-Questions/blob/main/src/questions/html-questions.md)
