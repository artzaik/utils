# utils


## Comprimir / Descomprimir
```
Archivos .tar.gz:
Comprimir: tar -czvf empaquetado.tar.gz /carpeta/a/empaquetar/
Descomprimir: tar -xzvf archivo.tar.gz

Archivos .tar.bz2
Comprimir: tar -jcfv empaquetado.tar.gz /carpeta/a/empaquetar/
Descomprimir: tar -jxfv archivo.tar.gz

Archivos .tar:
Empaquetar: tar -cvf paquete.tar /dir/a/comprimir/
Desempaquetar: tar -xvf paquete.tar

Archivos .gz:
Comprimir: gzip -9 index.php
Descomprimir: gzip -d index.php.gz

Archivos .zip:
Comprimir: zip archivo.zip carpeta
Descomprimir: unzip archivo.zip
```

## Borrar completamente paquetes, hasta sus ficheros de configuracion
```
dpkg --purge $(dpkg --list | grep ^rc | awk  '{ print $2; }')

```

## Change Encoding:
```
iconv -f old-encoding -t new-encoding file.txt > newfile.txt
```
## Supported encodings with (that's a lower-case L, not a one):
```
iconv -l 
```

## Echo coloreados
```
black='\E[30;47m'
red='\E[31;47m'
green='\E[32;47m'
yellow='\E[33;47m'
blue='\E[34;47m'
magenta='\E[35;47m'
cyan='\E[36;47m'
white='\E[37;47m'

\033[1m -> BOLD
\033[0m -> NORMAL
```
