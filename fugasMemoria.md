# Buscar fugas de memoria

Para buscar fugas de memoria se puede usar Valgrind.

## Añadir Valgrind

Para añadir Valgrind, hay que añadirlo al packagegroup, ya que ya tenemos la receta

En mi caso, lo he añadido a packagegroup-ca16-development.bb en RDEPENDS_${PN}

```Shell
RDEPENDS_${PN} = "\
        sshfs-fuse \
        i2c-tools \
        gdb \
        gdbserver \
        iperf \
        managementtask-debug \
        opkg-devconf \
        valgrind \
        valgrind-dbg \
        "
```

Generamos la imagen y listo.

## Obtener las trazas correctamente

Para que cuando Valgrind detecte una fuga te diga exactamente donde es (y valga para algo, ya que que te diga que tienes una fuga pero no donde es como no decir nada) hay que añadir el modo debug.

* Valgrind no tiene que stripearse. Para esto añadimos en la receta de valgrind lo siguiente:
```Shell
INHIBIT_PACKAGE_STRIP = "1"
```
IMPORTANTE: Este cambio hará que se recompile casi TODA la imagen, tarda horas, y la Imagen ocupa MUCHO mas.

* Los proyectos deben compilarse en modo debug. Esto se puede hacer añadiendo esto a las recetas:
```Shell
INHIBIT_PACKAGE_STRIP = "1"

SELECTED_OPTIMIZATION = "${DEBUG_FLAGS}"
```
Tambien se puede añadir -g a los flags en el Makefile en los proyectos devtooleados

## Lanzar el proceso

Una vez que tenemos todos grabado ya en el modulo, paramos el proceso si lo ha arrancado systemd y lo tenemos que lanzar a mano. Yo he usado esto:
```Shell
valgrind --track-fds=yes --track-origins=yes --leak-check=full  --show-leak-kinds=all -v controlador
```
Si el comando usa parametros se añaden sin problemas al final.

IMPORTANTE: El resumen donde te dice donde hay fugas DIRECTAS (son las importantes, normalmente si arreglas las directas, se arreglan las indirectas) aparece cuando acaba el proceso. Si es un proceso que no para, hay que añadir algo en el proceso para provocar un cierre ordenado del proceso liberando todo correctamente. (no lo matéis a pelo).
