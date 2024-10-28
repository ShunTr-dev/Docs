---
title: Etiquetas nuevas
date: 2024-08-20 00:00:00 -100
categories: [HTML]
tags: [etiquetas, html, label]
---

# Etiquetas nuevas

## `<picture>`

La etiqueta `<picture>` se utiliza para proporcionar diferentes versiones de una imagen con el fin de adaptarse a diferentes condiciones de visualización, como el tamaño de la pantalla o la resolución del dispositivo. Esto permite a los desarrolladores web mejorar la experiencia del usuario al servir imágenes optimizadas para cada situación.

La estructura básica de la etiqueta `<picture>` incluye una o más etiquetas `<source>` que especifican las diferentes versiones de la imagen, y una etiqueta `<img>` como respaldo en caso de que ninguna de las fuentes especificadas sea compatible.

```html
<picture>
    <source srcset="imagen-grande.jpg" media="(min-width: 800px)" />
    <source srcset="imagen-pequeña.jpg" media="(max-width: 799px)" />
    <img src="imagen-pequeña.jpg" alt="Descripción de la imagen" />
</picture>
```

En este ejemplo, se proporcionan dos versiones de la imagen: una para pantallas grandes y otra para pantallas más pequeñas. El navegador seleccionará automáticamente la imagen más adecuada según la resolución y el tamaño de la pantalla del dispositivo. Si ninguna de las fuentes especificadas es compatible, se cargará la imagen de respaldo especificada en la etiqueta `<img>`.
