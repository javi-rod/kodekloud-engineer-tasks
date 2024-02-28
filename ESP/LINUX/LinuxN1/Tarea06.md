# Linux Nivel 1

## Tarea 6 - Archivos de usuario Linux

#### El equipo de soporte de producción de Nautilus en Stratos DC copió algunos datos de usuarios en Nautilus App Server 2 en la ubicación /home/usersdata. Más tarde se dieron cuenta de que habían mezclado por error diferentes datos de usuario. Ahora quieren filtrar algunos datos de usuario y copiarlos a otra ubicación. Encuentre los detalles a continuación:

#### En App Server 2 encuentre todos los archivos (no directorios) propiedad del usuario james dentro del directorio /home/usersdata y cópielos todos manteniendo la estructura de carpetas (conserve la ruta de los directorios) al directorio /media.

Para hacer la búsqueda de los ficheros del directorio usaremos el comando find, usando -type f para indicar que queremos buscar ficheros, ademas de usar -exec para después ejecutar un comando, en este caso un cp. Usaremos --parents para mantener la estructura de directorios. Las {} serán remplazadas por los ficheros y el \; representa el fin del comando exec.

```bash
$ find /home/usersdata -type f -user james -exec cp --parents {} /media \;
```

![Comando find](/img/LINUX/LinuxL01/Task06_01_find.png)

La manera de comprobar que realmente se han copiado todos los ficheros es la siguiente, usaremos el comando find con la ruta origen como se muestra y añadimos una | para que se ejecute el comando wc -l para ver el número de ficheros. Ese mismo comando lo lanzamos con la ruta destino sin el usuario en este caso y debemos ver que ambas salidas devuelven el mismo valor.

```bash
$ find /home/usersdata -type f -user james| wc -l
```

```bash
$ find /media/home/userdata/ -type f | wc -l
```

![Comando find](/img/LINUX/LinuxL01/Task06_02_find.png)

Como vemos ambas devuelven el mismo valor, por lo que hemos realizado bien la copia.

En este caso podríamos haber ejecutado en un primer momento el comando siguiente ahorrando un paso.

```bash
$ find /home/usersdata -type f -user james -exec cp --parents {} /media \; -print | wc -l
```
