---
title: Tamaños carpetas FTP
date: 2024-08-20 00:00:00 -100
categories: [Shell]
tags: [shell, ftp]
---

# Tamaños de Carpetas en FTP

Para obtener los tamaños de los archivos en un servidor FTP, puedes seguir estos pasos:

1. Conéctate al servidor FTP utilizando el cliente `lftp`:

```bash
lftp -u ns3089822.ip-54-36-61.eu,j6JnjgdgPu ftpback-rbx6-7.ovh.net
```

2. Es posible que necesites desactivar la verificación de certificados si estás experimentando problemas de conexión debido a diferentes versiones de certificados:

```bash
set ssl:verify-certificate false
```

3. Realiza un comando `du` para obtener los tamaños de las carpetas en el servidor FTP. Por ejemplo, para obtener los tamaños de las carpetas específicas que mencionas:

```bash
du -hs . ./web ./img ./resources
```

La salida de este comando te proporcionará los tamaños de las carpetas en el servidor FTP.

Si prefieres realizar esta operación en el propio servidor, puedes utilizar el siguiente comando:

```bash
du -h --max-depth=1
```

Este comando te dará el tamaño de las carpetas en el servidor FTP limitando la profundidad de la búsqueda a 1 nivel.
