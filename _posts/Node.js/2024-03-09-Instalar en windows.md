---
title: Instalar en windows
date: 2024-03-09 00:00:00 -100
categories: [Node.js]
tags: [herramientas]
---

# Instalar en Windows Node.js

Para instalar Node.js en Windows, sigue estos pasos:

1. **Ejecutar PowerShell como administrador:** Abre PowerShell en tu sistema Windows como administrador. Puedes hacerlo buscando "PowerShell" en el menú de inicio, haciendo clic derecho sobre él y seleccionando "Ejecutar como administrador".

2. **Instalar Chocolatey:** Chocolatey es un gestor de paquetes para Windows que facilita la instalación de software. Para instalarlo, ejecuta los siguientes comandos en PowerShell:

```powershell
Get-ExecutionPolicy
```

Si el resultado es `Restricted`, ejecuta el siguiente comando para cambiar la política de ejecución:

```powershell
Set-ExecutionPolicy AllSigned
```

Luego, ejecuta el siguiente comando para instalar Chocolatey:

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

3. **Verificar la instalación de Chocolatey:** Para asegurarte de que Chocolatey se haya instalado correctamente, puedes ejecutar el siguiente comando en PowerShell:

```powershell
choco -v
```

4. **Instalar Node.js:** Una vez que tienes Chocolatey instalado, puedes usarlo para instalar Node.js fácilmente. Ejecuta el siguiente comando en PowerShell:

```powershell
choco install nodejs.install
```

Durante la instalación, se te pedirá que confirmes la instalación. Presiona "A" y luego "Enter" para instalar todo.

5. **Verificar la instalación de Node.js:** Después de la instalación, puedes verificar que Node.js se haya instalado correctamente ejecutando los siguientes comandos en PowerShell:

```powershell
node -v
npm -v
```

Esto te mostrará las versiones de Node.js y npm instaladas en tu sistema.