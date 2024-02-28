# Linux Nivel 1

## Tarea 8 - Archivos Linux

#### En el servidor de almacenamiento Nautilus en Stratos DC, hay una ubicación de almacenamiento llamada /data, que es utilizada por diferentes desarrolladores para guardar sus datos (datos no confidenciales). Uno de los desarrolladores llamado mariyam ha planteado un ticket y pidió una copia de sus datos presentes en /data/mariyam en el servidor de almacenamiento. /home es una ubicación FTP en el propio servidor de almacenamiento donde los desarrolladores pueden descargar sus datos. A continuación se presentan las instrucciones compartidas por el equipo de administración del sistema para llevar a cabo esta tarea.

#### - Haga un archivo comprimido mariyam.tar.gz del directorio /data/mariyam y mueva el archivo al directorio /home en el servidor de almacenamiento.

Una vez conectados al servidor, iremos al directorio /data y listaremos el contenido de éste y del directorio de mariyam.

```bash
$ cd /data/
```

```bash
$ ls
```

```bash
$ ls -al mariyam/
```

![comando cd](/img/LINUX/LinuxL01/Task08_01_cd.png)

Como podemos ver, en el directorio /mariyam hay 3 ficheros .txt. Para comprimir el directorio y su contenido usaremos el comando siguiente

```bash
$ tar zcvf mariyam.tar.gz /data/mariyam
```

Opciones del comando:

- z : Para comprir el archivo usando gzip

- c : Para crear un nuevo archivo

- v : Muestra por pantalla lo que se está realizando

- f : Indica que el siguiente argumento es el nombre del archivo

![comando tar](/img/LINUX/LinuxL01/Task08_02_tar_zcfv.png)

Para comprobar que se ha creado el archivo .tar.gz ejecutaremos un ls -al en /data

```bash
$ ls -al
```

![comando ls](/img/LINUX/LinuxL01/Task08_03_ls_al.png)

Si queremos asegurarnos que el archivo crado contiene los archivos .txt ejecutaremos el comando siguiente.

```bash
$ tar tvf mariyam.tar.gz
```

La diferencia del comando con respecto el anterior, es el uso de la opción t que es la que nos muestra un listado del contenido del archivo. Así verificamos que se ha incluido todo el contenido.

![comando tar](/img/LINUX/LinuxL01/Task08_04_tar_tvf.png)

Para mover el archivo ejecutaremos el comando mv y después listaremos el contenido del directorio de destino.

```bash
$ sudo mv mariyam.tar.gz /home/
```

```bash
$ ls -al /home/
```

![comando sudo mv](/img/LINUX/LinuxL01/Task08_05_sudo_mv.png)

Como se aprecia en la imagen anterior, se ha movido el archivo mariyam.tar.gz
