---
title: Optimizar web
date: 2024-08-20 00:00:00 -100
categories: [Herramientas]
tags: [herramientas]
---

# Herramientas para optimizar tu web

## [SQUOOSH](https://squoosh.app/)

Optimiza imágenes para que tu web cargue más rápido

-   Usa formatos más modernos
-   Redimensiona tu imagen
-   Reduce calidad para reducir el peso
-   Desarrollado por Google

## [The Front-End Checklist](https://frontendchecklist.io/)

Esta página ofrece una lista detallada de tareas para:
✓ Mejorar tu HTML, CSS y JavaScript
✓ Revisar SEO, Rendimiento y la Accesibilidad
✓ Carga de fuentes e imágenes de tu web

## [CSS code Quality ](https://www.projectwallace.com/css-code-quality)

Analiza la calidad de tu código CSS.
Rendimiento, buenas prácticas y mantenibilidad.
Detecta el código y te da consejos para arreglarlo.

## [Cruxvis](https://cruxvis.withgoogle.com/#/)
Página de google para ver los core web vitals.
Para ver la experiencia de los usuarios.

## Lista para mejorar la velocidad de tu web:

1. Carga sólo el JavaScript y CSS que necesitas.

Para saber si eso es un problema, puedes usar la pestaña de Cobertura en las DevTools.

Esta pestaña está un poco oculta, pero te dice el % de uso de tus archivos.

Al darle a un archivo, te muestra las líneas que se usan:

Captura de Code Coverage para ver en las DevTools cuanto JavaScript y CSS se usa 2. Carga diferida de dependencias

Utiliza imports dinámicos para cargar bibliotecas sólo cuando las necesitas.

Si algo sólo se necesita tras la interacción del usuario...
¡Entonces cárgalo sólo ahí y no desde el principio!

Un ejemplo con código JavaScript:

Código de JavaScript donde se usa un import dinámico para cargar la dependencia de canvas-confetti al hacer clic en un botón 3. Optimiza tus imágenes

Usa formato y tamaños adecuados para tus imágenes:

-   webp o avif siempre que puedas
-   Haz imágenes responsive y cargar según el dispositivo
-   Usa SVG para iconos e imágenes vectoriales
-   Evita PNG siempre que puedas

→ Usa squoosh․app como herramienta

4. Usa la plataforma web
   Evita usar dependencias grandes o innecesarias:

-   Busca alternativas más pequeñas (lodash vs just)
-   Favorece soluciones nativas (axios vs fetch)

Con bundlephobia entiendes el coste que tiene:
→ bundlephobia․com

5. Favorece CSS en lugar de JavaScript
   CSS ha mejorado muchísimo y cada vez es más potente.
   Hoy en día puedes hacer ciertos sliders y UIs sin JS.

Revisa y aprende a usar CSS ya que:

-   La solución ocupa menos que JS normalmente
-   La evaluación es mucho más rápida
-   No bloqueará el hilo principal
-   Mejor UX

6. Carga diferida de imágenes
   Usa la etiqueta nativa lazy de imágenes e iframes para cargarlas sólo cuando el usuario las necesita.

¡Ojo! Usa esta técnica para imágenes que sabes que no están en pantalla desde el principio.

```html
<img loading="lazy" src="imagen.webp" alt="..." />
```

7. Cuantas menos fuentes, mejor
   Las fuentes son críticas para mostrar nuestra web.
   Si puedes, usa sólo fuentes del sistema.
   Si no usa el mínimo número necesario...
   ¡Y siempre con formato woff2 y desde tu dominio!

No uses Google Fonts para cargar tus fuentes.
Google Fonts puede ser buena idea para probar algo... ¡Pero no es lo más óptima en cuanto a rendimiento!
Lo mejor es hospedarlas en tu sitio.

8. Evita mostrar un loader al principio
   A veces ponemos una pantalla de carga al inicio.
   ¡Esto es fatal para la percepción de carga del usuario!

Optimiza tu web para que se renderice en el servidor y pueda mostrar información útil desde el inicio.
