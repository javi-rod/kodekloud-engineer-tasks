# Linux Nivel 2

## Tarea 6 - Comando Find de Linux

#### Durante una auditoría de seguridad rutinaria, el equipo identificó un problema en el Nautilus App Server. Se identificó contenido malicioso en el código del sitio web. Tras investigar el problema, descubrieron que podría haber más archivos infectados. Antes de realizar una limpieza, les gustaría encontrar todos los archivos similares y copiarlos a una ubicación segura para su posterior investigación. Realice la tarea según los siguientes requisitos:

#### a. En App Server 3, en la ubicación /var/www/html/blog, busque todos los archivos (no directorios) que tengan la extensión .php.

#### b. Copie todos esos archivos junto con su estructura de directorios padre a la ubicación /blog en el mismo servidor.

#### c. Asegúrese de no copiar todo el contenido del directorio /var/www/html/blog.

Nos conectaremos vía SSH al servidor correspondiente, en este caso APP Server 3.

```bash
$ ssh banner@172.16.238.12
```

![Conexión ssh al servidor](/img/LINUX/LinuxL02/Task06_01_ssh.png)

Una vez conectados, vamos hacer una búsqueda con el comando find pasando además el comando wc con la opción -l, esto nos permite ver el número de ficheros con extensión php.

```bash
$ find /var/www/html/blog -type f -name '*.php' | wc -l
```

![Búsqueda y recuento de apariciones](/img/LINUX/LinuxL02/Task06_02_find_wc.png)

Como vemos, tenemos 1077 ficheros php.

Ahora vamos a volver a buscar los ficheros y los copiaremos en el directorio que nos indica el ejercicio, teniendo en cuenta que hay que respetar la estructura. Usaremos el comando sudo para poder copiar los ficheros en el destino.

```bash
$ sudo find /var/www/html/blog -type f -name "*.php" -exec bash -c 'dir="/blog/$(dirname "{}")"; mkdir -p "$dir"; cp "{}" "$dir"' \;
```

A continuación, una explicación más detallada de qué hace el comando.

• find /var/www/html/blog -type f -name "\*.php": Con esto realizamos la búsqueda de todos los archivos (no directorios) con extensión .php en el directorio /var/www/html/blog.

• -exec bash -c '...' \;: Esta opción le dice a find que ejecute el comando especificado en '...' para cada archivo encontrado. El \; al final indica el fin del comando -exec.

• 'dir="/blog/$(dirname "{}")"; mkdir -p "$dir"; cp "{}" "$dir"': Este es el comando que se ejecuta para cada archivo encontrado. Aquí, {} es un marcador de posición que find reemplaza con el nombre de cada archivo encontrado.

- dir="/blog/$(dirname "{}")": Aquí, dirname "{}" obtiene el nombre del directorio del archivo actual, y luego se concatena con "/blog/" para obtener la ruta del directorio de destino. El resultado se guarda en la variable dir.

- mkdir -p "$dir": Este comando crea el directorio de destino (y cualquier directorio padre necesario) si no existe.

- cp "{}" "$dir": Este comando copia el archivo actual al directorio de destino.

![Buscar y copiar ficheros](/img/LINUX/LinuxL02/Task06_03_find_exec.png)

Si ahora listamos el contenido del directorio /blog/var/html/blog/ veremos los ficheros copiados así como los directorios de la estructura.

![Listar directorio](/img/LINUX/LinuxL02/Task06_04_ls.png)

Para verificar que se han copiado todos, ejecutaremos el comando siguiente

```bash
$ find /blog -type f -name '*.php' | wc -l
```

![Búsqueda y recuento de ficheros](/img/LINUX/LinuxL02/Task06_05_find_wc.png)

Como vemos, aparece el mismo número de ficheros.
