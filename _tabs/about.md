---
# the default layout is 'page'
icon: fas fa-info-circle
order: 4
---

> Add Markdown syntax content to file `_tabs/about.md`{: .filepath } and it will show up on this page.
{: .prompt-tip }








### Cómo se hizo este sitio:

Para empezar hay que instalar [jekyll](https://jekyllrb.com/) con sus dependencias.
Pero no hace falta empezar desde cero, puedes usar un template como [chirpy](https://github.com/cotes2020/jekyll-theme-chirpy?tab=readme-ov-file) para crear el proyecto.

Puedes usar la plantilla clickando en el botón de ["Use this template"](https://github.com/cotes2020/chirpy-starter) y empezar un repo nuevo a partir de esa plantilla.

Y puedes ver la documentación [aquí](https://chirpy.cotes.page/posts/getting-started/).

Una vez que tienes el repo creado y en local. Hay que instalar las dependencias:

```bash
bundle
```

Para levantar el servicio en local:

```bash
bundle exec jekyll s
```

Con esto ya tenemos todo corriendo. Para configurar el sitio se puede configurar en el `_config.yml`