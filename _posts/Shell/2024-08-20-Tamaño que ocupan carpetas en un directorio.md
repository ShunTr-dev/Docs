---
title: Tamaño que ocupan carpetas en un directorio
date: 2024-08-20 00:00:00 -100
categories: [Shell]
tags: [herramientas]
---

# Tamaño de Carpetas

Para conocer el tamaño que ocupan las carpetas en un directorio, puedes utilizar el siguiente comando:

```bash
du -h --max-depth=1
```

Este comando mostrará el tamaño de las carpetas presentes en el directorio actual, indicando el tamaño de cada una en un formato legible para humanos (`-h`) y limitando la profundidad de la búsqueda a 1 nivel (`--max-depth=1`).
