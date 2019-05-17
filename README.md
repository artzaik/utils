# utils

## SSH legacy
```Shell
ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 123.123.123.123
```
source: https://unix.stackexchange.com/questions/340844/how-to-enable-diffie-hellman-group1-sha1-key-exchange-on-debian-8-0

## Comprimir / Descomprimir
```Shell
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
```Shell
dpkg --purge $(dpkg --list | grep ^rc | awk  '{ print $2; }')

```

## Change Encoding:
```Shell
iconv -f old-encoding -t new-encoding file.txt > newfile.txt
```
## Supported encodings with (that's a lower-case L, not a one):
```Shell
iconv -l 
```

## Echo coloreados
```Shell
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

## Readme.md resources

- Code highlight list: https://github.com/github/linguist/blob/master/lib/linguist/languages.yml
- MD Help: https://help.github.com/categories/writing-on-github/

## Change MKV audio position and default ffmpeg
```Shell
ffmpeg -i input.mkv -map 0:v:0 -map 0:a:1 -map 0:a:2 -map 0:a:0 -disposition:a:0 default -disposition:a:1 none -disposition:a:2 none -c copy output.mkv
```

## Find text in files
```Shell
grep -rnw '/path/to/somewhere/' -e 'pattern'
```
  -r or -R is recursive,
  -n is line number, and
  -w stands for match the whole word.
  -l (lower-case L) can be added to just give the file name of matching files.

Along with these, --exclude, --include, --exclude-dir flags could be used for efficient searching:

  This will only search through those files which have .c or .h extensions:
```Shell
    grep --include=\*.{c,h} -rnw '/path/to/somewhere/' -e "pattern"
```
  This will exclude searching all the files ending with .o extension:
```Shell
    grep --exclude=*.o -rnw '/path/to/somewhere/' -e "pattern"
```
For directories it's possible to exclude a particular directory(ies) through --exclude-dir parameter. For example, this will exclude the dirs dir1/, dir2/ and all of them matching *.dst/:
```Shell
    grep --exclude-dir={dir1,dir2,*.dst} -rnw '/path/to/somewhere/' -e "pattern"
```

## Regular Expressions
1 - IPv4
```Shell
^((^|\.)((25[0-5])|(2[0-4]\d)|(1\d\d)|([1-9]?\d))){4}$
```
2 - Netmask
```Shell
^(((255\.){3}(255|254|252|248|240|224|192|128|0+))|((255\.){2}(255|254|252|248|240|224|192|128|0+)\.0)|((255\.)(255|254|252|248|240|224|192|128|0+)(\.0+){2})|((255|254|252|248|240|224|192|128|0+)(\.0+){3}))$
```
https://www.regextester.com/97579
