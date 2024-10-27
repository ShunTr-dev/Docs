---
title: Agrupar details
date: 2024-04-01 00:00:00 -100
categories: [HTML, Code-snippet sin JS]
tags: [herramientas]
---

En HTML, puedes usar el atributo `name` para agrupar elementos de `details` y `summary` juntos, de modo que cuando uno se abre, los demás se cierren automáticamente. Esto se logra utilizando la misma cadena de texto en el atributo `name` de cada elemento `details` que deseas agrupar. Aquí te muestro un ejemplo:

```html
<style type="text/css">
    details {
        margin-bottom: 8px;
        border-radius: 4px;
        border: 1px solid #ccc;
        padding: 16px;
        transition: all .2 ease;
    }

    details[open] {
        background: #09f;
    }
</style>


<details name="grupo1" open>
    <summary>Grupo 1</summary>
    Contenido del Grupo 1
</details>

<details name="grupo1">
    <summary>Grupo 1</summary>
    Otro contenido del Grupo 1
</details>

<details name="grupo2">
    <summary>Grupo 2</summary>
    Contenido del Grupo 2
</details>

<details name="grupo2">
    <summary>Grupo 2</summary>
    Otro contenido del Grupo 2
</details>
```

En este ejemplo, hay dos grupos: "Grupo 1" y "Grupo 2". Cada grupo tiene dos elementos `details`. Cuando hagas clic en el resumen de uno de los detalles de un grupo, se abrirá ese detalle y se cerrarán automáticamente todos los detalles del mismo grupo debido a que tienen el mismo valor en el atributo `name`. Sin embargo, los detalles de diferentes grupos no se cerrarán entre sí. Esto permite que solo se pueda abrir un detalle a la vez dentro del mismo grupo.