---
title: Comprimir
date: 2024-08-20 00:00:00 -100
categories: [Shell]
tags: [herramientas]
---

# Comandos para Comprimir Archivos

### Archivos .tar.gz:

#### Comprimir:

```bash
tar -czvf empaquetado.tar.gz /carpeta/a/empaquetar/
```

#### Descomprimir:

```bash
tar -xzvf archivo.tar.gz
```

### Archivos .tar:

#### Empaquetar:

```bash
tar -cvf paquete.tar /dir/a/comprimir/
```

#### Desempaquetar:

```bash
tar -xvf paquete.tar
```

### Archivos .gz:

#### Comprimir:

```bash
gzip -9 index.php
```

#### Descomprimir:

```bash
gzip -d index.php.gz
```

### Archivos .zip:

#### Comprimir:

```bash
zip archivo.zip carpeta
```

#### Descomprimir:

```bash
unzip archivo.zip
```
