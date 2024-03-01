Ejecutar el powershell de windows como administrador.

Procedemos a instalar Cholatey, que es un gestor de paquetes para windows.

Ejecuta para saber el estado de los paquetes instalados

```
Get-ExecutionPolicy
```
Si devuelve Restricted ejecuta:

```
Set-ExecutionPolicy AllSigned
```
Con esto ponemos todos los paquetes como firmados "AllSigned".

Ejecutamos el siguiente comando para instalar chocolatey.

```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```
Para comprobar si la instalación finalizó correctamente puedes ejecutar:

```
choco -v
```
Para instalar node.js

```
choco install nodejs.install
```
Le damos a la A para instalar todo. Para comprobar que la instalación se realizó correctamente ejecutamos:

```
node -v
npm -v
```