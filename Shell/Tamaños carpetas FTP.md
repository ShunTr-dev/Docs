Sacar los tamaños de los archivos en FTP:\ Te conectas al servidor:

```
lftp -u ns3089822.ip-54-36-61.eu,j6JnjgdgPu ftpback-rbx6-7.ovh.net
```
Metes esta línea de código por que los certificados que tenemos son de diferentes versiones y sino se pone no permite la conex

```
set ssl:verify-certificate false
```
Se hace un du con las carpetas:

```
du -hs . ./crabim ./estaticos ./moncake ./primate ./tiendas ./wordpress ./welfaretracker 
```
Salida: 27/10/2020

```
495G    .
480M    ./crabim
5.0G    ./estaticos
313G    ./moncake
111G    ./primate
29G     ./tiendas
37G     ./wordpress
1.6G    ./welfaretracker
```
SI quieres hacer esto en el servidor....

```
du -h --max-depth=1
```